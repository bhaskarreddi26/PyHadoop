**Properties of Partitions:**

* Partitions never span multiple machines i.e., tuples in the same partition are guaranteed to be on same machine.

* Each machine in the cluster contain one or more partitions

* The number of partitions to use is configurable .By default , it equals the total number of cores on all executor nodes.

**Default no of partitions **

Example if Machine have 4 core and 6 worker node means default no of partitions is 4*6 =24

-------------------------------------------------------

Partitioning is possible only on pair RDD as partition working only key.  



-------------------------------------------------------


          case class CFFPurchase(customerId:Int,destination:String,price:Double)

          val purchases =List(CFFPurchase(100,"Geneva",22.25),
                    CFFPurchase(300,"Zurich",42.25),
                    CFFPurchase(100,"Firebourg",12.40),
                    CFFPurchase(200,"st.Fallen",8.20),
                    CFFPurchase(100,"Lucerne",31.80),
                    CFFPurchase(300,"Basel",16.20))

         val purchasesRDD =sc.parallelize(purchases,3)

         val purchesePerMonth= purchasesRDD.map(p=>(p.customerId,(1,p.price))).reduceByKey((v1,v2)=>
        (v1._1+v2._1,v1._2+v2._2)).collect()
                     

-------------------------------------------------------

Hash partitioning :

Hash partitioning distribute data as er hashcode equlaay distributed.
p=k.hashCode() % numPartitions

Then , all tuples in the same partition p are sent to the achin hosting p

Range Partitioning :

1) an ordering of keys
2) a set of sorted ranges of key

Note : tuples with keys in the same range apper on the same machine 
-------------------------------------------------------
