# Kafka Terminal Commands.

## Topic.
`/bin/kafka-topics.sh --create --zookeeper [zookeeperHost:port, zookiperHost:port] --replication-factor 3 --partitions 3 --topic hello-world` - create topic
`/bin/kafka-topics.sh --list --zookeeper [zookeeperHost:port, zookiperHost:port]` - list topics
`/bin/kafka-topics.sh --describe --topic hello-world --zookeeper [zookeeperHost:port, zookiperHost:port]` - describe topic
`/bin/kafka-topics.sh --zookeeper [zookeeperHost:port, zookiperHost:port] --delete --topic hello-world` - delete topic

## Producer.
`/bin/kafka-console-producer --topic hello-world --broker-list [kafkaHost:port;kafkaHost:port]`

## Consumer.
`/bin/kafka-console-consumer --topic hello-world --bootstrap-server [kafkaHost:port;kafkaHost:port]`