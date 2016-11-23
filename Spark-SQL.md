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
