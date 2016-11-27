Note: when using custom objects as the key in key-value pair operations, you must be sure that a custom equals() method is accompanied with a matching hashCode() method. For full details, see the contract outlined in the Object.hashCode() documentation.

**Shuffle operations**

* Certain operations within Spark trigger an event known as the shuffle. The shuffle is Spark’s mechanism for re-distributing data so that it’s grouped differently across partitions. This typically involves copying data across executors and machines, making the shuffle a complex and costly operation.

In Spark, data is generally not distributed across partitions to be in the necessary place for a specific operation. During computations, a single task will operate on a single partition - thus, to organize all the data for a single reduceByKey reduce task to execute, Spark needs to perform an all-to-all operation. It must read from all partitions to find all the values for all keys, and then bring together values across partitions to compute the final result for each key - this is called the shuffle.


  1. mapPartitions to sort each partition using, for example, .sorted
  1. repartitionAndSortWithinPartitions to efficiently sort partitions while simultaneously repartitioning
  1. sortBy to make a globally ordered RDD
