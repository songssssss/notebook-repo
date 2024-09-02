https://www.passnexam.com/google/professional-data-engineer/1

Question 5

You are designing a basket abandonment system for an ecommerce company. The system will send a message to a user based on these rules:
• No interaction by the user on the site for 1 hour
• Has added more than $30 worth of products to the basket
• Has not completed a transaction

You use Google Cloud Dataflow to process the data and decide if a message should be sent.

How should you design the pipeline?
Use a fixed-time window with a duration of 60 minutes.
Use a sliding time window with a duration of 60 minutes.
Use a session window with a gap time duration of 60 minutes.
Use a global window with a time based trigger with a delay of 60 minutes.

In data processing and streaming analytics, windowing concepts are crucial for handling and analyzing data in time-bound segments. These windows help in aggregating data over specific time periods and are used in various scenarios depending on the nature of the data and the requirements of the analysis. Here’s a breakdown of the three primary windowing concepts:

### 1. Fixed Window

**Definition:**
- **Fixed Window** (also known as a tumbling window) divides the data stream into non-overlapping, contiguous windows of a fixed duration. Each window is independent of the others.

**Use Case:**
- **Use Case:** Fixed windows are useful when you want to aggregate data over regular, fixed intervals of time, such as hourly or daily reports. For instance, if you need to compute the total number of transactions every hour, you can use fixed windows of one hour each.

**Example:**
- Suppose you have a stream of event timestamps, and you want to count the number of events every hour. Using a fixed window of 1 hour, the events from 00:00 to 01:00 will be aggregated into one window, events from 01:00 to 02:00 into another, and so on.

### 2. Sliding Window

**Definition:**
- **Sliding Window** (also known as a moving window) divides the data stream into overlapping windows that slide over time. Each window has a fixed duration and the window can slide by a smaller time increment, allowing for overlapping windows.

**Use Case:**
- **Use Case:** Sliding windows are suitable for scenarios where you need continuous, real-time analysis and aggregation. For instance, if you want to calculate the moving average of a metric every 5 minutes but with a window that slides every minute, sliding windows are appropriate.

**Example:**
- If you use a sliding window of 10 minutes with a slide interval of 1 minute, you’ll get a new aggregation every minute, but each aggregation will include data from the past 10 minutes. Thus, there will be overlapping windows (e.g., 00:00 to 10:00, 00:01 to 10:01, etc.).

### 3. Session Window

**Definition:**
- **Session Window** is designed to group events into windows based on periods of activity or sessions. It creates windows based on periods of user activity separated by gaps of inactivity. The windows are not fixed in size but rather are based on the activity of the data stream.

**Use Case:**
- **Use Case:** Session windows are useful for handling user session data, where the timing and length of the session can vary. For example, in user activity analysis on a website, a session window can group all the interactions of a user into a session, with inactivity periods separating different sessions.

**Example:**
- If you’re tracking user interactions on a website and define a session timeout of 30 minutes, any sequence of interactions separated by less than 30 minutes will be grouped into the same session window. If a user is inactive for more than 30 minutes, a new session window will begin after the inactivity period.

In summary, the choice of windowing concept depends on the data characteristics and the analysis needs:

- **Fixed Window**: For regular, non-overlapping intervals.
- **Sliding Window**: For continuous, overlapping intervals with frequent updates.
- **Session Window**: For grouping events based on activity and inactivity periods.

---

Question 6

Your company is migrating their 30-node Apache Hadoop cluster to the cloud. They want to re-use Hadoop jobs they have already created and minimize the management of the cluster as much as possible. They also want to be able to persist data beyond the life of the cluster.

What should you do?
Create a Google Cloud Dataflow job to process the data.
Create a Google Cloud Dataproc cluster that uses persistent disks for HDFS.
Create a Hadoop cluster on Google Compute Engine that uses persistent disks.
Create a Cloud Dataproc cluster that uses the Google Cloud Storage connector.
Create a Hadoop cluster on Google Compute Engine that uses Local SSD disks.


Given the requirements of re-using existing Hadoop jobs, minimizing cluster management, and persisting data beyond the life of the cluster, the best option is:

**Create a Cloud Dataproc cluster that uses the Google Cloud Storage connector.**

Here’s why this choice is appropriate:

1. **Re-use Existing Hadoop Jobs**: Cloud Dataproc is fully compatible with Hadoop, Spark, and Hive. This means you can run your existing Hadoop jobs on Dataproc with minimal changes.

2. **Minimize Management**: Cloud Dataproc is a fully managed service, which reduces the complexity of cluster management. Google handles the infrastructure, scaling, and maintenance.

3. **Persist Data Beyond the Life of the Cluster**: Using Google Cloud Storage (GCS) as the storage backend allows you to persist data independently of the lifecycle of the Dataproc cluster. Data stored in GCS will remain available even if the cluster is deleted or recreated.

### Why the Other Options Are Less Suitable:

1. **Google Cloud Dataflow**: Dataflow is a service for stream and batch data processing using Apache Beam, and while it's powerful, it's not designed specifically for running existing Hadoop jobs.

2. **Google Cloud Dataproc with Persistent Disks for HDFS**: While Dataproc with persistent disks is a valid approach for HDFS, using Google Cloud Storage for persistence is generally preferred as it decouples the storage from the compute resources and is more cost-effective.

3. **Hadoop Cluster on Google Compute Engine with Persistent Disks**: This option involves manually managing the Hadoop cluster on Compute Engine instances, which increases management overhead and complexity. Persistent disks are also tied to the lifecycle of the Compute Engine instances.

4. **Hadoop Cluster on Google Compute Engine with Local SSDs**: Local SSDs offer high performance but are ephemeral, meaning the data stored on them is lost when the VM is terminated. This doesn’t meet the requirement to persist data beyond the life of the cluster.

In summary, **creating a Cloud Dataproc cluster that uses the Google Cloud Storage connector** aligns best with your goals of leveraging existing Hadoop jobs, minimizing management, and ensuring data persistence.

---

Question 10

You work for an economic consulting firm that helps companies identify economic trends as they happen. As part of your analysis, you use Google BigQuery to correlate customer data with the average prices of the 100 most common goods sold, including bread, gasoline, milk, and others. The average prices of these goods are updated every 30 minutes. You want to make sure this data stays up to date so you can combine it with other data in BigQuery as cheaply as possible.

What should you do?
Load the data every 30 minutes into a new partitioned table in BigQuery.
Store and update the data in a regional Google Cloud Storage bucket and create a federated data source in BigQuery
Store the data in Google Cloud Datastore. Use Google Cloud Dataflow to query BigQuery and combine the data programmatically with the data stored in Cloud Datastore
Store the data in a file in a regional Google Cloud Storage bucket. Use Cloud Dataflow to query BigQuery and combine the data programmatically with the data stored in Google Cloud Storage.

Store and update the data in a regional Google Cloud Storage bucket and create a federated data source in BigQuery.

Here’s why this approach is optimal:

1. Cost Efficiency
Storage Costs: Google Cloud Storage is typically more cost-effective for storing large volumes of data compared to BigQuery, especially when it involves frequent updates.
BigQuery Federated Queries: By creating a federated data source, you can query the data in Cloud Storage without having to load it into BigQuery directly. This avoids the costs associated with loading and storing large datasets in BigQuery.
2. Data Freshness
Frequent Updates: Storing the data in Cloud Storage allows you to update it every 30 minutes as required. You can automate this process using Cloud Functions or Cloud Scheduler to handle updates.
3. Integration with BigQuery
Federated Queries: BigQuery supports federated queries, which allow you to query data stored in Google Cloud Storage directly. This means you can combine the latest price data with other data stored in BigQuery without the need to physically import the data into BigQuery.
4. Scalability and Performance
Scalability: Google Cloud Storage scales easily and handles large datasets efficiently.
Performance: Federated queries in BigQuery are optimized to work efficiently with data stored in Google Cloud Storage.
Why the Other Options Are Less Suitable:
Load the Data Every 30 Minutes into a New Partitioned Table in BigQuery:

Cost: Regularly loading new tables into BigQuery can become expensive and complex to manage, especially with frequent updates.
Complexity: Managing multiple partitioned tables and handling frequent schema changes can increase operational complexity.
Store the Data in Google Cloud Datastore:

Data Model: Google Cloud Datastore is a NoSQL database and might not be the best choice for handling tabular data that is frequently updated and queried. It also does not natively support federated queries with BigQuery.
Store the Data in a File in Google Cloud Storage and Use Cloud Dataflow to Query BigQuery:

Complexity: Using Cloud Dataflow to combine data from Google Cloud Storage and BigQuery adds unnecessary complexity. Cloud Dataflow is more suitable for ETL and complex data transformations rather than just querying and combining datasets.
Summary
Storing and updating the data in a regional Google Cloud Storage bucket and creating a federated data source in BigQuery strikes the right balance between cost, ease of use, and performance. It allows you to keep your data up to date, leverage BigQuery’s powerful querying capabilities, and minimize costs associated with data storage and frequent updates.

---
Question 11

You are designing the database schema for a machine learning-based food ordering service that will predict what users want to eat. Here is some of the information you need to store:
- The user profile: What the user likes and doesn't like to eat
- The user account information: Name, address, preferred meal times
- The order information: When orders are made, from where, to whom

The database will be used to store all the transactional data of the product. You want to optimize the data schema.

Which Google Cloud Platform product should you use?
BigQuery
Cloud SQL
Cloud Bigtable
Cloud Datastore


Answer is Cloud SQL

The database will be used to store all the transactional data of the product. what we need is the database only for store transactional data, not for analysis and ML. so the answer should be "the database that stores transactional data", which means, Cloud SQL. if you want to analyze or do ML you just specify Cloud SQL as a federated data source.

A: it's good for analysis but it costs too much to input/output data frequently.
C: BigTable is not good for transactional data.
D: okay datastore supports transactions, but it is weaker than RDB, and also, in this case, the data schema has already defined , you should use RDB.

Google Cloud Datastore, now integrated into **Google Cloud Firestore** in Datastore mode, is a fully managed NoSQL document database designed for high-performance, scalable applications. It offers flexible, scalable, and reliable storage for applications that need to handle large amounts of data.

Here’s a detailed overview of Google Datastore (and its current Firestore in Datastore mode):

### Key Features of Google Cloud Datastore / Firestore in Datastore Mode

1. **NoSQL Database:**
   - **Schema-less**: Allows for flexible data modeling without requiring a fixed schema, making it easier to adapt to changes in your application’s data structure.
   - **Document-Oriented**: Stores data as documents in collections, which can be nested.

2. **Scalability:**
   - **Automatic Scaling**: Handles large amounts of data and high request volumes without manual intervention. Google Cloud manages the underlying infrastructure to ensure that the database scales automatically.

3. **High Performance:**
   - **Indexing**: Automatically indexes data to support fast queries without the need for manual index management.
   - **Low Latency**: Designed for high throughput and low-latency access, making it suitable for real-time applications.

4. **ACID Transactions:**
   - **Transaction Support**: Provides support for ACID transactions, allowing multiple operations to be executed atomically and consistently.

5. **Global Distribution:**
   - **Multi-Regional Replication**: Data is automatically replicated across multiple locations to ensure high availability and durability.

6. **Flexible Querying:**
   - **Powerful Queries**: Supports complex queries, including filters, range queries, and sorting. Queries are executed using indexed fields for efficiency.

7. **Integration with Google Cloud Services:**
   - **App Engine Integration**: Seamlessly integrates with Google App Engine for building scalable applications.
   - **BigQuery Integration**: Can be integrated with BigQuery for advanced analytics on your data.

8. **Security:**
   - **IAM Integration**: Uses Google Cloud Identity and Access Management (IAM) to control access to Datastore resources.
   - **Encryption**: Data is encrypted both in transit and at rest.

9. **Cost-Effective:**
   - **Pay-as-You-Go**: Charges based on usage, including the number of read/write operations and storage consumed.

### Use Cases:

- **Web and Mobile Applications**: Ideal for applications that require scalable and flexible data storage, such as user profiles, content management, and session data.
- **Real-Time Analytics**: Suitable for applications that need to process and analyze large volumes of data in real-time.
- **Gaming**: Often used for managing game state and player profiles in real-time multiplayer games.
- **IoT Applications**: Handles data from a large number of devices and sensors efficiently.

### Transition to Firestore:

Google Cloud Datastore has been integrated into **Google Cloud Firestore**. Firestore provides all the features of Datastore with additional enhancements, including:

- **Real-Time Updates**: Supports real-time data synchronization and offline capabilities.
- **Enhanced Query Capabilities**: Offers more powerful querying and data structuring options.
- **Hierarchical Data Model**: Supports a more flexible data model with nested collections.

**Firestore in Datastore Mode** allows users to leverage existing Datastore applications while benefiting from Firestore’s enhancements and infrastructure.

### Summary

Google Cloud Datastore (now Firestore in Datastore mode) is a powerful NoSQL database service designed for scalability, flexibility, and performance. It is ideal for applications that require a schema-less, scalable, and high-performance data storage solution. The transition to Firestore brings additional features and improvements while maintaining compatibility with existing Datastore applications.


---

Question 13

You are choosing a NoSQL database to handle telemetry data submitted from millions of Internet-of-Things (IoT) devices. The volume of data is growing at 100 TB per year, and each data entry has about 100 attributes. The data processing pipeline does not require atomicity, consistency, isolation, and durability (ACID).
However, high availability and low latency are required.
You need to analyze the data by querying against individual fields.

Which three databases meet your requirements? (Choose three.)
Redis
HBase
MySQL
MongoDB
Cassandra
F. HDFS with Hive

Answer is HBase, D. MongoDB, E. Cassandra

A. Redis - Redis is an in-memory non-relational key-value store. Redis is a great choice for implementing a highly available in-memory cache to decrease data access latency, increase throughput, and ease the load off your relational or NoSQL database and application. Since the question does not ask cache, A is discarded.
B. HBase - Meets reqs
C. MySQL - they do not need ACID, so not needed.
D. MongoDB - Meets reqs
E. Cassandra - Apache Cassandra is an open source NoSQL distributed database trusted by thousands of companies for scalability and high availability without compromising performance. Linear scalability and proven fault-tolerance on commodity hardware or cloud infrastructure make it the perfect platform for mission-critical data.
F. HDFS with Hive - Hive allows users to read, write, and manage petabytes of data using SQL. Hive is built on top of Apache Hadoop, which is an open-source framework used to efficiently store and process large datasets. As a result, Hive is closely integrated with Hadoop, and is designed to work quickly on petabytes of data. HIVE IS NOT A DATABSE.


