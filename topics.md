# Apache Kafka Topic.





## Topic.
* Topic: A particular stream of data.
    * Similar tu table in the database (without all the constrains).
    * You can have as many topics as you want.
    * A topic is identified by its name
* Topics are split in partitions.
* Data is kept only for limited time (default is one week)
* Cuando se crea un topic, por defecto se crean partitions=1 replication-factor=1
* Default size of topic message is 1MB





## Topic replication factor.
* Topics should have a replication factor > 1 (usually between 2 and 3). Three is the gold standard.
* This way if a broker si down, another broker can serve the data.
*
