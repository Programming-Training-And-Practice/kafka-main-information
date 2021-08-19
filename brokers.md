# Apache Kafka Brokers.



## Brokers.
* A Kafka cluster is composed of multiple brokers(servers).
* Each broker is identified with its id (integer).
* Each broker contains certain topic partitions.
* After connecting to any broker (called bootstrap broker), you will be connected to the entire cluster.
* A good number to get started is 3 broker, but some big clusters have over 100 brokers.



## Concept of leader for a partition.
* At any time only ONE broker can be a leader for a given partition.
* Only that leader can receive and serve data for a partition. In version of Apache Kafka after, version 2.5 it is actually
  posible to read from followers and not just the leader.
* The other brokers will synchronize the data.
* Therefore, each partition has one leader and multiple ISR(in-sync replica).


##
* Every Kafka broker is also called a "bootstrap server".
* That means that you only need to connect to one broker, and you will be connected to the entire cluster.
* Each broker knows about all brokers, topics and partitions(metadata)
