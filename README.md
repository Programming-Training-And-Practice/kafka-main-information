# Apache Kafka.





## Contents at a Glance.
* [About.](#about)
* [Documentation.](#documentation)
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
* Publisher.
* Broker.
* Consumer.
* Topic.
* Partition.
* Offsets.
* Consumer Groups.
* Distributed system.





## Kafka API.
* Producer API
* Consumer API
* Kafka Stream
* Kafka Connect

Interface SQL: KSQL





## Brokers.
* A Kafka cluster is composed of multiple brokers(servers)





## Topic.
* Topic: A particular stream of data.
  * Similar tu table in the database (without all the constrains).
  * You can have as many topics as you want.
  * A topic is identified by its name
* Topics are split in partitions.
* Data is kept only for limited time (default is one week) 
* cuando se crea un topic, por defecto se crean partitions=1 replication-factor=1




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
