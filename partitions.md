# Apache Kafka Partition.



## Partition.
* Each partition is ordered.
* Each message within a partition gets a incremental id, called offset.
* Order is guaranteed only within a partition (no across partitions)
* Once the data is written to a partition, it can't be changed(immutability)
* Data is assigned randomly to a partition unless a key is provided



## Partitions Count and  Replication Factor
* The two most important parameters when creating a topic.
* They impact performance and durability of the system overall
* It is best to get the parameters right the first time.
    * If the `Partitions Count` increase during a topic lifecycle, you will break your keys ordering guarantee
    * If the `Replication Factor` increase during a topic lifecycle, you put more pressure on your cluster, which can
      lead to unexpected performance decrease.


## Partitions Count
* Each partition can handle a throughput of a few MB/s (measure it for your setup!)
* More partitions implies:
  * Better parallelism, better throughput
  * Ability to run more consumers in a group to scale
  * Ability to average more brokers if you have large cluster
  * But more elections to perform for Zookeeper
  * But more files opened on Kafka

* Guidelines:
  * Partitions per topic == million dollar question
    * (Intuition) small cluster (< 6 brokers): 2X #brokers 
    * (Intuition) big cluster (> 12 brokers): 1X #brokers
    * Adjust for number of consumers you need to run in parallel at peak throughput
    * Adjust for producer throughput (increase if super-high throughput or projected increase in the next 2 years)
  * Test! Every Kafka cluster will have different performance
  * Don't create a topic with 1000 partitions!
  
