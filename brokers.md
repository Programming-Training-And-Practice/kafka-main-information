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


## Clusters Guidelines
* It is pretty much accepted that a broker should not hold more than 2000 to 4000 partitions (across all topic of that broker)
* Additionally, a Kafka cluster should have a maximum of 20,000 partitions across all brokers.
* The reason is that in case of brokers going down, Zookeeper needs to perform a lot of leader elections
* If you need more partitions in your cluster, add brokers instead
* If you need more that 20,000 partitions in your cluster (it will be take time to get there!), follow the Netflix 
  model and create more Kafka clusters.
* Overall, you don't need a topic with 1000 partitions to archive high throughput. Start at a reasonable number  and test the performance



## Kafka Cluster Setup High Level Architecture
* You want multiple brokers in different data center (racks) to distribute your load. You also want a cluster of at least zookeeper



## Kafka Cluster Setup Gotchas
* it's not easy to setup a cluster
* you want to isolate each Zookeeper & Broker on separate server
* monitoring needs to be implemented
* operations have to be mastered
* you need a really good Kafka admin

* Alternative: many different "Kafka as a service" offerings on the web
* No operational burdens (updates, monitoring, setup, etc...)


## Kafka Monitoring and Operations
* Kafka exposes metrics through JMX
* These metrics are highly important for monitoring Kafka, and ensuring the system are behaving correctly under load.
* Common places to host the Kafka metrics:
  * ELK(ElasticSearch + Kibana)
  * Datadog
  * NewRelic
  * Confluent Control Center
  * Prometheus
  * Many others...
* Some of the most important metrics are:
  * Under replicated partitions: number of partitions are have problems with the ISR(in-sync replicas). May indicate a high load on the system
  * Request Handlers: utilization of threads for IO, network, etc... overall utilization of an Apache Kafka broker.
  * Request Timing: how long is takes to reply to requests. Lower is better, as latency will be improved.
* Overall have a look at the documentation here:
  * [Link 1](https://kafka.apache.org/documentation/#monitoring)
  * [Link 2](https://docs.confluent.io/platform/current/kafka/monitoring.html)
  * [Link 3](https://www.datadoghq.com/blog/monitoring-kafka-performance-metrics/)
* Kafka Operations team must be able to perform the following tasks:
  * Rolling restart of Brokers
  * Updating configurations
  * Rebalancing Partitions
  * Increasing replication factor
  * Adding a Broker
  * Replacing a Broker
  * Removing a Broker
  * Updating a Kafka Cluster with zero downtime

