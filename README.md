# Apache Kafka.





## Contents at a Glance.
* [About.](#about)
* [Documentation.](#documentation)
* [Kafka terminal commands.](kafka-commands.md)
* [General Concepts.](#general-concepts)
* [Pros.](#pros)
* [Cons.](#cons)
* [Queue vs Pub/Sub](#queue-vs-pubsub)
* [Consumer Groups.](#consumer-groups)
* [Run in the docker.](#run-in-the-docker)
* [Help.](#help)





## About.





## Documentation.





## General Concepts.
* Broker.
* Topic.
* Partition.
* Offsets.
* Publisher.
* Consumer.
* Consumer Groups.
* Distributed system.





## Kafka API.
* Producer API
* Consumer API
* Kafka Stream
* Kafka Connect

Interface SQL: KSQL





## Brokers.
* A Kafka cluster is composed of multiple brokers(servers).
* Each broker is identified with its id (integer).
* Each broker contains certain topic partitions.
* After connecting to any broker (called bootstrap broker), you will be connected to the entire cluster. 
* A good number to get started is 3 broker, but some big clusters have over 100 brokers.
* At any time only ONE broker can be a leader for a given partition.
* Only that leader can receive and serve data for a partition.
* The other brokers will synchronize the data.
* Therefore, each partition has one leader and multiple ISR(in-sync replica).






## Producers.
* Producer write data to topics(which is made of partitions)
* Producers automatically know  to which broker and partition to write to.
* In case of broker failure, producer will automatically recover
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





## Consumers.
* Consumers read data from a topic(identified by name). 
* Consumers know which broker to read from.
* In case broker failure, consumers know how to recover.
* Data is read in order within each partitions. 





## Consumers Groups.
* Consumers read data in consumer group.
* Each consumer within a group reads from exclusive partitions.
* If you have more consumers than partitions, some consumers will be inactive.
* Consumers will automatically use a GroupCoordinator and a ConsumerCoordinator assign a consumers to a partition.





## Consumers Offsets.





## Topic.
* Topic: A particular stream of data.
  * Similar tu table in the database (without all the constrains).
  * You can have as many topics as you want.
  * A topic is identified by its name
* Topics are split in partitions.
* Data is kept only for limited time (default is one week) 
* Cuando se crea un topic, por defecto se crean partitions=1 replication-factor=1
* Default size of topic message is 1MB





## Topic replication factor.
* Topics should have a replication factor > 1 (usually between 2 and 3). Three is the gold standard.
* This way if a broker si down, another broker can serve the data.
* 





## Partition.
* Each partition is ordered.
* Each message within a partition gets a incremental id, called offset.
* Order is guaranteed only within a partition (no across partitions)
* Once the data is written to a partition, it can't be changed(immutability)
* Data is assigned randomly to a partition unless a key is provided





## Offsets.
* Offsets only have a meaning for a specific partition.
  * E.g offset 3 in partition 0 doesn't represent the same data as offsets 3 in partition 1





## Distributed Commit Log.
* Commit Log, sequence of records ordered by time.
* You can only add new records in order, never modify.
* Each new record is assigned a unique autoincremental record number as a unique identifier or key.
* The order of the records defines a notion of time.
* The log entry identifier or number can be seen as a timestamp of when that record entered the log.
* An integer is used and not a timestamp to avoid problems in distributed systems.
* The logs have a specific purpose, each record indicates what happened and when. They record events.
* Allows decoupled and asynchronous communication between replicas.
* It is used as a consistency mechanism to order the updates that are applied in all the replicas.
* Allows you to manage a distributed state. For this, the data processing has to be deterministic, it is not time dependent.
* Two pieces of deterministic code are fed the same log, will produce the same output and in the same order.
* Two identical deterministic processes that start from the same state and have the same inputs in the same order,
  they will produce the same output and therefore the same state.





## Kafka Record.
* It is the minimum unit of information.
* The default maximum size of a message is 1MB.
* Similar to a row or record in a table in a relational database.
* It is an array of bytes, so for Kafka it does not have a specific format or meaning.
* A message can optionally have a key associated with it.
* The key is also an array of bytes without formatting or meaning for Kafka.
* It is used as a partitioning key when we want to write messages in a controlled way to Kafka partitions.
* Ensures that messages with the same key are written to the same partition.
* To improve efficiency, messages are written in Kafka in batches called batches.
* A batch is a collection of messages that are written in the same topic and in the same partition.
* They are compressed so that they are transmitted more efficiently.
* It's a compromise between latency and performance.





## Delivery methods. [Link.](https://kafka.apache.org/documentation/#semantics)
* At least once semantics - A message will be resent if needed until it is acknowledged.
* At most once semantics - A message will only be sent once and not resent on failure.
* Exactly once semantics - A message will only be seen once by the consumer of the message.





## Kafka Registry.





## Apache Avro.





## Pros.
* Append only Commit log.
* Performance.
* Distributed.
* Long polling.
* Event driven, Pub/Sub and Queue.
* Scaling.
* Parallel processing.





## Cons.
* ZooKeeper.
* Producer explicit partition can lead to problems.
* Complex to install, configure and manage.





## Queue vs Pub/Sub.
* Queue: Message published once, consumed once.
* Pub/Sub: Message published once, consumed many times.

* Kafka support both Queue and Pub/Sub.





## Consumer Groups.
* To act like a queue, put all your consumers in one group.
* To act like a pub/sub, put each consumer in a unique group.





## Run in the docker.
`docker run --name kafka -p 9092:9092 
        -e KAFKA_ZOOKEEPER_CONNECT=localhost:2181
        -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092
        -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 
 confluentinc/cp-kafka
`





## Useful links.
* []()





## Help.
