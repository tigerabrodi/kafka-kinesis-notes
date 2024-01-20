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

# Kafka
