# Kafka Client Bi-Directional Compatibility.


* As of Kafka 0.10.2 (introduced in july 2017), your clients & Kafka Brokers have compatibility called be-directional
  compatibility (because API calls are now versioned)
* This means:
  * an OLDER client (ex 1.1) can talk to a NEWER broker (2.0)
  * A NEWER client (ex 2.0) can talk to an OLDER broker (1.1) 
* Bottom lines: always use the latest client library version if you can.
* [Link](https://www.confluent.io/blog/upgrading-apache-kafka-clients-just-got-easier/)




