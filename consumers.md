# Apache Kafka Consumers.





## Consumers.
* Consumers read data from a topic(identified by name).
* Consumers know which broker to read from.
* In case broker failure, consumers know how to recover.
* Data is read in order within each partitions.





## Delivery semantic for consumers.
* Consumer choose when to commit offsets.
* There are 3 delivery semantics:
  * At most once:
    * Off sets are committed as soon as the message is received.
    * If the processing going wrong, the message will be lost (it won't read again).
  * At least once(usually preferred)
    * Offsets are committed after the message will be processed.
    * If the processing going wrong, the message will be read again.
    * This can result in duplicate processing of messages. Make sure your processing is 
      idempotent(i.e processing again the messages won't impact your system).
  * Exactly once:
    * Can be archived for Kafka => Kafka workflow using Kafka Stream API.
    * For Kafka => External system workflow, use an idempotent consumer.
    * What: 
      * Strong transactional guarantees for kafka.
      * Prevents clients from processing duplicate messages.
      * Handles failures gracefully.
    * Use cases:
      * Tracking ad views.
      * Processing financial transactions.
      * Stream processing.
