- ShuffledRDD : ShuffledRDD is created while the data is shuffled over the cluster. If you use any transformation(e.g. join,groupBy,repartition, etc.) which shuffles your data it will create a shuffledRDD.

- MapPartitionsRDD : MapPartitionsRDD will be created when you use mapPartition transformation.

- ParallelCollectionRDD : ParallelCollectionRDD is created when you create the RDD with the collection object.



https://github.com/JerryLead/SparkInternals/tree/master/markdown