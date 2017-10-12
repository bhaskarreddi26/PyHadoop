Reduce by key internally calls combineBykey. Hence the basic way of task execution is same for both.

The choice of CombineByKey over reduceBykey is when the input Type and output Type is not expected to be the same. So combineByKey will have a extra overhead of converting one type to another .

If the type conversion is omitted there is no difference at all .

Please follow the following links

* http://bytepadding.com/big-data/spark/reducebykey-vs-combinebykey

* http://bytepadding.com/big-data/spark/groupby-vs-reducebykey

* http://bytepadding.com/big-data/spark/combine-by-key-to-find-max
