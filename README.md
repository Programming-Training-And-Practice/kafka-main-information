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
* Consumer Groups.
* Distributed system.





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
