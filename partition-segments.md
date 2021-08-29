# Apache Kafka Partition Segments



## Partitions and Segments
* Partitions are made of... segments(files)!
* Only one segment is `ACTIVE`(the one data is being writen to)
* Two segments settings:
    * `log.segment.bytes` the max size of a single segment in bytes
    * `log.segment.ms` the time Kafka will wait before committing the segment if not full. (by default is one weak)
* Segments come with two indexes(files)
    * An offset to position index: allows Kafka where to read to find a message
    * A timestamp ot offset index: allows Kafka to find messages with a timestamp
    * Therefore, Kafka knows where to find data in a constant time!



## Segments: Why should I care?
* a smaller `log.segment.byte` (default size: 1GB) means:
  * More segments per partition
  * Log compaction happens more often
  * But Kafka has not keep more files opened (Error: to many open files)
* Ask yourself: how fast will I have new segments based on throughput?
* A smaller `log.segment.ms` (default value 1 week) means:
  * You set a max frequency for log compaction (more frequent triggers)
  * Maybe you want daily compaction instead of weak?
* Ask yourself: how often do I need log compaction to happen?
