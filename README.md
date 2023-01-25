# ETL-Pipeline-with-Redshift

### Introduction

A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

Our task is to build an ETL pipeline that 
- EXTRACTs their data from S3, stages them in Redshift, and 
- TRANSFORMs data into a set of dimensional tables for their analytics team to continue finding insights into what songs their users are listening to.

![afa](https://video.udacity-data.com/topher/2022/May/62770f73_sparkify-s3-to-redshift-etl/sparkify-s3-to-redshift-etl.png)

### Data Source
<br>**Song Dataset**
<br>The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID.

<br>**Log Dataset**
<br>The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

<br>**Log JSON Meta Information**
<br>This third file contains the meta information that is required by AWS to correctly load `Log Dataset`

### Schema for Song Play Analysis
<br>Using the song and event datasets, a star schema optimized for queries on song play analysis. This includes the following tables.
<br>**Fact Table**<br>
1. **songplays** - records in event data associated with song plays i.e. records with page `NextSong`
- *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

<br>**Dimension Table**<br>
2. **users** - users in the app
- *user_id, first_name, last_name, gender, level*

3. **songs** - songs in music database
- *song_id, title, artist_id, year, duration*

4. **artists** - artists in music database
- *artist_id, name, location, latitude, longitude*

5. **time** - timestamps of records in **songplays** broken down into specific units
- *start_time, hour, day, week, month, year, weekday*

### ETL Pipeline
1. Create an IAM role that has read access to S3.
2. Add redshift database and IAM role info to `dwh.cfg`.
3. Launch a redshift cluster.
4. Run `create_tables.py` to connect to the database and create fact and dimension tables for the star schema in Redshift.
5. Run `etl.py` to load data from S3 into staging tables on Redshift, and then process that data into analytics tables on Redshift.
6. Delete your redshift cluster when finished.

### Example Queries

