# Apache Kafka Producers.





## Producers.
* Producer write data to topics(which is made of partitions)
* Producers automatically know to which broker and partition to write to.
* In case of broker failure, producer will automatically recover




## ## Producers Acknowledgment
* Producer can choose to receive acknowledgment of data writes:
    * acks=0 Producer won't wait for acknowledgment (possible data loss)
    * acks=1 Producer will wait for leader acknowledgment (limited data loss)
    * acks=all Leader + replicas(ISR) acknowledgment (no data loss)





## Producers. Message keys.
* Producers can choose to send a KEY with the message (string, number, etc...)
* If KEY=null(key is not set), data is sent round robin (broker 1 and 2 then 3)
* If KEY is sent, then all messages for that key will alloys go to the same partition.
* A KEY is basically sent if you need message ordering for a specific field (ex:truck_id)
* Advanced: we get this guarantee thanks to 'KEY HASHING', which depends on the number of partitions.
