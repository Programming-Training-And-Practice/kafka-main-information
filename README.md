# Apache Kafka.



## Contents at a Glance.
* [About.](#about)
* [Documentation.](#documentation)
* [Kafka terminal commands.](kafka-commands.md)
* [General Concepts.](#general-concepts)
* [Pros.](#pros)
* [Cons.](#cons)
* [Queue vs Pub/Sub](#queue-vs-pubsub)
* [Run in the docker.](#run-in-the-docker)
* [Help.](#help)
* [Apache Avro.](https://github.com/descriptions-of-it-technologies/apache-avro)
* [Apache Kafka Registry.](apache-kafka-schema-registry.md)
* [Brokers.](brokers.md)
* [Consumers.](consumers.md)
* [Consumers Groups.](consumers-groups.md)
* [Consumers Offsets.](consumers-offsets.md)
* [Distributed Commit Log.](distributed-commint-log.md)
* [Offsets.](offsets.md)
* [Partitions.](partitions.md)
* [Producers.](producers.md)
* [Records.](record.md)
* [Topics.](topics.md)



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



## Delivery methods. [Link.](https://kafka.apache.org/documentation/#semantics)
* At least once semantics - A message will be resent if needed until it is acknowledged.
* At most once semantics - A message will only be sent once and not resent on failure.
* Exactly once semantics - A message will only be seen once by the consumer of the message.



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




## Kafka guarantees.
* Message are appended to a topic-partition in the order they are sent. 
* Consumer read message in the order sored in a topic-partition
* With a replication factor of N, producers and consumers can tolerate up to N-1 broker being down.
* This is why replication factor of 3 is a good idea:
  * Allows for one broker to be taken down for maintenance.
  * Allows for another broker to be taken down unexpectedly.
* As long as the number of partitions remains constant for a topic(no new partition), the same key will always go to the same partition.



## Security Overview.
* Kafka supports Encryption in Transit. 
* Kafka supports authentication and authorization.
* No encryption at rest out of the box.
* Clients can be mixed with & without encryption & authentication.

* Using security is optional - But!



## Troubleshooting.
* Confluent control center.
* Log files
* Special config settings
    * SSL logging.
    * Authorizer debugging.

    

## Run in the docker.
`docker run --name kafka -p 9092:9092 
        -e KAFKA_ZOOKEEPER_CONNECT=localhost:2181
        -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092
        -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 
 confluentinc/cp-kafka
`



## Useful links.
* [Conductor.io](https://www.conduktor.io/)
* [KafkaCat](https://github.com/edenhill/kafkacat)



## Help.
