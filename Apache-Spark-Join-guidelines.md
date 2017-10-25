> Join is one of the most expensive operations you will commonly use in Spark, so it is worth doing what you can to shrink your data before performing a join.



- When both RDDs have duplicate keys, the join can cause the size of the data to expand dramatically. It may be better to perform a distinct or combineByKey operation to reduce the key space or to use cogroup to handle duplicate keys instead of producing the full cross product. By using smart partitioning during the combine step, it is possible to prevent a second shuffle in the join (we will discuss this in detail later).

- If keys are not present in both RDDs you risk losing your data unexpectedly. It can be safer to use an outer join, so that you are guaranteed to keep all the data in either the left or the right RDD, then filter the data after the join.

- If one RDD has some easy-to-define subset of the keys, in the other you may be better off filtering or reducing before the join to avoid a big shuffle of data, which you will ultimately throw away anyway.

- In order to join data, Spark needs the data that is to be joined (i.e., the data based on each key) to live on the same partition. The default implementation of a join in Spark is a shuffled hash join. The shuffled hash join ensures that data on each partition will contain the same keys by partitioning the second dataset with the same default partitioner as the first, so that the keys with the same hash value from both datasets are in the same partition. While this approach always works, it can be more expensive than necessary because it requires a shuffle. The shuffle can be avoided if:

1. Both RDDs have a known partitioner.

2. One of the datasets is small enough to fit in memory, in which case we can do a broadcast hash join (we will explain what this is later).

> **Note that if the RDDs are colocated the network transfer can be avoided, along with the shuffle.**
> **Always persist after repartitioning.**

- DataFrame Joins
Joining data between DataFrames is one of the most common multi-DataFrame transformations. The standard SQL join types are all supported and can be specified as the joinType in df.join(otherDf, sqlCondition, joinType) when performing a join. As with joins between RDDs, joining with nonunique keys will result in the cross product (so if the left table has R1 and R2 with key1 and the right table has R3 and R5 with key1 you will get (R1, R3), (R1, R5), (R2, R3), (R2, R5)) in the output. 

> Using a self join and a lit(true), you can produce the cartesian product of your Dataset, which can be useful but also illustrates how joins (especially self joins) can easily result in unworkable data sizes.


https://techmagie.wordpress.com/2015/12/19/understanding-spark-partitioning/



**How many Partitions are good ?**

Having too few and too large number of partitions has certain advantages and disadvantages.So it is recommended to partition judiciously depending upon your cluster configuration and requirements.

**Disadvantages of too few partitions**

- Less concurrency – You are not using advantages of parallelism. There could be worker nodes which are sitting ideal.
Data skewing and improper resource utilization – Your data might be skewed on one partition and hence your one worker might be doing more than other workers and hence resource issues might come at that worker.


**Disadvantages of too many partitions**

- Task scheduling may take more time than actual execution time.

So there is trade off between number of partitions.Below is recommended guideline –

**Usually between 100 and 10K partitions depending upon cluster size and data.**

> Lower bound – 2 X number of cores in cluster available to application

> Upper bound – task should take 100+ ms time to execute.If it is taking less time than your partitioned data is too small and your application might be spending more time in scheduling the tasks.


https://databricks.gitbooks.io/databricks-spark-knowledge-base/content/performance_optimization/how_many_partitions_does_an_rdd_have.html




**What is an optimized way of joining large tables in Spark SQL**

- Use a broadcast join if you can (see this notebook). 

- Consider using a very large cluster (it's cheaper that you may think).

- Use the same partitioner. 

https://stackoverflow.com/questions/28395376/does-a-join-of-co-partitioned-rdds-cause-a-shuffle-in-apache-spark

- If the data is huge and/or your clusters cannot grow such that even (3) above leads to OOM, use a two-pass approach.
  -  First, re-partition the data and persist using partitioned tables (dataframe.write.partitionBy()).
  -  join sub-partitions serially in a loop, "appending" to the same final result table.

Side note: I say "appending" above because in production I never use SaveMode.Append. It is not idempotent and that's a dangerous thing. I use SaveMode.Overwrite deep into the subtree of a partitioned table tree structure. Prior to 2.0.0 and 1.6.2 you'll have to delete _SUCCESS or metadata files or dynamic partition discovery will choke.





https://databricks.com/blog/2016/05/23/apache-spark-as-a-compiler-joining-a-billion-rows-per-second-on-a-laptop.html


https://umbertogriffo.gitbooks.io/apache-spark-best-practices-and-tuning/content/avoiding_shuffle_less_stage,_more_fast/joining-a-large-and-a-small-rdd.html
