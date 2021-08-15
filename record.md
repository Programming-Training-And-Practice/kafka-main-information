# Apache Kafka Record.





## Kafka Record.
* It is the minimum unit of information.
* The default maximum size of a message is 1MB.
* Similar to a row or record in a table in a relational database.
* It is an array of bytes, so for Kafka it does not have a specific format or meaning.
* A message can optionally have a key associated with it.
* The key is also an array of bytes without formatting or meaning for Kafka.
* It is used as a partitioning key when we want to write messages in a controlled way to Kafka partitions.
* Ensures that messages with the same key are written to the same partition.
* To improve efficiency, messages are written in Kafka in batches called batches.
* A batch is a collection of messages that are written in the same topic and in the same partition.
* They are compressed so that they are transmitted more efficiently.
* It's a compromise between latency and performance.
