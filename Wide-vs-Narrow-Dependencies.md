Compositions on RDDs are represented as a lineage graph ; a Directed Asyclic Graph 9DAG) representing the compositions done on the RDD.

Narrow Dependencies :

Each partion of the parent RDD is used by at most one partition of the child RDD.

FAST ! No shuffle necessary.Optimizations like pipelining possible.

Ex"  map,filter,union,narrow dependency join


Wide Dependencies :

Each partion of the parents RDD may be dpendend on by multiple child partions

Slow ! Requies  all or some data to be shuffled over the network.


Ex GroupByKet, input not co paritions Join,