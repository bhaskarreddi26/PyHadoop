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

