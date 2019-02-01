# Hadoop in GCP

Hadoop is an Apache open source framework written in Java that allows distributed processing of large datasets across clusters of computers using simple programming models. Hadoop is designed to scale up from a single machine to thousands of machines.

### Hadoop Architecture

##### MapReduce

* YARN based system for parallel processing of large datasets
* We call MapReduce api to define a map and reduce the task, then output is sent to YARN

##### YARN

* framework for job scheduling and cluster resource management
* Figures out where and how to run this job and stores the result in HDFS

##### HDFS

* Distributed filesystem that provides high-throughput access to application data

##### Common Utilities

* Java libraries and utils

### Hadoop EcoSystem in GCP

For each component of Hadoop, we have equivalent component on cloud platform

| Componenet | GCP Equivalent | Description |
| :--- | :--- | :--- |
| Hive | Big Query | works with HDFS |
| HBase | Big Table | Sparse data |
| PIG & Spark | Data flow | Tool to get unstructured data into the HDFS |
| Kafka or Flink | Pub/Sub | Deals with streaming data |

### Advantages

* Allows users to quickly write and test distributed systems
* Does not rely on hardware to provide fault-tolerance and high-availability \(FTHA\)
* Servers can be added/removed dynamically from the cluster without interrupting Hadoop's operation
* Apart from being open sourced, it supports all platform since it is Java-based

### Deepdown

##### Hive

* mainly deals with structured data, stored in HDFS, with a HQL query \(similar to SQL\)
* Also runs MapReduce program in backend to process data in HDFS
* Helps in Analytics and BI
* Hive or BigQuery should never be used for online transaction processing data

##### HBase

* non-relational database that runs on top of HDFS.
* Created for large tables with billions of rows and millions of columns with fault-tolerant capability and horizontal scalability and based on Google Big Table
* Hadoop can only perform batch processing, and data will be accessed only in a sequential manner. For random access of huge data, HBase is used.

##### PIG

* deals with structured data, just like Hive, using PIG Latin language. Works well with unstructured and incomplete datasets.
* An alternative to programmer who loves scripting and don't want to use Java/Python or SQL to process data
* Pig Latin is made up of series of operations, that are applied to input data, which runs MapReduce program in backend to produce output
* Transforms unstructured data into structured format.
* Pre-installed on Google DataProc machines along with Hive, HBase. Basically DataProc is managed Hadoop services on GCP

##### Spark

* distributed compute engine used along with Hadoop. Sort of a shell to quickly process datasets.
* Both Pig & Spark are used for data transformations using Have rich libraries.

##### HDFS

* supports large datasets.
* Not used for real-time application
* used for batch processing
* Doesn't depend on hardware, hence fault tolerance is high





