<b>Introduction</b>


Sparkify, a music streaming startup, is seeking a data engineer to assist their analysis team in extracting valuable insights from their song and user activity data. At present, the data is stored in a collection of CSV files, making it challenging to query and generate meaningful results. The team is looking for a professional who can develop an Apache Cassandra database capable of handling queries related to song plays. As part of your role, you will be responsible for designing and implementing the database solution. To validate its effectiveness, you will execute queries provided by the Sparkify analytics team, allowing them to obtain the desired results.

Additionally, Sparkify intends to transition its operations and data to the cloud due to their expanding user base and song library. Their data is currently stored in Amazon S3, with one directory containing JSON information about the songs and another directory containing JSON logs detailing user activity. Your objective is to create an Extract, Transform, Load (ETL) pipeline that extracts data from S3, stages it on Amazon Redshift, and transforms it into a series of dimension and fact tables. This pipeline will empower the analytics team to continue uncovering valuable insights regarding the music preferences and behaviors of Sparkify's users.


<b>Project Description</b>

Building an ETL pipeline for a database stored on Redshift using Data Warehouse and AWS In order to develop analytics, you must load data from S3 into staging tables on Redshift and then run SQL statements to create fact and dimension tables from these staging tables.

<b>Project Datasets</b>

Song Data Path     -->     s3://udacity-dend/song_data
Log Data Path      -->     s3://udacity-dend/log_data
Log Data JSON Path -->     s3://udacity-dend/log_json_path.json

<b>Song Dataset</b>

The first dataset is a subset of real data from the Million Song Dataset(https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. 
For example:

song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

<b>Log Dataset</b>

The second dataset consists of log files in JSON format. The log files in the dataset with are partitioned by year and month.
For example:

log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json

And below is an example of what a single log file, 2018-11-13-events.json, looks like.

{"artist":"Pavement", "auth":"Logged In", "firstName":"Sylvie", "gender", "F", "itemInSession":0, "lastName":"Cruz", "length":99.16036, "level":"free", "location":"Klamath Falls, OR", "method":"PUT", "page":"NextSong", "registration":"1.541078e+12", "sessionId":345, "song":"Mercy:The Laundromat", "status":200, "ts":1541990258796, "userAgent":"Mozilla/5.0(Macintosh; Intel Mac OS X 10_9_4...)", "userId":10}

# **Schema for Song Play Analysis**

Using the song and event datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

### **Fact Table**

1. **songplays** - records in event data associated with song plays i.e. records with page `NextSong`
    - *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

### **Dimension Tables**

1. **users** - users in the app
    - *user_id, first_name, last_name, gender, level*
2. **songs** - songs in music database
    - *song_id, title, artist_id, year, duration*
3. **artists** - artists in music database
    - *artist_id, name, location, lattitude, longitude*
4. **time** - timestamps of records in **songplays** broken down into specific units
    - *start_time, hour, day, week, month, year, weekday*

# **Project Template**


The project template includes four files:

- `create_table.py` is where you'll create your fact and dimension tables for the star schema in Redshift.
- `etl.py` is where you'll load data from S3 into staging tables on Redshift and then process that data into your analytics tables on Redshift.
- `sql_queries.py` is where you'll define you SQL statements, which will be imported into the two other files above.
- `README.md` is where you'll provide discussion on your process and decisions for this ETL pipeline.


# **Project Steps**

Below are steps you can follow to complete each component of this project.

### **Create Table Schemas**

1. Design schemas for your fact and dimension tables
2. Write a SQL `CREATE` statement for each of these tables in `sql_queries.py`
3. Complete the logic in `create_tables.py` to connect to the database and create these tables
4. Write SQL `DROP` statements to drop tables in the beginning of `create_tables.py` if the tables already exist. This way, you can run `create_tables.py` whenever you want to reset your database and test your ETL pipeline.
5. Launch a redshift cluster and create an IAM role that has read access to S3.
6. Add redshift database and IAM role info to `dwh.cfg`.
7. Test by running `create_tables.py` and checking the table schemas in your redshift database. You can use Query Editor in the AWS Redshift console for this.

### **Build ETL Pipeline**

1. Implement the logic in `etl.py` to load data from S3 to staging tables on Redshift.
2. Implement the logic in `etl.py` to load data from staging tables to analytics tables on Redshift.
3. Test by running `etl.py` after running `create_tables.py` and running the analytic queries on your Redshift database to compare your results with the expected results.
4. Delete your redshift cluster when finished.# data-warehouse-with-amazon-redshift
