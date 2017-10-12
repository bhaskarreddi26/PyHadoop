- ShuffledRDD : ShuffledRDD is created while the data is shuffled over the cluster. If you use any transformation(e.g. join,groupBy,repartition, etc.) which shuffles your data it will create a shuffledRDD.

- MapPartitionsRDD : MapPartitionsRDD will be created when you use mapPartition transformation.

- ParallelCollectionRDD : ParallelCollectionRDD is created when you create the RDD with the collection object.



https://github.com/JerryLead/SparkInternals/tree/master/markdown


A reduceByKey operation still involves a shuffle, as it's still required to ensure that all items with the same key become part of the same partition.

However, this will be a much smaller shuffle operation than a groupByKey operation. A reduceByKey will perform the reduction operation within each partition before shuffling, thus reducing the amount of data to be shuffled.

