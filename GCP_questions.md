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
