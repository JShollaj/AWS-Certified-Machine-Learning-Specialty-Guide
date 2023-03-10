# AWS Certified Machine Learning Specialty Course MLS C01

## Data Engineering: Moving, Storing and Processing data in AWS

### Amazon S3

#### **Overview**

- Simple Storage Service (S3)
- Store objects (files) in buckets (directories).
- Buckets must have a globally unique name.
- Max object size is 5TB.

- Durability and Availability:

  - Durability of: **11 x 9s** &rarr; If we have 10 million objects, lose 1 every 10,000 years.

  - Availability of: **4 x 9s** &rarr; Not available ~53 minutes in a year.

#### **S3 For ML**

- We can create **Data Lakes** with S3 as the storage.

  - Fully managed & 11 x 9s Durability
  - Storage is decoupled from Computing resources.

- Object storage supports any file format.
  
  - Best files formats for performance are Avro & Parquet.

- We can perform data partitioning to optimize performance.

  - By Date (Hourly, Daily, Monthly).
  - By Product (ID, Family).
  - Query Patterns

#### **S3 Storage Classes**

- Amazon S3 **Standard - General Purpose**

  - Used for frequently accessed data
  - Sustain 2 concurrent facility failures.
  - Low latency & High throughput.
  - Used for Big Data Analytics, Mobile & Gaming etc.

- Amazon S3 **Standard - Infrequent Access (IA)**

  - Less frequent, but required rapid access.
  - Lower cost than S3.
  - Lower Availability (99.9%).
  - Used for Disaster Recovery, Backups etc.

- Amazon S3 One Zone - Infrequent Access

  - High durability (11x9s), but only in single AZ.
  - Lower cost than S3 Standard IA.
  - Storing secondary data.

- Amazon S3 Glacier - Instant Retrieval

  - Lowest cost (meant for deep archives).
  - Millisecond retrieval, objects but needs to be stored for at least 90 days.

- Amazon S3 Glacier - Flexible Retrieval

  - Minimum storage duration (90 days).
  - Different types of retrievals:
    - Expedited (1-5 minutes)
    - Standard (3-5 hours)
    - Bulk (5-12 hours) - Free tier

- Amazon S3 Glacier - Deep Archive

  - Cheapest ($1 per TB)
  - Longest term storage.
  - Minimum storage duration (180 days).
  - For regulatory and compliance cases.
  - Data retrieval options:
    - Standard (12 hours)
    - Bulk (48 hours)

- Amazon S3 Intelligent Tiering

  - Shifts data through different storages.
  - Has 5 different access tiers, based on frequency:
  
    - **Frequent Access** tier (within 30 days)
    - **Infrequent Access** tier (> 30 days, but still low latency & high throughput)
    - **Archive Instant Access** tier (> 90 days, but still low latency & high throughput)
    - **Archive Access** tier (> 90 days; we choose async access, to save costs; 3-5 hours to access)
    - **Deep Archive Access** tier (> 180 days, 12 hours to access)

- We can also configure lifecycle rules based on:

  - Start with S3 Storage Analysis to create rules.
  - Transition to storage class.
  - Costs.
  - Object based.
  - Expiration/Deletion based on inactivity.

#### **S3 Security**
  
- S3 Encryption for Objects (4 Types)

  - **SSE-S3**: encrypts S3 objects using keys handled & managed by AWS.

  - **SSE-KMS**: use AWS Key Management Service to manage encryption keys (audit trail & increased security).

  - **SSE-C**: client manages encryption keys.

  - **Client-Side**

- S3 Security Layers

  - User Based (IAM Policies)
  - Resource Based (Object & Bucket policies)
  - JSON Based (Objects/Buckets, Actions, Effect, Principal)
  - Networking (Allowing traffic within configured VPC)

---

### Amazon Kinesis

#### **Kinesis Overview**

- Real-time processing service for big data.
- Composed of 4 main sub-groups:
  
  - Kinesis Streams (Ingesting in Real Time)

    - Ingests data in divided shards.
      - Provisioned Mode: We choose between 1MBs/s or 2MBs/s.
      - On-Demand Mode: 4MBs/s - we pay for stream/hr & data instead of shards.
    - Limits:
      - 1MB/s or 1000 messages/s at write per shard (Producer)
      - 2MB/s at read PER SHARD across all consumers
      - 5 API calls per second PER SHARD across all consumers
      - Data retention (24hrs - 365days)

  - Kinesis Analytics (Analytics in Real-Time)
    - Serverless responsive analytics in real time.
    - Continuous metric generation (f.ex live leaderboard).
    - Can be configured through IAM for permissions.
    - Lambda can be used for preprocessing.
  - Kinesis Firehose (Storing in Real-Time
    - Automatic scaling & fully managed data storing for  *near* real time.
    - Supports data conversion, transformantion & compression.
  - Kinesis Video Streams (Video Streaming)
    - Keeps data for 1hr - 10years.
    - Used for security cameras, RADAR etc.

---

### Amazon Glue (Batch)

- **Glue Data Catalog**

  - Automated and versioned schema inference (useful for DB).
  - Glue Crawlers to built the catalog on schedule or demand.
    - They need IAM role to access data stores.
    - Works with JSON, Parquet, CSV & S3, Redshift, RDS.
    - Extracts partitions on how data is organized in S3.

- **Glue ETL**

  - Serverless ETL Tool, used for batch transformations.
    - Bundled Transformations (Drop/Filter/Join/Map).
    - ML Transformations (Matching Records).
    - Apache Spark Transformations.
    - Format transformations (CSV, JSON, Avro, Parquet, ORC, XML).

---

### Stores for ML

- **Redshift**

  - Data Warehousing; OLAP (S3 &rarr; Redshift).
  - Can query data in S3 through Redshift Spectrum.

- **RDS, Aurora**

  - Relational Store, SQL (OLTP Online Transaction Processing)
  - Must provision servers in advance.

- **DynamoDB**

  - NoSQL data store, serverless, provision, read/write capacity.

- **S3**

  - Object storage, Serverless, infinite storage

- **OpenSearch**

  - Indexing of data
  - Search amongst data points
  - Clickstream Analytics

- **ElastiCache**

  - Caching mechanism
  - Not really used for Machine Learning

---

### AWS Data Pipelines Features

- **AWS Data Pipeline**

  - Orchestration service (controls environment, EC2, Code).
  - Destinations such as S3, RDS, DynamoDB, EMR, Redshift.
  - Notifies on failure, and is highly available.

- **AWS Batch**

  - Run batch jobs as Docker images & Dynamic Provisioning.
  - Can be integrated to schedule jobs with CloudWatch/StepFunctions


