# Apache Kafka Consumers.





## Consumers.
* Consumers read data from a topic(identified by name).
* Consumers know which broker to read from.
* In case broker failure, consumers know how to recover.
* Data is read in order within each partitions.





## Delivery semantic for consumers.
* Consumer choose when to commit offsets.
* There are 3 delivery semantics:
  * `at-most-once`:
    * Off sets are committed as soon as the message is received.
    * If the processing going wrong, the message will be lost (it won't read again).
  * `at-least-once`(usually preferred)
    * Offsets are committed after the message will be processed.
    * If the processing going wrong, the message will be read again.
    * This can result in duplicate processing of messages. Make sure your processing is 
      idempotent(i.e processing again the messages won't impact your system).
  * `exactly once`:
    * Can be archived for Kafka => Kafka workflow using Kafka Stream API.
    * For Kafka => External system workflow, use an idempotent consumer.
    * What: 
      * Strong transactional guarantees for kafka.
      * Prevents clients from processing duplicate messages.
      * Handles failures gracefully.
    * Use cases:
      * Tracking ad views.
      * Processing financial transactions.
      * Stream processing.



## Consumers poll behavior.
* Kafka Consumers have a 'poll' model, while many others messaging bus in enterprises have a 'push' model.
* This allow consumers to control where in the log they want to consume, how fast, and give them the ability to replay events.
* `fetch.min.butes` (default 1)
  * Controls how much data you want to pull at least on each request
  * Helps improving throughput's and decreasing requests number
  * At the const of latency
* `mas.poll.records` (default 500)
  * Controls how many records to receive per poll request.
  * Increase if your messages are very small and have a lot of available RAM
  * Good to monitoring how many records are polled per request.
* `max.partitions.fetch.butes` (default 1MB)
  * Maximum data returned by the broker per partition
  * If you read from 100 partitions, you'll need a lot of memory RAM
* `fetch.max.butes` (default 50MB)
  * Maximum data returned for each fetch request (covers multiple partitions)
  * The consumer performs multiple fetches in parallel.
  * Change these settings only if your consumer maxes out on throughput already.



## Consumer offsets commits  strategies.
* There are two most common patterns for committing offsets in a consumer application.
* 2 strategies:
  * (easy) `enable.auto.commit`=true & synchronous processing of batch.
    * With auto commit, offsets will be committed automatically for you at regular interval 
      (`auto.commit.interval.ms`=5000 by default) every time you call1 `poll()` 
    * If you don't use synchronous processing, you will be in `at-most-once` behavior because offsets will be 
      committed before your data is processed. 
  * (medium) `enable.auto.commit`=false & manual commit of offsets
    * You control when you commit offsets and what's the condition for committing them.
    * Example: accumulating records into a buffer and then flushing the buffer  to a database + committing offsets them.



## Consumer offsets reset behavior.
* The behavior for the consumer is to then use:
  * `auto.offsets.reset=latest` will read from the end of the log
  * `auto.offsets.reset=earliest` will read from the start of the log 
  * `auto.offsets.reset=none` will throw exception if no offset is found
* Additionally, consumer offsets can be lost:
  * If a consumer hasn't read new data in 1 day(Kafka < 2.0)
  * If a consumer hasn't read new data in 7 day(Kafka >= 2.0)
* This can be controlled by the broker settings `offsets.retention.minutes`



















