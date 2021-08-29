# Apache Kafka Producers.



## Producers.
* Producer write data to topics(which is made of partitions)
* Producers automatically know to which broker and partition to write to.
* In case of broker failure, producer will automatically recover



## ## Producers Acknowledgment
* Producer can choose to receive acknowledgment of data writes:
    * acks=0 Producer won't wait for acknowledgment (possible data loss)
    * acks=1 Producer will wait for leader acknowledgment (limited data loss)
    * acks=all Leader + replicas(ISR) acknowledgment (no data loss)



## Producers. Message keys.
* Producers can choose to send a KEY with the message (string, number, etc...)
* If KEY=null(key is not set), data is sent round robin (broker 1 and 2 then 3)
* If KEY is sent, then all messages for that key will alloys go to the same partition.
* A KEY is basically sent if you need message ordering for a specific field (ex:truck_id)
* Advanced: we get this guarantee thanks to 'KEY HASHING', which depends on the number of partitions.



## Producer retries.
* In case of transient failures, developer are expected to handle exceptions, otherwise the data will be lost
* Example of transient failure:
  * NotEnoughReplicasExceptions
* There is retries settings 
  * defaults to 0 for Kafka <= 2.1
  * defaults to 2147483647 for Kafka >= 2.1
* The `retry.backoff.ms` setting is by default 100 ms



## Producer timeouts.
* If retries > 0, for example retries 2147483647 the producer won't try request for ever, it's bounded by a timeout.
* For this, you can set an intuitive Producer timeout (KIP-91 Kafka 2.1)
* `delivery.timeout.ms` = 120 000 ms == 2 minutes
* Records will be failed if they can't be acknowledged in `delivery.timeout.ms`



## Producer retries warnings.
* In case of retries, there is a chance that messages will be sent out of order(if a batch has failed to be sent)
* If you rely on key-based ordering, that can be an issue.
* For this you can set the setting while controls how many producers requests can be made in parallel `max.in.flight.requests.per.connection`
  * Default 5
  * Set it to I if you need ensure ordering (may impact throughput)
* In Kafka >= 1.0.0, there's a better solution with idempotent producers!



## Idempotent Producer.
* Idempotent producers are great to guarantee a stable and safe pipeline.
* They con with:
  * retries == Integer.MAX_VALUE
  * `max.flight.requests` = 1 (Kafka == 0.11) or
  * `max.flight.requests` = 5 (Kafka >= 1.0 - higher performance & keep ordering). See [link](https://issues.apache.org/jira/browse/KAFKA-5494)
  * acks=all
* These settings applied automaticaly after your producer has started if you don't set them manually.
* Just set `enable.idempotency`=true



## Safe producer summary.
* Kafka < 0.11
  * `acks`=all (producer level)
    * ensures data is properly replicated before an ack is received
  * `min.insync.replicas`=2 (broker/topic level)
    * ensure two brokers in ISR at least have the data after an ack
  * `retries`=MAX_INT (producer level)
    * ensure transient errors are retried indefinitely
  * `max.in.flight.requests.per.connection`=1 (producer level)
    * Ensures only one request is tried at any time, preventing message re-ordering in case of retries.

* Kafka >=0.11
  * `enable.idempotence`=true (producer level) + `min.insync.replicas`=2 (broker/topic level)
    * implies `acks=all`, `retries=MAX_INT`, `max.in.flight.requests.per.connection=1` if Kafka 0.11 or if Kafka >=1.0 
    * while keeping ordering guarantees and improving performance!

* Runnin a 'safe producer' might impact throughput and latency, always test for your use cases 




## Message Compression.
* Producer usually send data that is text-based, for example with JSON data.
* In this case, it is important to apply compression to the producer.
* Compression is enabled at the producer level and doesn't requiere any configuration change in the brokers or in the consumers
* `compresion.type` can be `none`(default),`gzip`, `lz4`, `snappy` 
* Compression is more effective the bigger the batch of message being sent to Kafka! 
* The compressed batch has the following advantages:
  * Much smaller producer request size (compression ration up to 4x!)
  * Faster to transfer over the network => less latency.
  * Better throughput 
  * Better disc utilization in Kafka (storage message on disk are smaller)
* Disadvantages:
  * Producer must commit some CPU cycle to compress.
  * Consumer must commit some CPU cycle to decompress.
* Overall:
  * Consider testing `snappy` or `lz4` for optimal speed/compression ratio.



## Message Compression Recommendations.
* Find a compression algorithm that gives you the best performance for your specific data. Test all of them!
  * Always use compression in production and specially if you have high throughput.
  * Consider tweaking `linger.ms` and `batch.size` to have bigger batches, and therefore more compression and higher throughput




## Producers batching.
* By default, Kafka tries to send records as soon as posible:
  * It will have up to 5 requests in flight, meaning up to 5 messages individually send at the same time.
  * After this, if more messages have to be sent while others are in flight, Kafka is smart and will start batching 
    them while they wait to send them all at once.
* This smart batching allows Kafka to increase throughput while maintaining very low latency.
* Batches have higher compression ratio so better efficiency.



## `linger.ms` & `batch.size`
* `linger.ms` number of milliseconds a produce is willing to wait before sending a batch out. (default 0)
* By introducing some lag(for example `linger.ms`=5), we increase the chance of messages being sent together in a batch.
* So at the expense of introducing a small delay, we can increase throughput, compression and efficiency of your producer.
* If a batch is full(see `batch.size`) before the end ot the `linger.ms` period, it will be sent to Kafka right away!
* `batch.size` maximum number of bytes that will be included in a batch. The default is `16KB`
* Increase a batch size to something like `32KB` or `64KB` can help increasing the compression, throughput, and efficiency of request.
* Any message that is bigger than the batch size will not be batched.
* A batch is allocated per partition, so make sure that you don't set it to a number that's too high, otherwise you'll run waste memory!
* (Note: you can monitor the average batch size metric using Kafka Producer metrics)


## Producer default partitioner and how keys are hashed.
* By default, your keys are hashed using the `murmur2` algorithm.
* It is most likely preferred to not override the behavior of the partitioner, but it is posible to do so (partitioner.class)
* The formula is: `targetPartition = Utils.abs(Utils.murmur2(record.key())) % numPartitions;`
* This means that same key will go to  the same partition, and adding partitions to a topic will completely alter the formula.



## `max.block.ms` & `buffer.memory`
* If the producer produces faster that the broker can take, the records will be buffered in memory
* `buffer-memory`=33554432 (32MB) the size of the send buffer.
* That buffer will fill up over time and fill back down when the throughput to the broker increases.
* If that buffer is full (all 32MB), then the `send()` method will start to block(won't return right away)
* `mas.block.ms`=60000: the time the `send()` will bock until throwing an exception. Exceptions are basically thrown when:
  * The producer has failed up its buffer
  * The broker is no t accepting any new date
  * 60 seconds has elapsed.
* If you hit an exception hit that usually means your brokers are down or overloaded as they can't respond to requests.



## `min.insync.replicas`
* `acks=all` must be used in conjunction with `min.insync.replicas` 
* `min.insync.replicas` can be set at the broker or topic level (override)
* `min.insync.replicas=2` implies that at least 2 brokers that are ISR (including leader) must respond that they have the data
* that means if you use `replication.factor=3`, `min.insync=2`, `acks=all`, you can only tolerate 1 broker going down, 
  otherwise the producer will receive an exception on send.



## `unclean.leader.election`
* if all of you in sync replicas dies (but you still have out of sync replicas up), you have the following options:
  * wait for an ISR to come back online (default)
  * enable `unclean.leader.election=true` and start producing to non ISR partitions
* if you enable `unclean.leader.election=true`, you improve availability, but you will lose data because other messages on ISR will be discarded
* overall this is a very dangerous setting and its implication must be understood fully before enabling it.
  * user cases include: metrics collection, log collections, and other cases where data loss is somewhat acceptable, at the trade-off of availability.












