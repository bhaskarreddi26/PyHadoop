* https://databricks.gitbooks.io/databricks-spark-knowledge-base/content/
* http://www.slideshare.net/pwendell/tuning-and-debugging-in-apache-spark
* https://sparkhub.databricks.com/video/tuning-and-debugging-apache-spark/
* https://spark-summit.org/2014/training/

****Configuring Spark with SparkConf****


    Creating an application using a SparkConf in Scala
    // Construct a conf
    val conf = new SparkConf()
    conf.set("spark.app.name", "My Spark App")
    conf.set("spark.master", "local[4]")
    conf.set("spark.ui.port", "36000") // Override the default port

    // Create a SparkContext with this configuration
    val sc = new SparkContext(conf)
   

    Example Creating an application using a SparkConf in Java
    // Construct a conf
    SparkConf conf = new SparkConf();
    conf.set("spark.app.name", "My Spark App");
    conf.set("spark.master", "local[4]");
    conf.set("spark.ui.port", "36000"); // Override the default port
    // Create a SparkContext with this configuration
    JavaSparkContext sc = JavaSparkContext(conf);



The following are the key performance considerations:

**1.      Parallelism level**
Out of the box, Spark will infer what it thinks is a good degree of parallelism for RDDs, and this is sufficient for many use cases.

Input RDDs typically choose parallelism based on the underlying storage systems. For example, HDFS input RDDs have one partition for each block of the underlying HDFS file.

RDDs that are derived from shuffling other RDDs will have parallelism set based on the size of their parent RDDs.

 There are two ways to tune the degree of parallelism for operations.

a. During operations that shuffle data, you can always specify a degree of parallelism of the produced RDD as a parameter, for an example ReduceByKey is defined as reduceByKey([func], [numTasks]) something like

    val rdd2 = rdd1.reduceByKey(_ + _, numPartitions = X)

b. Any existing RDD can be redistributed to have more or fewer partitions.

The repartition() operator will randomly shuffle an RDD into the desired number of partitions. If you know you are shrinking the RDD, you can use the coalesce() operator; this is more efficient than repartition() since it avoids a shuffle operation. Either command has to be followed by a cache() or persist() to get the optimization benefit

 

For an Example if you are reading a large text file and immediately you filter to keep only a small fraction of the data. By default the RDD returned by filter() will have the same size as its parent and might have many empty or small partitions.

 

    textInput = sc.textFile(“hdfs://weblogs/*.log”)

    textInput.getNumPartitions()


# A filter which only use one day

    lines = textInput.filter(lambda line: line.startswith(“2016-05-21”))

    lines.getNumPartitions()



#  coalesce the lines RDD before caching

    lines = lines.coalesce(10).cache()

    lines.getNumPartitions()



 

**2.      Serialization Format**
When Spark is transferring data over the network or saving data to disk as part of the shuffling operations, it needs to serialize object into binary format. By default Spark uses built-in Java Serialization and it also support the use of Kryo Serialization library which enhance Java Serialization performance. Using Kryo can be set through the SparkConf  as you see in the example below

    val conf = new SparkConf()
    conf.set(“spark.serializer”, “org.apache.spark.serializer.KryoSerializer”)

 
**3.      Memory Management**

Workers memory is usually consumed for RDD Storage 60 %, temp shuffling storage 20 % and user code 20 %.

There are two tweaking options to consider:

* By defaulat the cahce() operation use MEMORY_ONLY storage level which mean that Spark might have to recompute the RDD if it was not in memory anymore  because the storage was needed for another newer RDD. In this case if recomputing is expensive as the data need to be read from a Database, you might consider using MEMORY_AND_DISK. Spark documentations has more details on all the different storage levels which can be used by the persist() operations

* Improving the default caching by using serialization instead of storing raw java object. Something like MEMORY_AND_Disk_SER

 

**4.  Hardware Provisioning**

 Generally speaking, Spark applications will benefit from having more memory and cores because Spark architecture allows for linear scaling. In addition to that Spark uses local disk volumes to store intermediate data required during shuffle operations along with RDD partitions that are spilled to disk. Using local large number of local disk or SSD would help the performance.

 
**5.  Use aggregateByKey, or reduceByKey instead of GroupByKey**
Both reduceByKey and aggregateByKey works better on a large dataset than groupByKey. That’s because Spark knows it can combine output with common key on each partition before shuffling the data. This is similar to the MapReduce Combiners which also known as a semi-reducer.

For more details, check out this blog from Databricks

**6.    Switching to LZF Compression can improve Shuffle performance**
Spark by default uses snappy-Java compressor but you might consider using LZF, you can use the following configuration property    conf.set(“Spark.io.compression.codec”,”lzf”), re-run your job and validate for any performance gain


**7.    To retrieve the RDD data, use Take(n) instead of collect() if possible**
If you need to retrieve partial of the data from a large RDD,  using the take(n) function is more efficient than using the collect() fn. This is due to the fact that take(n) will cause Spark to process only enough partitions to return n items. So for an example when using [some RDD].take(10), if the first partition have more than 10 items then the take(10) will only process one partition. However the collect() fn would trigger processing all the data and send it back to the driver.

**8.      Turn on speculative execution to prevent straggler**
Spark has provided a speculative mechanism to avoid the effect of stragglers (slow nodes). Essentially Spark identified slow tasks by looking at runtime distribution and re-launches those tasks on other nodes. To turn speculative execution ON, you need to set the configuration property spark.speculation to true, the default is false. Something like

Val conf= new SparkConf().set(“spark.speculation”,”true”)

 

**9. Consider using high level API as DataFrame, Spark SQL or Spark ML for core processing**

A DataFrame is a distributed collection of data organized into named columns and it works across Scala, Java, Python and R. When using DataFrames you get a key benefit is that Python performance is identical to other language. For a detailed example check out my other blog post

 

References
1.       Learning Spark Lightning-Fast Big Data Analysis – Book

2.       A Deeper Understanding of Spark Internals – Aaron Davidson’s presentation

3.       Tuning and Debugging in Apache Spark – Patrick Wendell’s excellent internals and debugging presentation

