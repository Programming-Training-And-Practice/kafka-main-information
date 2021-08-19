## Zookeeper




## 
* Zookeeper manages brokers (keep a list of them)
* Zookeeper helps in performing leader election for partitions
* Zookeeper sends notifications to Kafka in case of changes (e.g. new topic, broker dies, broker comes up, delete topic, etc...) 
* Kafka cannot work with Zookeeper. Apache Kafka 2.8. 0 is finally out and you can now have early-access to KIP-500 that removes the Apache Zookeeper dependency.
* Zookeeper by design operates with an odd number of servers.
* Zookeeper has a leader (handle writes) the rest of the servers are followers(handle reads)
