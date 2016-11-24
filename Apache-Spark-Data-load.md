****Loading text files****

spark is spark context

    Loading a text file in Scala
    val input = spark.textFile("file:///home/holden/repos/spark/README.md")

    Loading a text file in Java
    JavaRDD<String> input = spark.textFile("file:///home/holden/repos/spark/README.md")


Multipart inputs in the form of a directory containing all of the parts can be handled in two ways. We can just use the same textFile method and pass it a directory and it will load all of the parts into our RDD.

If our files are small enough, then we can use the SparkContext.wholeTextFiles() method and get back a pair RDD where the key is the name of the input file.

wholeTextFiles() can be very useful when each file represents a certain time period’s data. If we had files representing sales data from different periods, we could easily compute the average for each period,

    Example Average value per file in Scala
    val input = sc.wholeTextFiles("file://home/holden/salesFiles")
    val result = input.mapValues 
    { y => val nums = y.split(" ").map(x => x.toDouble)  nums.sum / nums.size.toDouble   }

**Spark supports reading all the files in a given directory and doing wildcard expansion on the input (e.g., part-*.txt). This is useful since large datasets are often spread across multiple files**


