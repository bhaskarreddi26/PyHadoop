
- [A Gentle Introduction to Apache Spark on Databricks](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/346304/2168141618055043/484361/latest.html)
- [Apache Spark on Databricks for Data Scientists](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/346304/2168141618055194/484361/latest.html)
- [Apache Spark on Databricks for Data Engineers](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/346304/2168141618055109/484361/latest.html)



* https://www.youtube.com/watch?v=ssPBlqiRJGY


# **The Data Interfaces**

**The Dataset:**
The Dataset is Apache Spark's newest distributed collection and can be considered a combination of DataFrames and RDDs. It provides the typed interface that is available in RDDs while providing a lot of conveniences of DataFrames. It will be the core abstraction going forward.

**The DataFrame:**
The DataFrame is collection of distributed  <code>Row</code> types. These provide a flexible interface and are similar in concept to the DataFrames you may be familiar with in python (pandas) as well as in the R language.

**The RDD (Resilient Distributed Dataset):**
Apache Spark's first abstraction was the RDD or Resilient Distributed Dataset. Essentially it is an interface to a sequence of data objects that consist of one or more types that are located across a variety of machines in a cluster. RDD's can be created in a variety of ways and are the "lowest level" API available to the user. While this is the original data structure made available, new users should focus on Datasets as those will be supersets of the current RDD functionality.


**Transformation :**

![](http://training.databricks.com/databricks_guide/gentle_introduction/trans_and_actions.png)


