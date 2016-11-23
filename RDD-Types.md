Pair RDDs are a useful building block in many programs, as
they expose operations that allow you to act on each key in parallel or regroup data
across the network. For example, pair RDDs have a reduceByKey() method that can
aggregate data separately for each key, and a join() method that can merge two
RDDs together by grouping elements with the same key.