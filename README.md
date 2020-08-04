# Data-Lake-with-Apache-Spark-and-AWS
Data Lake project on extracting and loading data in Amazon S3 and processing and transforming data using Apache Spark

##Project Description
A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

In this project, we will build an ETL pipeline for a data lake hosted on S3. We will load data from S3, process the data into analytics tables using Spark, and load them back into S3. We will deploy this Spark process on a cluster using AWS.

##Deployement
File ```dl.cfg``` contains :

```
KEY=YOUR_AWS_ACCESS_KEY
SECRET=YOUR_AWS_SECRET_KEY
```
If you are using local as your development environemnt - then move project directory from local to EMR
```
scp -i <.pem-file> <Local-Path> <username>@<EMR-MasterNode-Endpoint>:~<EMR-path>
```

###OR 

You can also create the files directly in emr cluster using vi editor or any editor of your choice.

```
vi etl.py
```

##How to Run

Create an S3 Bucket named ```sparkify-datalake-***``` where output results will be stored.

Running spark job (Before running job make sure EMR Role have access to s3)
```
usr/log/bin/spark-submit --master yarn ./etl.py
```
Confirm the spark-submit location on your emr using below command:
```
which spark-submit
```

##ETL pipeline
1. Load credentials

2. Read data from S3
```
Song data: s3://udacity-dend/song_data
Log data: s3://udacity-dend/log_data
```
The script reads song_data and load_data from S3.

3. Process data using spark
<br/>Transforms them to create five different tables listed under Dimension Tables and Fact Table. Each table includes the right columns and data types. Duplicates are addressed where appropriate.

4. Load it back to S3
<br/>Writes them to partitioned parquet files in table directories on S3.

Each of the five tables are written to parquet files in a separate analytics directory on S3. Each table has its own folder within the directory. Songs table files are partitioned by year and then artist. Time table files are partitioned by year and month. Songplays table files are partitioned by year and month.

**Note:** ```Data_lake_spark.ipnyb``` notebook is not a part of project. It was created to run all the commands seprately and understand individual output. It access the data from local, processes it and create the output in seperate directory in local.

