# Apache Kafka Schema Registry.



## 
* The schema registry has to be a separated component
* Producers and Consumers need to be able to talk to it
* The Schema Registry must be able to reject bad data
* A common data format must be agreed upon
  * It needs to support schemas 
  * It needs to support evolution 
  * It needs to be lightweight



## Confluent Schema Registry Purposes
* Store and retrieve schemas for Producers/Consumers
* Enforce backward/forward/full compatibility on topics
* Decrease the size of the payload of data sent to Kafka


