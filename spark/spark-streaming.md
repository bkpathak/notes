    A DStream is associated with a single receiver. For attaining read parallelism multiple receivers i.e. multiple DStreams need to be created.
    A receiver is run within an executor. It occupies one core. Ensure that there are enough cores for processing after receiver slots are booked i.e. spark.cores.max should take the receiver slots into account.
    The receivers are allocated to executors in a round robin fashion.
    When data is received from a stream source, receiver creates blocks of data.  A new block of data is generated every blockInterval milliseconds. N blocks of data are created during the batchInterval where N = batchInterval/blockInterval.
    These blocks are distributed by the BlockManager of the current executor to the block managers of other executors. After that, the Network Input Tracker running on the driver is informed about the block locations for further processing.
    A RDD is created on the driver for the blocks created during the batchInterval. The blocks generated during the batchInterval are partitions of the RDD. Each partition is a task in spark. blockInterval== batchinterval would mean that a single partition is created and probably it is processed locally.
    Having bigger blockinterval means bigger blocks. A high value of spark.locality.wait increases the chance of processing a block on the local node. A balance needs to be found out between these two parameters to ensure that the bigger blocks are processed locally.
    Instead of relying on batchInterval and blockInterval, you can define the number of partitions by calling dstream.repartition(n). This reshuffles the data in RDD randomly to create n number of partitions.
    An RDD's processing is scheduled by driver's jobscheduler as a job. At a given point of time only one job is active. So, if one job is executing the other jobs are queued.
    If you have two dstreams there will be two RDDs formed and there will be two jobs created which will be scheduled one after the another.
    To avoid this, you can union two dstreams. This will ensure that a single unionRDD is formed for the two RDDs of the dstreams. This unionRDD is then considered as a single job. However the partitioning of the RDDs is not impacted.
    If the batch processing time is more than batchinterval then obviously the receiver's memory will start filling up and will end up in throwing exceptions (most probably BlockNotFoundException). Currently there is  no way to pause the receiver.
    For being fully fault tolerant, spark streaming needs to enable checkpointing. Checkpointing increases the batch processing time.
    The frequency of metadata checkpoint cleaning can be controlled using spark.cleaner.ttl. But, data checkpoint cleaning happens automatically when the RDDs in the checkpoint are no more required. 
An RDD's processing is scheduled by driver's jobscheduler as a job. At a given point of time only one job is active. So, if one job is executing the other jobs are queued.
