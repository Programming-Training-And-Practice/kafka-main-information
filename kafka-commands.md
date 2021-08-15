# Kafka Terminal Commands.

## Topic.
* `/bin/kafka-topics.sh --create --zookeeper [zookeeperHost:port, zookiperHost:port] --replication-factor 3 --partitions 3 --topic hello-world` - create topic
* `/bin/kafka-topics.sh --list --zookeeper [zookeeperHost:port, zookiperHost:port]` - list topics
* `/bin/kafka-topics.sh --describe --topic hello-world --zookeeper [zookeeperHost:port, zookiperHost:port]` - describe topic
* `/bin/kafka-topics.sh --zookeeper [zookeeperHost:port, zookiperHost:port] --delete --topic hello-world` - delete topic

* `/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list`
* `/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic Orders`
* `/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic Orders --config max.message.bytes=10485760`
* `/bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe`
* `/bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic Order`
* `/bin/kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic Order`

## Producer.
* `/bin/kafka-console-producer --broker-list [kafkaHost:port;kafkaHost:port] --topic hello-world` - create producer
* `/bin/kafka-console-producer --bootstrap-server localhost:9092 --topic hello-world JSON`

* `/bin/kafka-console-producer --topic hola-mundo --property parse.key=true --property key.separator=":" --broker-list [kafkaHost:port;kafkaHost:port]`

## Consumer.
* `/bin/kafka-console-consumer --bootstrap-server [kafkaHost:port;kafkaHost:port] --topic hello-world` - create consumer
* `/bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic hello-world`
* `/bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic hello-world --from-beginning`

* `/bin/kafka-console-consumer --topic hola-mundo --property print-timestamp=true --partition=2 --bootstrap-server [kafkaHost:port;kafkaHost:port]`
* `/bin/kafka-console-consumer --topic hola-mundo --property print-timestamp=true --property print.key=true --property key.separator=":" --partition=2 --bootstrap-server [kafkaHost:port;kafkaHost:port]`

## Configs.
* `/bin/kafka-configs.sh --bootstrap-server localhos:9092 --entiry-type topics --entity-name topicName --alter --add-config max.message.bytes=10485760`
