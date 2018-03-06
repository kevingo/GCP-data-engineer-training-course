# Notes for Data Engineering on Google Cloud Platform(v1.1)

> This four-day instructor-led class provides participants a hands-on introduction to
> designing and building data processing systems on Google Cloud Platform.

> Through a combination of presentations, demos, and hand-on labs, participants will learn how to design data processing systems, build end-to-end data pipelines, analyze data and carry out machine learning.

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
  - Delete clusters after your job finished.
  ```shell
  gcloud dataproc clusters delete my-second-cluster
  ```

- Labs
  - Execute PySpark in master node.
    - SSH to your master node and type pyspark command to open PySpark shell
    ```python
      data = [0, 1, 2, 3, 4, 5]  # range(6)
      distData = sc.parallelize(data)
      squares = distData.map(lambda x : x*x)
      res = squares.reduce(lambda a, b : a + b)
      print res
    ```
    ```python
    import numpy as np
    data = range(1000)
    distData = sc.parallelize(data)
    terms = distData.map(lambda k : 8.0/((2*k+1)*(2*k+1)))
    res = np.sqrt(terms.sum())
    print res
    ```
  - Submitting PySpark Jobs without copying anything (code or data) to the cluster
    - Input
    ```
    Dog,Noir
    Dog,Bree
    Dog,Pickles
    Dog,Sparky
    Cat,Tom
    Cat,Alley
    Cat,Cleo
    Frog,Kermit
    Pig,Bacon
    Pig,Babe
    Dog,Gigi
    Cat,George
    Frog,Hoppy
    Pig,Tasty
    Dog,Fred
    Cat,Suzy
    ```
    - Code
    ```python
    #!/usr/bin/env python

    from pyspark import SparkContext
    sc = SparkContext("local")

    file = sc.textFile("gs://<YOUR-BUCKET-NAME>/unstructured/lab2-input.txt")
    dataLines = file.map(lambda s: s.split(",")).map(lambda x : (x[0], [x[1]]))
    print dataLines.take(100) # output: [(u'Dog', [u'Noir']), (u'Dog', [u'Bree']), (u'Dog', [u'Pickles']), (u'Dog', [u'Sparky']), (u'Cat', [u'Tom']), (u'Cat', [u'Alley']), (u'Cat', [u'Cleo']), (u'Frog', [u'Kermit']), (u'Pig', [u'Bacon']), (u'Pig', [u'Babe']), (u'Dog', [u'Gigi']), (u'Cat', [u'George']), (u'Frog', [u'Hoppy']), (u'Pig', [u'Tasty']), (u'Dog', [u'Fred']), (u'Cat', [u'Suzy'])]


    databyKey = dataLines.reduceByKey(lambda a, b: a + b)
    print databyKey.take(100) # output: [(u'Cat', [u'Tom', u'Alley', u'Cleo', u'George', u'Suzy']), (u'Dog', [u'Noir', u'Bree', u'Pickles', u'Sparky', u'Gigi', u'Fred']), (u'Frog', [u'Kermit', u'Hoppy']), (u'Pig', [u'Bacon', u'Babe', u'Tasty'])]


    countByKey = databyKey.map(lambda (k,v): (k, len(v)))
    print countByKey.take(100) # output: [(u'Cat', 5), (u'Dog', 6), (u'Frog', 2), (u'Pig', 3)]
    ```
    - Run job using CLI
    ```shell
    gcloud dataproc jobs submit pyspark \
    --cluster my-cluster gs://<YOUR-BUCKET-NAME>/unstructured/lab2.py
    ```

### Module 2: Running Dataproc jobs

- All the serverless services are stateless.
- Separation of Storage and Compute is what
enables Serverless to work.
  - Compute: Cloud Dataflow、BigQuery Analytics、Cloud Dataproc
  - Storage: Cloud Storage (File)、BigQuery Storage (Tables)、Cloud BigTable (NoSQL)
- Only change `hdfs://` to `gs://`

### Module 3: Leveraging GCP

- Use Dataproc to run OSS on GCP
- But about OSS that’s not already installed?
  - Install software on Dataproc cluster
    - To install software on Dataproc cluster
    - Upload it to Cloud Storage
    - Specify GCS location in Dataproc creation command
    - E.g.
    ```shell
    #!/bin/bash
    apt-get update || true
    apt-get install -y python-numpy python-scipy python-matplotlib python-pandas
    ```
    - Notes: The script is run as root, there is no need to use "sudo"
    - Can only install software on master or worker node
    ```shell
    #!/bin/bash
    apt-get update || true
    ROLE=$(/usr/share/google/get_metadata_value attributes/dataproc-role)
    if [[ "${ROLE}" == 'Master' ]]; then
      apt-get install -y vim
    else
      # something that goes only on worker
    Fi
    # things that go on both
    apt-get install -y python-numpy python-scipy python-matplotlib python-pandas
    ```
    - Specify GCS location when creating cluster
    ```shell
    gcloud dataproc clusters create mycluster \
    --initialization-actions gs://mybucket/init-actions/my_init.sh \
    --initialization-action-timeout 3m
    ```


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
