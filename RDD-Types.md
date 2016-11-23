****Pair RDD ****
Pair RDDs are a useful building block in many programs, as they expose operations that allow you to act on each key in parallel or regroup data across the network. For example, pair RDDs have a reduceByKey() method that can aggregate data separately for each key, and a join() method that can merge two RDDs together by grouping elements with the same key.

For example, pair RDDs have a reduceByKey() method that can aggregate data separately for each key, and a join() method that can merge two RDDs together by grouping elements with the same key. It is common to extract fields from an RDD (representing, for instance, an event time, customer ID, or other identifier) and use those fields as keys in pair RDD operations.


**Creating Pair RDDs**
There are a number of ways to get pair RDDs in Spark. Many formats we explore loading from in Chapter 5 will directly return pair RDDs for their key/value data. In other cases we have a regular RDD that we want to turn into a pair RDD. We can do this by running a map() function that returns key/value pairs. To illustrate, we show code that starts with an RDD of lines of text and keys the data by the first word in each line.

The way to build key-value RDDs differs by language. In Python, for the functions on keyed data to work we need to return an RDD composed of tuples Creating a pair RDD using the first word as the key in Python

    pairs = lines.map(lambda x: (x.split(" ")[0], x))

In Scala, for the functions on keyed data to be available, we also need to return tuples . An implicit conversion on RDDs of tuples exists to provide the additional key/value functions.

Creating a pair RDD using the first word as the key in Scala

    val pairs = lines.map(x => (x.split(" ")(0), x))

Java doesn’t have a built-in tuple type, so Spark’s Java API has users create tuples using the scala.Tuple2 class. This class is very simple: Java users can construct a new tuple by writing new Tuple2(elem1, elem2) and can then access its elements with the ._1() and ._2() methods.

Java users also need to call special versions of Spark’s functions when creating pair RDDs. For instance, the mapToPair() function should be used in place of the basic map() function. This is discussed in more detail in “Java” on page 43, but let’s look at a simple case in Example 

Creating a pair RDD using the first word as the key in Java

    PairFunction<String, String, String> keyData =
    new PairFunction<String, String, String>() {
    public Tuple2<String, String> call(String x) {
    return new Tuple2(x.split(" ")[0], x);
    }
    };
JavaPairRDD<String, String> pairs = lines.mapToPair(keyData);