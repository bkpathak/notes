## Notes from Learning Spark book
### Partitioning in Spark

Many of the Spark's operation involves shuffling of the data acroos the networks. Partitioning of the RDDs will help all of these operations. Some of the operations that benefits from partitioning are:
> cogroup, groupWith, join, leftOutherJoin, rightOuterJoin, groupByKey, reduceByKey, combineBykey, and lookup.

``` val listRDD = sc.parallelize(List(1 to 10000)).partitionBy(new hashPartitioner(100)).cache```

### Transformations that affect Partitioning
The transformation which cannot be guaranteed to produce a known partitioning, the output RRD will not have a `partiitoner` set.

The `map` and `flatMap` transformation doesn't guarantte to have the `key` remain unchanged after applying the transformation, so the output RDD will not have a `partitioner`.  

Operations that result in a partitioner being set on the output RDD are:
> cogroup, groupWith, join, leftOuterJoin, rightOuterJoin, groupByKey, reduceByKey, combineByKey, partitionBy, sort, mapValues, flatMapValues and filter.

All other operations will produce result with no partitioner.

### Stages and Task
When map() transformation is run om dataset, a single stage of tasks is launched. A stage is a group of tasks that all perform the same computation, but on different input data. One task is launched for each partitition.
