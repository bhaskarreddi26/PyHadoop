find all the prime numbers up to 2 million. We’ll do this very naively by first finding all composite (non-prime) numbers, then find all numbers that are not composite to get the prime numbers.

We’ll find all composite numbers by taking every natural number from 2 to 2 million, then find all multiples of these numbers that are smaller than or equal to 2 million. We will have many duplicates (6 will show up in our multiples of both 2 and 3, for example),

      val n = 2000000
      n: Int = 2000000
      val composite = sc.parallelize(2 to n, 8).map(x => (x, (2 to (n / x)))).flatMap(kv => kv._2.map(_ * kv._1))
      val prime = sc.parallelize(2 to n, 8).subtract(composite)
      prime.collect()
    

![](http://dev.sortable.com/images/spark-repartition/no_repartition_DAG.png)

**What is Wrong :+1: **

When we ran sc.parallelize(2 to n, 8), Spark used a partitioning scheme that nicely divided the data into 8 even groups. It most likely used a range partitioner, where the numbers from 2-250000 were in the first partition, 250001-500000 in the second, etc. However, our map turned this into (key,value) pairs where the values had wildly different sizes. Each value was a list of all integers we needed to multiply the key by to find the multiples up to 2 million. For half of them (all keys greater than 1 million) this meant that the value was an empty list. Our largest value was for key 2, which had all integers from 2 to 1000000. This is why the first partition had most of the data and took the greatest amount of time, while the last four had no data.



**How do we fix this?**
We can repartition our data. Calling .repartition(numPartitions) on an RDD in Spark will shuffle the data into the number of partitions we specify. Let’s try adding that to our code.

We’ll run the same thing as before, but insert .repartition(8) between the .map and the .flatMap. Our RDD will have the same number of partitions as before, but the data will be redistributed across those partitions. Then our second line looks like this:

       val composite = sc.parallelize(2 to n, 8).map(x => (x, (2 to (n / x)))).repartition(8).flatMap(kv => kv._2.map(_ * kv._1))


![](http://dev.sortable.com/images/spark-repartition/repartition_DAG.png)


http://dev.sortable.com/spark-repartition/
