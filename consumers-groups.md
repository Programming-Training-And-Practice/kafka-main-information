# Apache Kafka Consumers Groups.





## Consumers Groups.
* Consumers read data in consumer group.
* Each consumer within a group reads from exclusive partitions.
* If you have more consumers than partitions, some consumers will be inactive.
* Consumers will automatically use a GroupCoordinator and a ConsumerCoordinator assign a consumers to a partition.
* To act like a queue, put all your consumers in one group.
* To act like a pub/sub, put each consumer in a unique group.
