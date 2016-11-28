Partitioning data is often used for distributing load horizontally, this has performance benefit, and helps in organizing data in a logical fashion. Example: if we are dealing with a large employee table and often run queries with WHERE clauses that restrict the results to a particular country or department . For a faster query response Hive table can be PARTITIONED BY (country STRING, DEPT STRING). Partitioning tables changes how Hive structures the data storage and Hive will now create subdirectories reflecting the partitioning structure like

.../employees/country=ABC/DEPT=XYZ.
If query limits for employee from country=ABC, it will only scan the contents of one directory country=ABC. This can dramatically improve query performance, but only if the partitioning scheme reflects common filtering. Partitioning feature is very useful in Hive, however, a design that creates too many partitions may optimize some queries, but be detrimental for other important queries. Other drawback is having too many partitions is the large number of Hadoop files and directories that are created unnecessarily and overhead to NameNode since it must keep all metadata for the file system in memory.

Bucketing is another technique for decomposing data sets into more manageable parts. For example, suppose a table using date as the top-level partition and employee_id as the second-level partition leads to too many small partitions. Instead, if we bucket the employee table and use employee_id as the bucketing column, the value of this column will be hashed by a user-defined number into buckets. Records with the same employee_id will always be stored in the same bucket. Assuming the number of employee_id is much greater than the number of buckets, each bucket will have many employee_id. While creating table you can specify like CLUSTERED BY (employee_id) INTO XX  BUCKETS; where XX is the number of buckets . Bucketing has several advantages. The number of buckets is fixed so it does not fluctuate with data. If two tables are bucketed by employee_id, Hive can create a logically correct sampling. Bucketing also aids in doing efficient map-side joins etc.



Hive Partitioning:

Partition divides large amount of data into multiple slices based on value of a table column(s).

Assume that you are storing information of people in entire world spread across 196+ countries spanning around 500 crores of entries. If you want to query people from a particular country (Vatican city), in absence of partitioning, you have to scan all 500 crores of entries even to fetch thousand entries of a country. If you partition the table based on country, you can fine tune querying process by just checking the data for only one country partition. Hive partition creates a separate directory for a column(s) value.

Pros:

Distribute execution load horizontally
Faster execution of queries in case of partition with low volume of data. e.g. Get the population from "Vatican city" returns very fast instead of searching entire population of world.
Cons:

Possibility of too many small partition creations - too many directories.
Effective for low volume data for a given partition. But some queries like group by on high volume of data still take long time to execute. e.g. Grouping of population of China will take long time compared to grouping of population in Vatican city. Partition is not solving responsiveness problem in case of data skewing towards a particular partition value.
Hive Bucketing:

Bucketing decomposes data into more manageable or equal parts.

With partitioning, there is a possibility that you can create multiple small partitions based on column values. If you go for bucketing, you are restricting number of buckets to store the data. This number is defined during table creation scripts.

Pros

Due to equal volumes of data in each partition, joins at Map side will be quicker.
Faster query response like partitioning
Cons

You can define number of buckets during table creation but loading of equal volume of data has to be done manually by programmers.


http://www.geoinsyssoft.com/hive-partition-bucketing/

https://community.hortonworks.com/questions/23103/hive-deciding-the-number-of-buckets.html
http://www.slideshare.net/BenjaminLeonhardi/hive-loading-data



