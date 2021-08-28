# Apache Kafka Consumers Groups.



## Consumers Groups.
* Consumers read data in consumer group.
* Each consumer within a group reads from exclusive partitions.
* If you have more consumers than partitions, some consumers will be inactive.
* Consumers will automatically use a GroupCoordinator and a ConsumerCoordinator assign a consumers to a partition.
* To act like a queue, put all your consumers in one group.
* To act like a pub/sub, put each consumer in a unique group.

* Consumers Groups subscribe to a topic, not to a specific partition



## Consumer rebalances into consumers Groups.



## Replaying data for consumers.
* To replay data for a consumer group:
  * Take all the consumers from a specific group down
  * Use `kafka-consuemer-group` command to set offsets to what you want
  * Restart consumers.
  
* Bottom line:
  * Set property data retention period & offsets retention period
  * Ensure the auto offset reset behavior is the one you expect/want
  * Use replay capability in case of unexpected behavior.



## Consumer heartbeat thread.
* `sesion.timeout.ms` (default 10 seconds)
  * heartbeat are sent periodically to the broker
  * if no heartbeat is sent during that period, the consumer is considered dead
  * set even lower to faster consumer rebalances
* `heartbeat.interval.ms` (default 3 seconds)
  * how often to sent heartbeats
  * usually set to 1/3rd of `sesion.timeout.ms`

* take-away: this mechanism is used to detect a consumer application being down. 



## Consumer poll thread.
* `max.poll.interval.ms` (default 5 minutes)
  * maximum amount of time between two `.poll()` calls before declaring the consumer dead.
  * this is particularly relevant for `Big Data frameworks` like `Spark` in case the processing takes time
  
* take-away: this mechanism is used to detect a data processing issues with the consumer.
