Compositions on RDDs are represented as a lineage graph ; a Directed Asyclic Graph 9DAG) representing the compositions done on the RDD.

**Narrow Dependencies :**

Each partion of the parent RDD is used by at most one partition of the child RDD.

FAST ! No shuffle necessary.Optimizations like pipelining possible.

Ex-  map,filter,union,narrow dependency join


**Wide Dependencies :**

Each partion of the parents RDD may be dpendend on by multiple child partions

Slow ! Requies  all or some data to be shuffled over the network.


Ex GroupByKey, input not co partitions Join


![](https://4.bp.blogspot.com/-YGgWG0dOd1w/WdBrr-UeclI/AAAAAAAACYs/JpGnsvQuGrEVgWtDPyT4pFUf4BmFFNW_ACLcBGAs/s320/Untitled.png)

– Narrow dependency: RDD operations like map, union, filter can operate on a single partition and map the data of that partition to resulting single partition. These kind of operations which maps data from one to one partition are referred as Narrow operations. Narrow operations doesn’t required to distribute the data across the partitions.

– Wide dependency: RDD operations like groupByKey, distinct, join may require to map the data across the partitions in new RDD. These kind of operations which maps data from one to many partitions are referred as Wide operations


![](https://d26dzxoao6i3hh.cloudfront.net/items/1m0S1m2V0k302D45252Y/Image%202014-04-03%20at%2010.24.16%20nachm..png?v=7bf2cf00)