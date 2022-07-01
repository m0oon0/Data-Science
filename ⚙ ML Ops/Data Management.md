## Data Sources

- Most DL applications require lots of data (Exceptions : RL, GANs, GPT-3)
- Publicly available datasets = No competitive advantage (But can serve as starting point)

- Companies usually spend money&time to collect and label data
- Other ways
  - Data flywheel
  - Semi-supervised learning : Use parts of data to label other parts (e.g. language model, vision)
  - Data augmentation
    - `Image`  
        Must to for training vision models.  
        Frameworks (e.g. torchvision) provide functions to do this. (Done in parallel to GPU training, on the CPU)
    -  `Tabular` Delete some ceels to simulate missing data
    - `Text` No well established techniques, but replace words with synonyms, change order of words, etc
    - `Speech / Video` Change speed, Insert noise, Crop out a portion, Mask frequency..
    
  - Synthetic Data  
    ![image](https://user-images.githubusercontent.com/79262676/176193571-c19e37be-2870-4d3e-b09a-aaa5a3d98ee7.png)


## Data Storage

### Filesystem : Foundational layer of storage  
  Can be networked (e.g. NFS) accessible over network  
  Can be distributed (e.g. HDFS) stored and accessed over multiple machines
  
### Local data format
  - Binary data (image, audio, video) : Just files
  - Large tabular / text data  
    `HDF5` powerful but declining | `Parquet` recommended | `Feather` up-and-coming
    
### Object Storage 
  - (Amazon S3, ceph, Google Cloud)
  - Use as an API over the filesystem. 
  - GET, PUT, DELETE methods without understanding how they are actually handled.
  - Object unit. Usually binary data
  - Not fast as local, but fast enough within the cloud.
  ![image](https://user-images.githubusercontent.com/79262676/176195873-bdb4297b-1c79-4533-929b-7e1606475214.png)

### Database
  - Persistent storage and retrieval of structured data 
  - Online Transaction Processing (OLTP)
  - Everything is actually in RAM (very fast), but SW should ensure that everything is logged to disk and never lost. (consistency guaranteed)
  - Not for binary data (Store references instead ; URL in S3 & actual binary data in S3)

### Data Warehouse
  - Structured aggregation of data for analysis
  - Online Analytical Processing (OLAP)
  - ETL (Extract, Transform, Load)  
   ![image](https://user-images.githubusercontent.com/79262676/176197506-8366c1d4-31ed-435c-815e-0e0e439a4062.png)
  - Most data solutions use SQL (standard interface for structured data)
  - In Python ecosystem, Pandas is the main DataFrame
  - Become fluent in both!
 
### Data Lake
    - Unstructured aggregation of data from multiple sources. 
    - ELT (Dump everything in into this lake, and then transform into specific use later)
 
  ![image](https://user-images.githubusercontent.com/79262676/176198373-727fa9b8-f9db-4769-b218-d9678d9f69fd.png)
  
- Trend : Data Lake
 
 ![image](https://user-images.githubusercontent.com/79262676/176198702-24c43248-e509-461d-9e85-5a8d1e70b3be.png)

- For now,
  - Binary data (image, sound, ) : Stored as objects
  - Metadata (labels, user activity) : In database

## Data Processing

We are training a photo popularity predictor every night.  
For each photo, training data include :  
- Metadata (posting time, title, location) : In database
- Features of the user (log) : Need to compute from logs
- Outputs of photo classifiers (content, style) : Need to run classifiers  

### Considerata
- Task dependencies (programs, databases)
- Over multiple machines
- Many dependency graphs executing all at once

`Hadoop` `Spark`  

`Airflow` Distributing work : The workflow manager has a queue for the tasks, and manages workers that pull from it, restarting jobs if they fail.
![image](https://user-images.githubusercontent.com/79262676/176201322-d69d1531-2fa0-4a25-8d00-2aa5c25de162.png)

`Apache Beam` `Prefect` `dbt`

## Feature Store

Michelangelo : Uber's Machine Learning Platform

![image](https://user-images.githubusercontent.com/79262676/176201893-11414796-0e16-4e31-957f-067c4689b048.png)

- Try to keep things simple : Don't overengineer (UNIX has powerful parallelism, optimization)

## Data Exploration

- `Pandas`
- Scalable & Parallelized Pandas interface `DASK` 
![image](https://user-images.githubusercontent.com/79262676/176203104-44e9d60c-0de3-4b81-979d-f06a7972b57b.png)

- `RAPIDS` Data analytics on GPU

## Data Labeling

![image](https://user-images.githubusercontent.com/79262676/176203655-05f185bb-cef6-4c43-9f4b-f152ba0baca8.png)

### Sources of labor

- Hire : Secure, fast But expensive
- Crowdsource : Cheaper, scalable But quality doubted
- Data labeling company
