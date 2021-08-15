# Apache Kafka Brokers.





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
