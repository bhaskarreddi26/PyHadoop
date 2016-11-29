**Spark SQL**

**Spark Sql Exposes 3 processing interfaces:**
 *  SQL
 *   HiveQL 
 *   Language integrated queries 

Can be used in 2 modes as a library data processing tasks are expressed as SQL, HiveQL or integrated queries in a Scala app

**3 key abstractions**
* SQLContext
* HiveContext
* DataFrame
as a distributed SQL execution engine allows multiple users to share a single spark cluster allows centralized caching across all jobs and across multiple data stores

DataFrame represents a distributed collection of rows organized into named columns Executing SQL queries provides us a DataFrame as the result is schema aware i.e knows names and types of columns provides methods for processing data
can be easily converted to regular RDD can be registered as a temporary table to run SQL/HiveQL 2 ways to create a DF
from existing RDD toDF if we can infer schema using a case class createDataFrame is you want to pass the Schema explicitly (StructType, StructField) from external DataSources single unified interace to create DF, either from data stores (MySQL, PostgresSQL, Oracle, Cassandra) or from files (JSON, Parquet, ORC, CSV, HDFS, local, S3) built-in support for JSON, Parquet, ORC, JDBC, Hive uses DataFrameReader to read data from external datasources can specify partiotioning, format and data source specific options SQL/HiveContext has a factory method called read() that returns an instance of dataFrameReader uses DataFrameWriter to write data to external datasources can specify partiotioning, format and data source specific options build-in functions optimized for faster execution through code generation

    import org.apache.spark.sql.functions._

* Optimization techniques used 
* Reduced Disk IO
* Skip rows

if a data store (for e.g. Parquet, ORC) maintains statistical info about data (min, max of a particular column in a group) then SparkSQL can take advantage of it to skip these groups
* Skip columns (Use support of Parquet)
* skip non-required partitions

Predicate Push down i.e. pushing filtering predicates to run natively on data stores like Cassandra, DB etc.
* In-memory columnar caching
* cache only required columns from any data store
* compress the cached columns (using snappy) to minimize memory usage and GC

SparkSQL can automatically select a compression codec for a column based on data type columnar format enables using of efficient compression techniques run length encoding
* delta encoding
* dictionary encoding
* Query optimization
uses both cost-based (in the physical planning phase) and rule-based (in the logical optimization phase) optimization
can even optimize across functions code generation


* [https://www.youtube.com/watch?v=h71MNWRv99M](https://www.youtube.com/watch?v=h71MNWRv99M)

* [https://github.com/parmarsachin/spark-dataframe-demo](https://github.com/parmarsachin/spark-dataframe-demo)

* [https://www.cloudera.com/documentation/enterprise/5-6-x/topics/spark_sparksql.html](https://www.cloudera.com/documentation/enterprise/5-6-x/topics/spark_sparksql.html)

* [https://www.cloudera.com/documentation/enterprise/5-6-x/topics/spark_sparksql.html](https://www.cloudera.com/documentation/enterprise/5-6-x/topics/spark_sparksql.html)

* [http://www.slideshare.net/jeykottalam/spark-sqlamp-camp2014](http://www.slideshare.net/jeykottalam/spark-sqlamp-camp2014)

* [http://www.meetup.com/Bangalore-Spark-Enthusiasts/events/227008581/](http://www.meetup.com/Bangalore-Spark-Enthusiasts/events/227008581/)

Spark SQL architecture contains three layers namely, Language API, Schema RDD, and Data Sources.

Language API − Spark is compatible with different languages and Spark SQL. It is also, supported by these languages- API (python, scala, java, HiveQL).

Schema RDD − Spark Core is designed with special data structure called RDD. Generally, Spark SQL works on schemas, tables, and records. Therefore, we can use the Schema RDD as temporary table. We can call this Schema RDD as Data Frame.

Data Sources − Usually the Data source for spark-core is a text file, Avro file, etc. However, the Data Sources for Spark SQL is different. Those are Parquet file, JSON document, HIVE tables, and Cassandra database.

* [https://rklicksolutions.wordpress.com/2016/03/03/tutorial-spark-1-6-sql-and-dataframe-operations/](https://rklicksolutions.wordpress.com/2016/03/03/tutorial-spark-1-6-sql-and-dataframe-operations/)
* Build Spark : [http://mbonaci.github.io/mbo-spark/](http://mbonaci.github.io/mbo-spark/)
* http://spark.apache.org/docs/latest/building-spark.html

Spark SQL example practice [https://www.infoq.com/articles/apache-spark-sql](https://www.infoq.com/articles/apache-spark-sql) Add a custom footer





**Alter Database**


    ALTER (DATABASE|SCHEMA) db_name SET DBPROPERTIES (key1=val1, ...)

Set one or more properties in the specified database. If a particular property is already set in the database, this will override the the old value with the new one.


**Alter Table or View**

    ALTER (TABLE|VIEW) [db_name.]table_name RENAME TO [db_name.]new_table_name

Rename an existing table or view. If the destination table name already exists, an exception will be thrown. This operation does not support moving tables across databases.


    ALTER (TABLE|VIEW) table_name SET TBLPROPERTIES (key1=val1, key2=val2, ...)

Set the properties of an existing table or view. If a particular property was already set, this will override the old value with the new one.


      ALTER (TABLE|VIEW) table_name UNSET TBLPROPERTIES
      [IF EXISTS] (key1, key2, ...)

Drop one or more properties of an existing table or view. If a specified property does not exist, an exception will be thrown.

       IF EXISTS
           If a specified property does not exist, nothing will happen.

      ALTER TABLE table_name [PARTITION part_spec] SET SERDE serde
         [WITH SERDEPROPERTIES (key1=val1, key2=val2, ...)]

      ALTER TABLE table_name [PARTITION part_spec]
         SET SERDEPROPERTIES (key1=val1, key2=val2, ...)

      part_spec:
          : (part_col_name1=val1, part_col_name2=val2, ...)

Set the SerDe and/or the SerDe properties of a table or partition. If a specified SerDe property was already set, this will override the old value with the new one. Setting the SerDe is only allowed for tables created using the Hive format.


**Alter Table Partitions**

      ALTER TABLE table_name ADD [IF NOT EXISTS]
          (PARTITION part_spec [LOCATION path], ...)

       part_spec:
         : (part_col_name1=val1, part_col_name2=val2, ...)

Add partitions to the table, optionally with a custom location for each partition added. This is only supported for tables created using the Hive format.

     IF NOT EXISTS
        If the specified partitions already exist, no action will be taken.

     ALTER TABLE table_name PARTITION part_spec RENAME TO PARTITION part_spec

       part_spec:
         : (part_col_name1=val1, part_col_name2=val2, ...)

Changes the partitioning field values of a partition. This operation is only allowed for tables created using the Hive format.


       ALTER TABLE table_name DROP [IF EXISTS] (PARTITION part_spec, ...)
       part_spec:
         : (part_col_name1=val1, part_col_name2=val2, ...)

Drops partitions from a table or view. This operation is only allowed for tables created using the Hive format.

      IF EXISTS
         If the specified partition does not exists, no action will be taken.



     ALTER TABLE table_name PARTITION part_spec SET LOCATION path

      part_spec:
        : (part_col_name1=val1, part_col_name2 =val2, ...)

Sets the location of the specified partition. Setting the location of individual partitions is only allowed for tables created using the Hive format.



**Analyze Table**


       ANALYZE TABLE [db_name.]table_name COMPUTE STATISTICS analyze_option

Write statistics about a table into the underlying metastore for future query optimizations. Currently the only analyze option supported is NOSCAN, which means the table won’t be scanned to generate the statistics. This command is only supported for tables created using the Hive format.


**Cache Table**


        CACHE [LAZY] TABLE [db_name.]table_name

Cache the contents of the table in memory. Subsequent queries on this table will bypass scanning the original files containing its contents as much as possible.


LAZY
    Cache the table lazily instead of eagerly scanning the entire table. 



**Clear Cache**

Clears the cache associated with a SQLContext.


     CLEAR CACHE



**Create Database**


        CREATE (DATABASE|SCHEMA) [IF NOT EXISTS] db_name
           [COMMENT comment_text]
           [LOCATION path]
           [WITH DBPROPERTIES (key1=val1, key2=val2, ...)]

Create a database. If a database with the same name already exists, an exception will be thrown.

      IF NOT EXISTS
          If a database with the same name already exists, nothing will happen.
      LOCATION
            If the specified path does not already exist in the underlying file system,
             this command will try to    create a directory with the path. When the database is dropped later, this directory will be deleted.




**Create Function**


      CREATE [TEMPORARY] FUNCTION [db_name.]function_name AS class_name
          [USING resource, ...]

      resource:
          : (JAR|FILE|ARCHIVE) file_uri

Create a function. The specified class for the function must extend either UDF or UDAF in org.apache.hadoop.hive.ql.exec, or one of AbstractGenericUDAFResolver, GenericUDF, or GenericUDTF in org.apache.hadoop.hive.ql.udf.generic. If a function with the same name already exists in the database, an exception will be thrown. Note: This command is supported only when Hive support is enabled.

TEMPORARY
    The created function will be available only in this session and will not be persisted to the underlying metastore, if any. No database name may be specified for temporary functions.
USING <resources>
    Specify the resources that must be loaded to support this function. A list of jar, file, or archive URIs may be specified. Known issue: adding jars does not work from the Spark shell (SPARK-8586).



**Create Table**


      CREATE [TEMPORARY] TABLE [IF NOT EXISTS] [db_name.]table_name
        [(col_name1[:] col_type1 [COMMENT col_comment1], ...)]
        USING datasource
        [OPTIONS (key1=val1, key2=val2, ...)]
        [PARTITIONED BY (col_name1, col_name2, ...)]
           [CLUSTERED BY (col_name3, col_name4, ...) INTO num_buckets BUCKETS]
           [AS select_statement]

Create a table using a data source. If a table with the same name already exists in the database, an exception will be thrown.

TEMPORARY
    The created table will be available only in this session and will not be persisted to the underlying metastore, if any. This may not be specified with IF NOT EXISTS or AS <select_statement>. To use AS <select_statement> with TEMPORARY, one option is to create a TEMPORARY VIEW instead.



     CREATE TEMPORARY VIEW table_name AS select_statement

There is also “CREATE OR REPLACE TEMPORARY VIEW” that may be handy if you don’t care whether the temporary view already exists or not. Note that for TEMPORARY VIEW you cannot specify datasource, partition or clustering options since a view is not materialized like tables.

      IF NOT EXISTS
           If a table with the same name already exists in the database, nothing will happen. This may not be specified when creating a temporary table.
USING <data source>
    Specify the file format to use for this table. The data source may be one of TEXT, CSV, JSON, JDBC, PARQUET, ORC, and LIBSVM, or a fully qualified class name of a custom implementation of org.apache.spark.sql.sources.DataSourceRegister.
PARTITIONED BY
    The created table will be partitioned by the specified columns. A directory will be created for each partition.
CLUSTERED BY
    Each partition in the created table will be split into a fixed number of buckets by the specified columns. This is typically used with partitioning to read and shuffle less data. Support for SORTED BY will be added in a future version.
AS <select_statement>
    Populate the table with input data from the select statement. This may not be specified with TEMPORARY TABLE or with a column list. To specify it with TEMPORARY, use CREATE TEMPORARY VIEW instead.

Examples:


       CREATE TABLE boxes (width INT, length INT, height INT) USING CSV

       CREATE TEMPORARY TABLE boxes
          (width INT, length INT, height INT)
         USING PARQUET
         OPTIONS ('compression'='snappy')

        CREATE TABLE rectangles
           USING PARQUET
          PARTITIONED BY (width)
          CLUSTERED BY (length) INTO 8 buckets
           AS SELECT * FROM boxes

        CREATE OR REPLACE TEMPORARY VIEW temp_rectangles
            AS SELECT * FROM boxes

Create Table with Hive format


            CREATE [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name
                [(col_name1[:] col_type1 [COMMENT col_comment1], ...)]
                [COMMENT table_comment]
                [PARTITIONED BY (col_name2[:] col_type2 [COMMENT col_comment2], ...)]
                [ROW FORMAT row_format]
                [STORED AS file_format]
                [LOCATION path]
                [TBLPROPERTIES (key1=val1, key2=val2, ...)]
                [AS select_statement]

row_format:
    : SERDE serde_cls [WITH SERDEPROPERTIES (key1=val1, key2=val2, ...)]
    | DELIMITED [FIELDS TERMINATED BY char [ESCAPED BY char]]
        [COLLECTION ITEMS TERMINATED BY char]
        [MAP KEYS TERMINATED BY char]
        [LINES TERMINATED BY char]
        [NULL DEFINED AS char]

file_format:
    : TEXTFILE | SEQUENCEFILE | RCFILE | ORC | PARQUET | AVRO
    | INPUTFORMAT input_fmt OUTPUTFORMAT output_fmt

Create a table using the Hive format. If a table with the same name already exists in the database, an exception will be thrown. When the table is dropped later, its data will be deleted from the file system. Note: This command is supported only when Hive support is enabled.

EXTERNAL
    The created table will use the custom directory specified with LOCATION. Queries on the table will be able to access any existing data previously stored in the directory. When an EXTERNAL table is dropped, its data is not deleted from the file system. This flag is implied if LOCATION is specified.
IF NOT EXISTS
    If a table with the same name already exists in the database, nothing will happen.
PARTITIONED BY
    The created table will be partitioned by the specified columns. This set of columns must be distinct from the set of non-partitioned columns. Partitioned columns may not be specified with AS <select_statement>.
ROW FORMAT
    Use the SERDE clause to specify a custom SerDe for this table. Otherwise, use the DELIMITED clause to use the native SerDe and specify the delimiter, escape character, null character etc.
STORED AS
    Specify the file format for this table. Available formats include TEXTFILE, SEQUENCEFILE, RCFILE, ORC, PARQUET and AVRO. Alternatively, the user may specify his own input and output formats through INPUTFORMAT and OUTPUTFORMAT. Note that only formats TEXTFILE, SEQUENCEFILE, and RCFILE may be used with ROW FORMAT SERDE, and only TEXTFILE may be used with ROW FORMAT DELIMITED.
LOCATION
    The created table will use the specified directory to store its data. This clause automatically implies EXTERNAL.
AS <select_statement>
    Populate the table with input data from the select statement. This may not be specified with PARTITIONED BY.

Examples:
Copy to clipboardCopy

CREATE TABLE my_table (name STRING, age INT)

CREATE EXTERNAL TABLE IF NOT EXISTS my_table (name STRING, age INT)
    COMMENT 'This table is created with existing data'
    LOCATION 'spark-warehouse/tables/my_existing_table'

CREATE TABLE my_table (name STRING, age INT)
    COMMENT 'This table is partitioned'
    PARTITIONED BY (hair_color STRING COMMENT 'This is a column comment')
    TBLPROPERTIES ('status'='staging', 'owner'='andrew')

CREATE TABLE my_table (name STRING, age INT)
    COMMENT 'This table specifies a custom SerDe'
    ROW FORMAT SERDE 'org.apache.hadoop.hive.ql.io.orc.OrcSerde'
    STORED AS
        INPUTFORMAT 'org.apache.hadoop.hive.ql.io.orc.OrcInputFormat'
        OUTPUTFORMAT 'org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat'

CREATE TABLE my_table (name STRING, age INT)
    COMMENT 'This table uses the CSV format'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    STORED AS TEXTFILE

CREATE TABLE your_table
    COMMENT 'This table is created with existing data'
    AS SELECT * FROM my_table

Create Table Like
Copy to clipboardCopy

CREATE TABLE [IF NOT EXISTS] [db_name.]table_name1 LIKE [db_name.]table_name2

Create a table using the metadata of an existing

table. The created table always uses its own directory in the default warehouse location even if the existing table is EXTERNAL. The existing table must not be a temporary table.
