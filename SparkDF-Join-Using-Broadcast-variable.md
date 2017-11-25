// Hive Tables
hive> select * from customer;
OK
1	Ramesh	32	Ahmedabad	000
2	Khilan	25	Delhi	1500
3	kaushik	23	Kota	2000 
4	Chaitali	25	Mumbai	6500 
5	Hardik	27	Bhopal	8500 
6	Komal	22	MP	4500 
Time taken: 0.568 seconds, Fetched: 6 row(s)

hive> select * from orders;
OK
102	2009-10-08 00:00:00	3	3000
100	2009-10-08 00:00:00	3	1500
101	2009-11-20 00:00:00	2	1560
103	2008-05-20 00:00:00	4	2060
Time taken: 0.185 seconds, Fetched: 4 row(s)

// Spark Shell

scala> sc.getConf.set("spark.serializer", "org.apache.spark.serializer.KryoSerializer")
res0: org.apache.spark.SparkConf = org.apache.spark.SparkConf@46c6541f

scala> import org.apache.spark.sql.hive.HiveContext
import org.apache.spark.sql.hive.HiveContext

scala> val hiveCtx = new HiveContext(sc)
hiveCtx: org.apache.spark.sql.hive.HiveContext = org.apache.spark.sql.hive.HiveContext@54139bd3

scala> val custtable = hiveCtx.sql("select * from customer");
custtable: org.apache.spark.sql.DataFrame = [id: string, name: string, age: string, address: string, salary: string]
scala> custtable.show
+---+--------+---+---------+------+
| id|    name|age|  address|salary|
+---+--------+---+---------+------+
|  1|  Ramesh| 32|Ahmedabad|   000|
|  2|  Khilan| 25|    Delhi|  1500|
|  3| kaushik| 23|     Kota| 2000 |
|  4|Chaitali| 25|   Mumbai| 6500 |
|  5|  Hardik| 27|   Bhopal| 8500 |
|  6|   Komal| 22|       MP| 4500 |
+---+--------+---+---------+------+

scala> val bcast_cust_table=sc.broadcast(custtable);
bcast_cust_table: org.apache.spark.broadcast.Broadcast[org.apache.spark.sql.DataFrame] = Broadcast(2)

scala> val ordertable=hiveCtx.sql("select * from orders");
ordertable: org.apache.spark.sql.DataFrame = [oid: string, odate: string, customer_id: string, amount: string]

val join_table=ordertable.join(bcast_cust_table.value,ordertable("customer_id")<=>bcast_cust_table.value("id") ,"inner")
+---+-------------------+-----------+------+---+--------+---+-------+------+
|oid|              odate|customer_id|amount| id|    name|age|address|salary|
+---+-------------------+-----------+------+---+--------+---+-------+------+
|102|2009-10-08 00:00:00|          3|  3000|  3| kaushik| 23|   Kota| 2000 |
|100|2009-10-08 00:00:00|          3|  1500|  3| kaushik| 23|   Kota| 2000 |
|101|2009-11-20 00:00:00|          2|  1560|  2|  Khilan| 25|  Delhi|  1500|
|103|2008-05-20 00:00:00|          4|  2060|  4|Chaitali| 25| Mumbai| 6500 |
+---+-------------------+-----------+------+---+--------+---+-------+------+
