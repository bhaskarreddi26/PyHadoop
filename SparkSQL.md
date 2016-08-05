SparkSQL

Exposes 3 processing interfaces: SQL, HiveQL and language integrated queries
Can be used in 2 modes
as a library
data processing tasks are expressed as SQL, HiveQL or integrated queries in a Scala app
3 key abstractions
SQLContext
HiveContext
DataFrame
as a distributed SQL execution engine
allows multiple users to share a single spark cluster
allows centralized caching across all jobs and across multiple data stores
DataFrame
represents a distributed collection of rows organized into named columns
Executing SQL queries provides us a DataFrame as the result
is schema aware i.e knows names and types of columns
provides methods for processing data
can be easily converted to regular RDD
can be registered as a temporary table to run SQL/HiveQL
2 ways to create a DF
from existing RDD
toDF if we can infer schema using a case class
createDataFrame is you want to pass the Schema explicitly (StructType, StructField)
from external DataSources
single unified interace to create DF, either from data stores (MySQL, PostgresSQL, Oracle, Cassandra) or from files (JSON, Parquet, ORC, CSV, HDFS, local, S3)
built-in support for JSON, Parquet, ORC, JDBC, Hive
uses DataFrameReader to read data from external datasources
can specify partiotioning, format and data source specific options
SQL/HiveContext has a factory method called read() that returns an instance of DataFrameReader
uses DataFrameWriter to write data to external datasources
can specify partiotioning, format and data source specific options
build-in functions
optimized for faster execution through code generation
import org.apache.spark.sql.functions._
Optimization techniques used
Reduced Disk IO
Skip rows
if a data store (for e.g. Parquet, ORC) maintains statistical info about data (min, max of a particular column in a group) then SparkSQL can take advantage of it to skip these groups
Skip columns (Use support of Parquet)
skip non-required partitions
Predicate Push down i.e. pushing filtering predicates to run natively on data stores like Cassandra, DB etc.
In-memory columnar caching
cache only required columns from any data store
compress the cached columns (using snappy) to minimize memory usage and GC
SparkSQL can automatically select a compression codec for a column based on data type
columnar format enables using of efficient compression techniques
run length encoding
delta encoding
dictionary encoding
Query optimization
uses both cost-based (in the physical planning phase) and rule-based (in the logical optimization phase) optimization
can even optimize across functions
code generation
