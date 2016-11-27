Note: when using custom objects as the key in key-value pair operations, you must be sure that a custom equals() method is accompanied with a matching hashCode() method. For full details, see the contract outlined in the Object.hashCode() documentation.

**Shuffle operations**

* Certain operations within Spark trigger an event known as the shuffle. The shuffle is Spark’s mechanism for re-distributing data so that it’s grouped differently across partitions. This typically involves copying data across executors and machines, making the shuffle a complex and costly operation.

In Spark, data is generally not distributed across partitions to be in the necessary place for a specific operation. During computations, a single task will operate on a single partition - thus, to organize all the data for a single reduceByKey reduce task to execute, Spark needs to perform an all-to-all operation. It must read from all partitions to find all the values for all keys, and then bring together values across partitions to compute the final result for each key - this is called the shuffle.


  1. mapPartitions to sort each partition using, for example, .sorted
  1. repartitionAndSortWithinPartitions to efficiently sort partitions while simultaneously repartitioning
  1. sortBy to make a globally ordered RDD

**Note :Operations which can cause a shuffle include repartition operations like repartition and coalesce, ‘ByKey operations (except for counting) like groupByKey and reduceByKey, and join operations like cogroup and join.**

* The Shuffle is an expensive operation since it involves disk I/O, data serialization, and network I/O. To organize data for the shuffle.

* Internally, results from individual map tasks are kept in memory until they can’t fit. Then, these are sorted based on the target partition and written to a single file. On the reduce side, tasks read the relevant sorted blocks.

* Certain shuffle operations can consume significant amounts of heap memory since they employ in-memory data structures to organize records before or after transferring them. Specifically, reduceByKey and aggregateByKey create these structures on the map side, and 'ByKey operations generate these on the reduce side. When data does not fit in memory Spark will spill these tables to disk, incurring the additional overhead of disk I/O and increased garbage collection.

* https://spark.apache.org/docs/latest/configuration.html

* Spark’s cache is fault-tolerant – if any partition of an RDD is lost, it will automatically be recomputed using the transformations that originally created it.



1. MEMORY_ONLY 	Store RDD as deserialized Java objects in the JVM. If the RDD does not fit in memory, some partitions will not be cached and will be recomputed on the fly each time they're needed. This is the default level.

1. MEMORY_AND_DISK 	Store RDD as deserialized Java objects in the JVM. If the RDD does not fit in memory, store the partitions that don't fit on disk, and read them from there when they're needed.

1. MEMORY_ONLY_SER
1. (Java and Scala) 	Store RDD as serialized Java objects (one byte array per partition). This is generally more space-efficient than deserialized objects, especially when using a fast serializer, but more CPU-intensive to read.

1. MEMORY_AND_DISK_SER
1. (Java and Scala) 	Similar to MEMORY_ONLY_SER, but spill partitions that don't fit in memory to disk instead of recomputing them on the fly each time they're needed.

1. DISK_ONLY 	Store the RDD partitions only on disk.

1. MEMORY_ONLY_2, MEMORY_AND_DISK_2, etc. 	Same as the levels above, but replicate each partition on two cluster nodes.

1. OFF_HEAP (experimental) 	Similar to MEMORY_ONLY_SER, but store the data in off-heap memory. This requires off-heap memory to be enabled. 
