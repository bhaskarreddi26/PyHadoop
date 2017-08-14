If an RDD has too many partitions, then task scheduling may take more time than the actual execution time. To the contrary, having too less partitions is also not beneficial as some of the worker nodes could just be sitting idle resulting in less concurrency. This could lead to improper resource utilization and data skewing i.e. data might be skewed on a single partition and a worker node might be doing more than other worker nodes. Thus, there is always a trade off when it comes to deciding on the number of partitions.

**Some acclaimed guidelines for the number of partitions in Spark are as follows-**

When the number of partitions is between 100 and 10K partitions based on the size of the cluster and data, the lower and upper bound should be determined.

The lower bound for spark partitions is determined by 2 X number of cores in the cluster available to application.

Determining the upper bound for partitions in Spark, the task should take 100+ ms time to execute. If it takes less time, then the partitioned data might be too small or the application might be spending extra time in scheduling tasks.

**Types of Partitioning in Apache Spark**

* Hash Partitioning in Spark
* Range Partitioning in Spark


Hash Partitioning in Spark:

Hash Partitioning attempts to spread the data evenly across various partitions based on the key. Object.hashCode method is used to determine the partition in Spark as partition = key.hashCode () % numPartitions.

Range Partitioning in Spark:

Some Spark RDDs have keys that follow a particular ordering, for such RDDs, range partitioning is an efficient partitioning technique. In range partitioning method, tuples having keys within the same range will appear on the same machine. Keys in a range partitioner are partitioned based on the set of sorted range of keys and ordering of keys.

Spark’s range partitioning and hash partitioning techniques are ideal for various spark use cases but spark does allow users to fine tune how their RDD is partitioned, by using custom partitioner objects. Custom Spark partitioning is available only for pair RDDs i.e. RDDs with key value pairs as the elements can be grouped based on a function of each key. Spark does not provide explicit control of which key will go to which worker node but it ensures that a set of keys will appear together on some node. For instance, you might range partition the RDD based on the sorted range of keys so that elements having keys within the same range will appear on the same node or you might want to hash partition the RDD into 100 partitions so that keys that have same hash value for modulo 100 will appear on the same node.




* http://dev.sortable.com/spark-repartition/
* http://www.edureka.co/blog/demystifying-partitioning-in-spark
* http://blog.cloudera.com/blog/2015/03/how-to-tune-your-apache-spark-jobs-part-1/
* https://stackoverflow.com/questions/31610971/spark-repartition-vs-coalesce