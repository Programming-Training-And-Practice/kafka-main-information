# Apache Kafka Distributed Commit Log.

## Distributed Commit Log.
* Commit Log, sequence of records ordered by time.
* You can only add new records in order, never modify.
* Each new record is assigned a unique autoincremental record number as a unique identifier or key.
* The order of the records defines a notion of time.
* The log entry identifier or number can be seen as a timestamp of when that record entered the log.
* An integer is used and not a timestamp to avoid problems in distributed systems.
* The logs have a specific purpose, each record indicates what happened and when. They record events.
* Allows decoupled and asynchronous communication between replicas.
* It is used as a consistency mechanism to order the updates that are applied in all the replicas.
* Allows you to manage a distributed state. For this, the data processing has to be deterministic, it is not time dependent.
* Two pieces of deterministic code are fed the same log, will produce the same output and in the same order.
* Two identical deterministic processes that start from the same state and have the same inputs in the same order,
  they will produce the same output and therefore the same state.
