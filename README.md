# Data Ingestion

Data ingestion is the process of obtaining and importing data for immediate use or storage in a database. It involves taking data from various sources and moving it to a place where it can be stored and analyzed, such as a data warehouse.

There are two main types of data ingestion:

**Batch Ingestion:** This method involves collecting and importing data in discrete chunks at scheduled times. For example, a company might collect all of its sales data at the end of each day.

**Stream Ingestion:** This method is about continuously collecting and importing data as soon as it becomes available. This is often used for real-time data processing needs, such as monitoring website traffic or financial transactions.

# AWS Services for data engineering

## Data Ingestion

We want to ingest data from different sources into our data lake.

### Batch Ingestion

- Doesn't need much compute and takes less than an hour to process? We can go with AWS Lambda.
- Need more compute? We can go with AWS Glue.
- Amazon EMR is also an option, it let's you run Open Source frameworks like Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto.

### Stream Ingestion

- Amazon Kinesis: Data Streams, Data Firehose & Data Analytics

## Where to store data?

Raw ingested data will go into the data lake.

Data is not ready for analysis yet.

S3 is a good option for data lake. We'll have a raw zone.

After processing out data, it can go into a processed zone in S3.

## Data Catalog

Data Catalog is a central repository to store structural and operational metadata for data lake analytics.

We can use the Glue crawler to automatically discover the schema of our data and store it in the Data Catalog.

## Data warehouse

If we have a lot of data, we can use a data warehouse to store it.

On AWS, we can use Amazon Redshift. Redshift is a columnar data warehouse aka OLAP (Online Analytical Processing). It's different from OLTP (Online Transaction Processing) which is row based. Column based databases are better for analytics, because we can query only the columns we need for our analysis.

## Data Analytics

We can use Amazon Athena to query data in S3. It's serverless and we only pay for the queries we run. Good for ad-hoc queries.

If you need dashboards, we can use Amazon QuickSight.

## Monitoring

Amazon CloudWatch is a monitoring service for AWS cloud resources and the applications you run on AWS. You can use Amazon CloudWatch to collect and track metrics, collect and monitor log files, set alarms, and automatically react to changes in your AWS resources.

# Why need Apache Kafka?

## Scenario

Imagine you have a startup with a popular app that allows users to share messages and media. Initially, your user base is small, so you manage the incoming data (messages, likes, uploads) easily. Your simple system reads data and processes it in real-time, handling tasks like updating user feeds, sending notifications, and storing messages.

## Problem with Scaling

As your app becomes more popular, the volume of data grows exponentially. You realize you need a better way to handle this data. So, you introduce a single queue system. Think of this queue as a line at a coffee shop, where orders are taken and processed one by one. It helps organize the flow of data and ensures that every piece of data is processed in order.

However, as your app continues to grow, even this system starts to falter. The queue gets too long, causing delays. Also, different types of data (like messages, notifications, and uploads) all use the same queue, which isn't efficient. Processing heavy uploads slows down sending quick notifications, for example.

## Apache Kafka to the Rescue

This is where Apache Kafka comes in. Kafka is like upgrading from a single coffee shop line to a large, efficient cafeteria with multiple specialized lines and stations, each handling different types of orders simultaneously and efficiently.

Kafka allows you to set up a distributed streaming platform. What does this mean?

1. **Distributed**: Kafka runs on a cluster of servers, which means it can handle a lot more data and many more operations than a single server or queue.

2. **Streaming**: It can handle continuous flow of data in real-time, perfect for live updates and instant reactions in your app.

3. **Multiple Producers and Consumers**: Imagine many users (producers) sending data to Kafka, like messages or likes. Kafka sorts and stores this data. Then, various parts of your system (consumers), like the notification system or the message storage system, retrieve and process this data as needed. This is much more efficient than the single queue system.

4. **Fault Tolerant**: If one server in the Kafka cluster fails, the others take over, ensuring your data processing doesn't stop.

5. **Scalable**: As your startup grows, you can add more servers to the Kafka cluster to handle even more data.

## General Requirements for Apache Kafka

Kafka is ideal for scenarios where you have high-volume, high-velocity data that needs to be processed in real-time and distributed across different systems. It's great for applications that require real-time analytics, monitoring, and handling streaming data from multiple sources.

# Queue Architecture

In a queue architecture, messages are published once and consumed once. Messages are stored in the queue until they are processed and deleted. It follows the point-to-point messaging pattern.

**Use Cases:** Task distribution, load leveling, and for ensuring that each message is processed by only one consumer.

**Limitations:** Limited support for multiple consumers and cannot guarantee that a message is delivered to all subscribers.

Common tech:

- RabbitMQ
- Apache ActiveMQ
- Amazon SQS

# Pub Sub Architecture

In a pub/sub architecture, messages are published once and consumed by multiple subscribers. Publishers send messages to a topic, and subscribers receive messages from topics they are interested in. It follows the publish-subscribe messaging pattern.

**Use Cases:** Broadcasting messages to multiple recipients, event-driven architectures, and decoupled communication between components.

**Limitations:** Cannot guarantee delivery of messages to all subscriber types, and a publisher could assume that a subscriber is listening to a channel when they are not.

Common tech:

- Google Cloud Pub/Sub
- Redis
- Apache Kafka

# Kafka Architecture

Kafka is a distributed streaming platform where messages are published once and can be consumed by one or more consumers. It is designed for high-throughput, fault-tolerant, and real-time data processing.

**Use Cases:** Log aggregation, stream processing, event sourcing, and real-time monitoring and analytics.

Requires careful setup and monitoring, may be overkill for simple use cases, and can be complex to manage.

Companies:

- LinkedIn
- Uber
- Confluent

# Kafka Components

## Producers

- **Detailed Explanation:** Producers are applications or services that create and send messages to Kafka. Imagine a news reporter (producer) who gathers news and sends it to the news channel (Kafka).
- **Role in Kafka:** They push data (in the form of messages or records) to Kafka topics. A record in Kafka is a basic unit of data, similar to a row in a database table. It contains key-value pairs and is stored in topics.
- **Impact of Absence:** Without producers, there would be no source of data for Kafka. It's like having a postal system (Kafka) with no one sending letters (data).

## Topics

- **Detailed Explanation:** Think of a topic as a specific category or channel in a TV network. Just as different channels have different content, each topic in Kafka is a distinct category of messages. For instance, one topic might be 'UserSignUps' and another 'UserActivity.'
- **Role in Kafka:** Topics categorize data, allowing consumers to subscribe to specific types of messages they are interested in. It's like subscribing to a particular TV channel to watch specific shows.
- **Impact of Absence:** Without topics, Kafka would lose its organizational structure, leading to a jumble of messages with no easy way to filter or manage them, like a TV with all shows playing on one channel.

## Brokers

- **Detailed Explanation:** Brokers are the servers in the Kafka cluster. Think of them as librarians in a library. Each librarian (broker) manages certain books (data).
- **Role in Kafka:** They store the data and handle requests from producers to store messages and requests from consumers to retrieve them. Each broker can store multiple topics.
- **Impact of Absence:** Without brokers, Kafka would have nowhere to store or manage the data, much like a library without librarians.

## Partitions

- **Detailed Explanation:** A partition is a segment of a topic, like chapters in a book. If 'UserActivity' is a book (topic), then each partition could be a chapter focusing on a specific type of activity.
- **Role in Kafka:** They enable Kafka to split the data of a topic across different brokers. This allows for parallel processing as different consumers can read different partitions simultaneously.
- **Impact of Absence:** Without partitions, parallel processing would be impossible, resulting in a significant bottleneck. It's like having a book where only one person can read one chapter at a time.

## Consumer Groups

- **Detailed Explanation:** Consumer groups are like teams working together to process information. Each member of the team (consumer) focuses on a part of the task (partitions of a topic).
- **Role in Kafka:** They allow multiple consumers to work together, processing data in parallel. Each consumer in the group reads from a unique partition, ensuring efficient processing and no overlap.
- **Impact of Absence:** Without consumer groups, individual consumers would either have to process all data (leading to inefficiency) or risk missing data, like a team where everyone does the same job or misses out on tasks.

## Zookeeper

- **Detailed Explanation:** Zookeeper acts as the coordinator in the Kafka system. Think of it as a manager in an office ensuring everyone knows their tasks and coordinates their efforts.
- **Role in Kafka:** It manages the brokers (keeping track of them), helps in leader election for partitions, and maintains configuration information.
- **Impact of Absence:** Without Zookeeper, Kafka would struggle with broker coordination, partition leadership, and configuration management, leading to chaos and inefficiency, like an office without a manager.

## Replicas

- **Detailed Explanation:** Replicas are duplicate copies of partitions stored on different brokers. It's like having backup copies of important documents.
- **Role in Kafka:** They provide data redundancy, ensuring that if one broker fails, another can serve the data, maintaining the system's reliability.
- **Impact of Absence:** Without replicas, any broker failure could lead to data loss and service interruption, similar to losing a sole copy of a critical document.
