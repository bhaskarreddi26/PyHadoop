* Dataset is a distributed collection of data. Dataset is a new interface added in Spark 1.6 that provides the benefits of RDDs (strong typing, ability to use powerful lambda functions) with the benefits of Spark SQL’s optimized execution engine.

* DataFrame is a Dataset organized into named columns. It is conceptually equivalent to a table in a relational database.

With a SparkSession, applications can create DataFrames from an existing RDD, from a Hive table, or from Spark data sources.

As an example, the following creates a DataFrame based on the content of a JSON file:
      val df = spark.read.json("/home/osboxes/Sparkdatafile/employee.json")
      df.show()
