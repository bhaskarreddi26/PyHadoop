**Starting Point: SparkSession**

    import org.apache.spark.sql.SparkSession

    val spark = SparkSession
      .builder()
      .appName("Spark SQL basic example")
      .config("spark.some.config.option", "some-value")
      .getOrCreate()

     // For implicit conversions like converting RDDs to DataFrames
     import spark.implicits._


Note 

- val sqlContext = new org.apache.spark.sql.SQLContext(sc)
constructor SQLContext in class SQLContext is deprecated: Use SparkSession.builder instead.

- registerTempTable in class Dataset is deprecated: Use createOrReplaceTempView(viewName) instead.
