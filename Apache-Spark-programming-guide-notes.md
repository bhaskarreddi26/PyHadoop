* Spark application consists of a driver program that runs the user’s main function and executes various parallel operations on a cluster.

* Spark provides is a resilient distributed dataset (RDD), which is a collection of elements partitioned across the nodes of the cluster that can be operated on in parallel.

* RDDs automatically recover from node failures.

* Spark is shared variables that can be used in parallel operations. By default, when Spark runs a function in parallel as a set of tasks on different nodes, it ships a copy of each variable used in the function to each task. Sometimes, a variable needs to be shared across tasks, or between tasks and the driver program.

* Spark supports two types of shared variables: 
   1. Broadcast variables, which can be used to cache a value in memory on all node.
   2. Accumulators, which are variables that are only “added” to, such as counters and sums.


* There are two ways to create RDDs:
  1. Parallelizing an existing collection in your driver program.

                  val data = Array(1, 2, 3, 4, 5)
                  val distData = sc.parallelize(data)

                  distData.reduce((a, b) => a + b) 

  2. Referencing a dataset in an external storage system, such as a shared filesystem, HDFS, HBase, or any data source offering a Hadoop InputFormat.




