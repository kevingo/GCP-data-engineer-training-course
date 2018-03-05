# Notes for the data engineering training on Google Cloud Platform

> This four-day instructor-led class provides participants a hands-on introduction to 
> designing and building data processing systems on Google Cloud Platform.

> Through a combination of presentations, demos, and hand-on labs, participants will learn 
> how to design data processing systems, build end-to-end data pipelines, analyze data and carry out machine learning.

> The course covers structured, unstructured, and streaming data.

## Day 1: Serverless Data Analysis

### Module 1: Serverless data analysis with BigQuery
- What is BigQuery.

- Advanced Capabilities.

- Performance and pricing.

- Lab: Queries and Functions.

- Lab: Load and Export data.

### Module 2: Serverless, autoscaling data pipelines with Dataflow
- Introduction to Dataflow and capabilities.

- Lab: Data pipeline.

- Lab: MapReduce in Dataflow.

- Lab: Side inputs.

- Lab: Streaming.

## Day 2: Serverless Machine Learning

### Module 3: Getting started with Machine Learning
- What is machine learning (ML).

- Effective ML: concepts, types.

- Evaluating ML.

- ML datasets: generalization.

- Lab: Explore and create ML datasets.

### Module 4: Building ML models with Tensorflow
- Getting started with TensorFlow.

- Lab: Using tf.learn.

- TensorFlow graphs and loops + lab.

- Lab: Using low-level TensorFlow + early stopping.

- Monitoring ML training.

- Lab: Charts and graphs of TensorFlow training.

### Module 5: Scaling ML models with CloudML
- Why Cloud ML?.

- Packaging up a TensorFlow model.

- End-to-end training.

- Lab: Run a ML model locally and on cloud.

### Module 6: Feature Engineering

- Creating good features.

- Transforming inputs.

- Synthetic features.

- Preprocessing with Cloud ML.

- Lab: Feature engineering.

### Module 7: ML architectures

- Wide and deep.

- Image analysis.

- Lab: Custom image classification with transfer learning.

- Embeddings and sequences.

- Recommendation systems.

## Day 3: Leveraging unstructured data
### Module 8: Google Cloud Dataproc Overview
- Introducing Google Cloud Dataproc.

- Creating and managing clusters.

- Defining master and worker nodes.

- Leveraging custom machine types and preemptible worker nodes.

- Creating clusters with the Web Console.

- Scripting clusters with the CLI.

- Using the Dataproc REST API.

- Dataproc pricing.

- Scaling and deleting Clusters.

- Lab: Creating Hadoop Clusters with Google Cloud Dataproc.

### Module 9: Running Dataproc Jobs
- Controlling application versions.

- Submitting jobs.

- Accessing HDFS and GCS.

- Hadoop.

- Spark and PySpark.

- Pig and Hive.

- Logging and monitoring jobs.

- Accessing onto master and worker nodes with SSH.

- Working with PySpark REPL (command-line interpreter).

- Lab: Running Hadoop and Spark Jobs with Dataproc.

### Module 10: Integrating Dataproc with Google Cloud Platform
- Initialization actions.

- Programming Jupyter/Datalab notebooks.

- Accessing Google Cloud Storage.

- Leveraging relational data with Google Cloud SQL.

- Reading and writing streaming Data with Google BigTable.

- Querying Data from Google BigQuery.

- Making Google API Calls from notebooks.

- Lab: Big Data Analysis with Dataproc.

### Module 11: Making Sense of Unstructured Data with Google's Machine Learning APIs
- Google's Machine Learning APIs.

- Common ML Use Cases.

- Vision API.

- Natural Language API.

- Translate.

- Speech API.

- Lab: Adding Machine Learning Capabilities to Big Data Analysis.

## Day 4: Resilient streaming systems
### Module 12: Need for real-time streaming analytics
- What is Streaming Analytics?

- Use-cases.

- Batch vs Streaming (Real-time).

- Related terminologies.

- GCP products that help build for high availability, resiliency, high-throughput, real-time streaming analytics (review of Pub/Sub and Dataflow).

- Lab: Setup project, enable APIs, setup storage.

### Module 13: Architecture of streaming pipelines
- Streaming architectures and considerations.

- Choosing the right components.

- Lab: Explore the dataset.

- Windowing.

- Streaming aggregation.

- Events, triggers.

- Lab: Create architecture reference.

### Module 14: Stream data and events into PubSub
- Topics and Subscriptions.

- Publishing events into Pub/Sub.

- Lab: Streaming data ingest into PubSub.

- Subscribing options: Push vs Pull.

- Alerts.

### Module 15: Build a stream processing pipeline
- Pipelines, PCollections and Transforms.

- Windows, Events, and Triggers.

- Aggregation statistics.

- Streaming analytics with BigQuery.

- Low-volume alerts.

- Lab: alerting scenario for anomalies.

### Module 16: High throughput and low-latency with Bigtable
- Latency considerations.

- Lab: create streaming data processing pipelines with Dataflow.

- What is Bigtable.

- Designing row keys.

- Performance considerations.

- Lab: high-volume event processing.

### Module 17: Building Dashboards
- What is Google Data Studio.

- From data to decisions.

- Lab: build a real-time dashboard to visualize processed data.

# Reference
- [Data Engineering on Google Cloud Platform](https://cloud.google.com/training/courses/data-engineering)
- [Data Engineering on Google Cloud Platform in Taipei](https://events.withgoogle.com/data-engin-422792/class-outline/#content)
