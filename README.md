# Notes for Data Engineering on Google Cloud Platform(v1.1)

> This four-day instructor-led class provides participants a hands-on introduction to 
> designing and building data processing systems on Google Cloud Platform.

> Through a combination of presentations, demos, and hand-on labs, participants will learn 
> how to design data processing systems, build end-to-end data pipelines, analyze data and carry out machine learning.

> The course covers structured, unstructured, and streaming data.

## Day 1: Leveraging Unstructured Data

### Module 1: Introduction to Cloud Dataproc

- Cloud Dataproc automation helps you create clusters quickly, manage them easily, and save money by turning clusters off when you don't need them.

- Unstructured data accounts for 90% of enterprise data. It's hard to analyzed.
  - Even with Google, e.g. Google has lots of street view data. It contatins bunch of valuable information.
  
- MapReduce split big data so each compute node process data local to it.
  - Operating and adminitraing takes a lot of times.
  - Dataproc ease Hadoop management.
  - Scaling takes less than 5 mins.
  
- Dataproc
  - Zone is important. Match your data location with your compute location.
  - Data in Google Cloud Storage (GCS) is replicated across zones. So you can pick any zone within the region where your data
resides.
  - But cross region cause performace issue.
  - Standard/HA Mode for master node.
  - For worker node, disk performance scale with size.
  - Don't store input/output data in HDFS. 
    - You want to delete your cluster after your job done.
  - Preemptible workers can be a good deal.
    - 50% cost reduction.
    - Best practice is 50%/50% of on-demand and preemptible-vm
  - Create Dataproc via scripts/console/REST API. E.g.
  ```shell
  gcloud dataproc clusters create my-second-cluster --zone us-central1-a \
  --master-machine-type n1-standard-1 --master-boot-disk-size 50 \
  --num-workers 2 --worker-machine-type n1-standard-1 \
  --worker-boot-disk-size 50
  ```
  


### Module 2: Running Dataproc jobs

### Module 3: Leveraging GCP

### Module 4: Analyzing unstructured data

### Module 5: BigQuery

## Day 2: Serveerless data analysis

## Day 3: Serverless Machine Learning

## Day 4: Streaming Data Processing

# Reference
- [Data Engineering on Google Cloud Platform](https://cloud.google.com/training/courses/data-engineering)
- [Data Engineering on Google Cloud Platform in Taipei](https://events.withgoogle.com/data-engin-422792/class-outline/#content)
- [Labs Code on Github](https://github.com/GoogleCloudPlatform/training-data-analyst)
- [20180306_DEonGCP_Taipei Documents/Questions/Refs](https://goo.gl/s7uR8Y)
- [Dataproc initialization scripts](https://github.com/GoogleCloudPlatform/dataproc-initialization-actions)
