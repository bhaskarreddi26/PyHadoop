**Starting Point: SparkSession**

    import org.apache.spark.sql.SparkSession

    val spark = SparkSession
      .builder()
      .appName("Spark SQL basic example")
      .config("spark.some.config.option", "some-value")
      .getOrCreate()

     // For implicit conversions like converting RDDs to DataFrames
     import spark.implicits._


**Note **

- val sqlContext = new org.apache.spark.sql.SQLContext(sc)
constructor SQLContext in class SQLContext is deprecated: Use SparkSession.builder instead.

- registerTempTable in class Dataset is deprecated: Use createOrReplaceTempView(viewName) instead.


--------------------------------------------------------------
Creating Dataframe 


      import org.apache.spark.sql.functions._


     val client = sc.parallelize(Seq(
     ("Abhishek", "C1"), 
     ("XUELAN", "C2"),
     ("Xahir", "C3")

    )).toDF("ClientName", "ClientCode")

    client.show()





    val amount = sc.parallelize(Seq(
     ("C1", "C11",3122), 
     ("C1", "C12",4312), 
     ("C2", "C21",21431), 
     ("C2", "C31",87588), 
     ("C3", "C32",98769), 
     ("C3", "C33",86567), 
     ("C3", "C34",23112)
 

    )).toDF("ClientCode", "OperationCode" ,"opAmount")

    amount.show()


      val dfAverage = amount.join(client,"clientCode") .groupBy(client("clientName"))
       .agg(avg(amount("opAmount")).as("average"))
        .select("clientName","average")

       dfAverage.show()


        import sqlContext.implicits._
        import org.apache.spark.sql._
        import org.apache.spark.sql.functions._
     
         client.createOrReplaceTempView("client")
         amount.createOrReplaceTempView("amount")

         val result = spark.sqlContext.sql("SELECT client.ClientName,avg(amount.opAmount)as average FROM amount JOIN client on 
       amount.ClientCode=client.ClientCode GROUP BY client.ClientName")

       result.show()


         +----------+----------+
         |ClientName|ClientCode|
         +----------+----------+
         |  Abhishek|        C1|
         |    XUELAN|        C2|
         |     Xahir|        C3|
         +----------+----------+

         +----------+-------------+--------+
         |ClientCode|OperationCode|opAmount|
         +----------+-------------+--------+
         |        C1|          C11|    3122|
         |        C1|          C12|    4312|
         |        C2|          C21|   21431|
         |        C2|          C31|   87588|
         |        C3|          C32|   98769|
         |        C3|          C33|   86567|
         |        C3|          C34|   23112|
         +----------+-------------+--------+

       +----------+-----------------+
       |clientName|          average|
       +----------+-----------------+
       |  Abhishek|           3717.0|
       |     Xahir|69482.66666666667|
       |    XUELAN|          54509.5|
       +----------+-----------------+