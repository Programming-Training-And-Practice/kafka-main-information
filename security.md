# Apache Kafka Security



## The need for encryption, authentication & authorization in Kafka
* Currently, any client can access your Kafka cluster (authentication)
* The clients can publish/consume any topic data (authorization)
* All the data being sent is fully visible on the network (encryption)

* Someone could intercept data being sent
* Someone could publish bad data/setal data
* Someone could delete topics

* All these reasons push for more security and an authentication model


## Encryption in Kafka
* Encryption in Kafka ensures that the data exchanged between clients and brokers is secret to routers on the way
* This is similar concept to an https website



## Authentication in Kafka
* Authentication in Kafka ensures that only clients that can prove their identity can connect to our Kafka Cluster
* This is similar concept to a login (username/password)
* Authentication in Kafka can take a few forms:
  * SSL Authentication: clients authenticate to Kafka using SSL certificates
  * SASL Authentication:
    * PLAIN: clients authenticate using username/password (weak - easy to setup)
    * Kerberos: such as Microsoft Active Directory (strong - hard to set)
    * SCRAM: username/password (strong- medium to setup)


## Authorisation in Kafka
* Once a client is authenticated, Kafka can verify its identity.
* It still needs to be combined with authorisation, so that Kafka knows that:
  * user alice can view topic finance
  * user bob cannot view topic trucks
* ACL(Access Control List) have to be maintained by administration and onboard new users.
