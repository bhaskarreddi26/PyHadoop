**Properties of Partitions:**

* Partitions never span multiple machines i.e., tuples in the same partition are guaranteed to be on same machine.

* Each machine in the cluster contain one or more partitions

* The number of partitions to use is configurable .By default , it equals the total number of cores on all executor nodes.

Example if Machine have 4 core and 6 worker node means default no of partitions is 4*6 =24