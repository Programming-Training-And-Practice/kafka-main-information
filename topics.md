# Apache Kafka Topic.



## General.
* [Kafka Topic Naming Conventions](https://cnr.sh/essays/how-paint-bike-shed-kafka-topic-naming-conventions)



## Topic.
* Topic: A particular stream of data.
    * Similar tu table in the database (without all the constrains).
    * You can have as many topics as you want.
    * A topic is identified by its name
* Topics are split in partitions.
* Data is kept only for limited time (default is one week)
* Cuando se crea un topic, por defecto se crean partitions=1 replication-factor=1
* Default size of topic message is 1MB



## Topic replication factor.
* Topics should have a replication factor > 1 (usually between 2 and 3). Three is the gold standard.
* This way if a broker si down, another broker can serve the data.



## Partitions Count and  Replication Factor
* The two most important parameters when creating a topic.
* They impact performance and durability of the system overall
* It is best to get the parameters right the first time.
  * If the `Partitions Count` increase during a topic lifecycle, you will break your keys ordering guarantee
  * If the `Replication Factor` increase during a topic lifecycle, you put more pressure on your cluster, which can 
    lead to unexpected performance decrease.



## Replication Factor
* Should be at least 2, usually 3, maximum 4
* The higher the replication factor (N)
  * Better resilience of your system (N-1 broker can fail)
  * But more replication (higher latency if acks=all)
  * But more disc space on your system (50% more if RF is 3 instead of 2)

* Guidelines:
  * Set it to 3 to get started (you must have at least 3 brokers for that)
  * If replication performance is an issue, get a better broker instead of less RF
  * Never set it to 1 in production


## Why should I care about topic configuration 
* Brokers have defaults for all the topic configuration parameters
* These parameter impact performance and topic behavior
* Some topics may need different values than the defaults
  * Replication factor
  * number of partitions
  * message size 
  * compression level
  * log cleanup policy
  * min insync replicas
  * other configurations
* A list of configuration can be found at [Link](https://kafka.apache.org/documentation/#brokerconfigs)
