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





## Brokers.
* A Kafka cluster is composed of multiple brokers(servers)


## Topic.
* Topic: A particular stream of data.
  * Similar tu table in the database (without all the constrains).
  * You can have as many topics as you want.
  * A topic is identified by its name
* Topics are split in partitions.
* Data is kept only for limited time (default is one week) 



## Partition.
* Each partition is ordered.
* Each message within a partition gets a incremental id, called offset.
* Order is guaranteed only within a partition (no across partitions)
* Once the data is written to a partition, it can't be changed(immutability)
* Data is assigned randomly to a partition unless a key is provided



## Offsets.
* Offsets only have a meaning for a specific partition.
  * E.g offset 3 in partition 0 doesn't represent the same data as offsets 3 in partition 1



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





## Help.
