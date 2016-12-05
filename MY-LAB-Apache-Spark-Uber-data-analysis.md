First, we import the packages needed for Spark ML K-means and SQL.       
              
              import org.apache.spark._
              import org.apache.spark.sql.SQLContext
              import org.apache.spark.sql.functions._
              import org.apache.spark.sql.types._
              import org.apache.spark.sql._
              import org.apache.spark.ml.feature.VectorAssembler
              import org.apache.spark.ml.clustering.KMeans


We specify the schema with a Spark Structype (Please note that if you are using a notebook, then you do not have to create the SQLContext).


             val SQLContext = new SQLContext(sc)

             import sqlContext.implicits._
             import sqlContext._



            val schema = StructType(Array(
                           | StructField("dt",TimestampType,true),
                           | StructField("lat",DoubleType,true),
                           | StructField("lon",DoubleType,true),
                           | StructField("base",StringType,true)
                          | ))



Using Spark 2.0 and --packages com.databricks:spark-csv_2.10:1.5.0, we create a DataFrame from a CSV file data source and apply the schema. 

![](https://www.mapr.com/sites/default/files/otherpageimages/112816blog/7.png)

Create same in csv file and keep your local.


****Load Data****

                val df=spark.read.format("com.databricks.spark.csv").
                        option("header","false").schema(schema).
                        csv("///home/osboxes/Sparkdatafile/Uber-Jan-Feb-FOIL.csv")

               or


               val df=spark.read..option("header","false").
                      schema(schema).
                      csv("///home/osboxes/Sparkdatafile/Uber-Jan-Feb-FOIL.csv") 


Data :+1: Download "Uber-Jan-Feb-FOIL.csv"

https://github.com/vaquarkhan/uber-tlc-foil-response



https://www.mapr.com/blog/monitoring-real-time-uber-data-using-spark-machine-learning-streaming-and-kafka-api-part-1