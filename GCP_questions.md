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
