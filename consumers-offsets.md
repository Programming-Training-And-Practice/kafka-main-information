# Apache Kafka Consumers Offsets.


* Kafka stores the offsets at which a consumer group has been reading
* The offsets committed live in a Kafka topic named '__consumer_offsets'
* When a consumer in a group has process data received from Kafka, its should be committing the offsets.
* If a consumer dies, it will be able to read back from where it left off thanks to the committed consumer offsets.
