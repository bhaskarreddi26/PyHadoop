Apache Kafka

Apache Kafka is a real time, fault tolerant, scalable messaging system for moving data in real time. It's a good candidate for use cases like capturing user activity on websites, logs, stock ticker data, and instrumentation data.

Kafka works like a distributed database and is based on a partitioned and replicated low latency commit log. When we post a message to Kafka, it's replicated to different servers in the cluster and at the same time it’s also committed to disk.

**[Apache Kafka](http://kafka.apache.org/documentation.html)**includes client API as well as a data transfer framework called Kafka Connect.

**[Kafka Clients](http://kafka.apache.org/documentation.html#api):** Kafka includes Java clients (for both message producers and consumers). We will use the Java producer client API in our sample application.

**[Kafka Connect:](http://kafka.apache.org/documentation.html#connect) **Kafka also includes Kafka Connect, which is a framework for streaming data between Apache Kafka and external data systems to support the data pipelines in organizations. It includes import and export connectors to move data sets into and out of Kafka. Kafka Connect program can run as a standalone process or as a distributed service and supports REST interface to submit the connectors to Kafka Connect cluster using a REST API.


**How to install**


https://devops.profitbricks.com/tutorials/install-and-configure-apache-kafka-on-ubuntu-1604-1/

https://kafka.apache.org/quickstart