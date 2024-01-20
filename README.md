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
