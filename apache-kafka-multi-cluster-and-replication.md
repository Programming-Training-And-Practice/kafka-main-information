# Apache Kafka Multi Cluster and Replication



##
* Kafka can only operate well in a single region(geographical region)
* Therefore, it is very common for enterprise to have Kafka clusters across the world, with some level of replication between them.
* A replication application at its core is just a consumer + a producer
* There are different tools to perform it:
  * Mirror Maker - open source tool that ships with Kafka
  * Netflix uses Flink - they wrote their own application
  * Uber uses uReplicator - address performance and operations issues with MM
  * Comcast has their own open source Kafka Connector Source
  * Confluent has their own Kafka Connect Source

* Overall, try these and see if it works for your use case before writing your own
* There are two designs for cluster replication:
  * Active => Active 
    * You have a global application
    * You have a global dataset
  * Active => Passive
    * You want to have an aggregation cluster (for example for analytic) 
    * You want to create some form of disaster recovery strategy(*its hard)
    * Cloud migration (from on-premise cluster to Cloud Cluster)
  * Replicating doesn't preserve offsets, just data!
  * Optimization resources online:
    * [Kafka mirroring (MirrorMaker)](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330)
    * [MirrorMaker Performance Tuning](https://engineering.salesforce.com/mirrormaker-performance-tuning-63afaed12c21)
    * [Improving Network Utilization of a Connect Task](https://docs.confluent.io/platform/current/multi-dc-deployments/replicator/replicator-tuning.html#improving-network-utilization-of-a-connect-task)
    * [Kafka Mirror Maker Best Practices ](https://community.cloudera.com/t5/Community-Articles/Kafka-Mirror-Maker-Best-Practices/ta-p/249269)
    * [Multi-Tenant, Multi-Cluster and Hierarchical Kafka Messaging Service](https://www.confluent.io/kafka-summit-sf17/multitenant-multicluster-and-hieracrchical-kafka-messaging-service/)
    * [uReplicator: Uber Engineering’s Robust Apache Kafka Replicator](https://eng.uber.com/ureplicator-apache-kafka-replicator/)
    * [Multi-Cluster Deployment Options for Apache Kafka: Pros and Cons](https://www.altoros.com/blog/multi-cluster-deployment-options-for-apache-kafka-pros-and-cons/)
    * [MirrorTool for Kafka Connect (Deprecated)](https://github.com/Comcast/MirrorTool-for-Kafka-Connect)
    * []()
