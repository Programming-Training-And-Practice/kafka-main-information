# Log



## Log cleanup policies
* Many Kafka clusters make data expire, according to a policy
* That concept is called log `cleanup`
* Policy 1: `log.cleanup.policy=delete` (Kafka default for all user topics)
  * Delete based on age of data (default is one weak)
  * Delete based on max size of log (default is -1 == infinite)
* Policy 2: `log.cleanup.policy=compact` (Kafka default for topic__consumer_offsets)
  * Delete based on keys of your message
  * Will delete old duplicate keys after the active segment is committed
  * Infinite time and space retention



## Log Cleanup: Why and When?
* Deleting data from Kafka allows you to:
  * Control the size of data on the disk, delete obsolete data
  * Overall: Limit maintenance work on the Kafka Cluster
* How often does log cleanup happen?
  * Log cleanup happen on your partition segments
  * Small/More segment means that log cleanup will happen more often!
  * Log cleanup shouldn't happen to often => take CPU and RAM resource
  * The cleaner checks for work every 15 seconds(`log.cleaner.backoff.ms`)



## Log Cleanup Policy: Delete
* `log.retention.hours`:
  * number of hours to keep data for (default is 168 - one week)
  * high numbers means more disc space
  * lower number means that less data is retained (if your consumers are down for too long, they can miss data)
* `log.retention.bytes`:
  * max size in bytes for each partition (default is -1 == infinite)
  * useful to keep the size of a log under a threshold
* use cases - two commons pair of options:
  * one week of retention:
    * `log.retention.hours=168` and `log.retention.bytes=-1`
  * infinite time retention bounded by 500MB:
    * `log.retention.hours=17520` and `log.retention.bytes=524288000`



## Log Cleanup Policy: Compact
* log compaction ensures that your log contains at least the last known value for a specific key within a partition.
* very useful if we just requiere a snapshot instead of full history (such as for a data table in database)
* the idea is that we only keep the latest update for a key in out log



## Log compaction guarantee
* any consumer that is reading from the tail of a log (most current date) will still see all the messages sent to the topic
* ordering of messages it kept, log compaction only removes some message, but does not re-order them
* the offset of a message is immutable(it never changed). Offsets are just skipped if a message is missing
* deleted records can still be seen by consumer for a period of `delete.retention.ms`(default value is 24 hours)



## Log compaction myth busting
* it doesn't prevent you from pushing duplicates data to Kafka
  * de-duplication is done after a segment is committed
  * your consumers will still read from tail as soon as the data arrives
* it doesn't prevent you from reading duplicate data from Kafka
  * some points as above
* log compaction can fail from time to time
  * it is optimization and it the compaction thread might crash
  * make sure you assign enough memory to it and that it gets triggered
  * restart kafka if log compaction is broken(this is a bug and may get fixed in the future)
* You can't trigger log compaction using API cals(from now...)


## Log compaction
* log compaction is configured by (`log.cleanup.policy=compact`):
  * `segment.ms` (default 7 days) max amount of time to wait to close active segment
  * `segment.byte` (default 1GB) max size of segment
  * `min.compaction.lag.ms` (default 0) how long to wait before message can be compacted
  * `delete.retention.ms` (default 24 hours) wait before deleting data marked for compaction
  * `min.cleanable.dirty.ration` (default 0.5) higher => less, more efficient cleaning. lower => opposite




