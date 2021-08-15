# Apache Kafka Partition.





## Partition.
* Each partition is ordered.
* Each message within a partition gets a incremental id, called offset.
* Order is guaranteed only within a partition (no across partitions)
* Once the data is written to a partition, it can't be changed(immutability)
* Data is assigned randomly to a partition unless a key is provided
