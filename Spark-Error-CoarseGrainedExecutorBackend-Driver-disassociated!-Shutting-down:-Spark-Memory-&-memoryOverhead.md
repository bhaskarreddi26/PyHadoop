7/08/31 15:58:07 WARN CoarseGrainedExecutorBackend: An unknown (datanode-022:43969) driver disconnected.

17/08/31 15:58:07 ERROR CoarseGrainedExecutorBackend: Driver 10.1.1.111:43969 disassociated! Shutting down.

ERROR CoarseGrainedExecutorBackend: Driver xx.xx.x.x:1xx disassociated! Shutting down.


Googling this error suggests increasing spark.yarn.driver.memoryOverhead or spark.yarn.executor.memoryOverhead or both. That has apparently worked for a lot of people. Or at least those who were smart enough to understand how these properties work.

What you need to consider here is that memoryOverhead is allocated out of the total amount of memory available to driver or executor, which is controlled by spark.driver.memory & spark.executor.memory.

What this means is that if you’re increasing executor’s or driver’s memoryOverhead, double check if there is enough memory allocated to driver and executor or not. In our case, the user was allocating all the memory available to driver as memoryOverhead, which meant there was none left for other other driver operations:

      spark-submit \
      –queue lis \
      –verbose \
      –master yarn-cluster \
      –conf spark.shuffle.service.enabled=true \
     –conf spark.shuffle.manager=sort \
     –conf spark.executor.memory=8g \
     –conf spark.dynamicAllocation.enabled=true \
     –conf spark.dynamicAllocation.minExecutors=10 \
    –conf spark.executor.cores=2 \
     –conf spark.driver.memory=8g \
    –conf spark.network.timeout=600s \
     –conf spark.scheduler.executorTaskBlacklistTime=3600000 \
     –conf spark.yarn.driver.memoryOverhead=8192 \
    –conf spark.yarn.executor.memoryOverhead=8192 \

You can clearly see what I meant in above paragraph. Instead of doing this, user should have increased executor and driver memory according to increase in executor memory overhead:

    spark-submit \
    –queue lis \
    –verbose \
    –master yarn-cluster \
    –conf spark.shuffle.service.enabled=true \
   –conf spark.shuffle.manager=sort \
   –conf spark.executor.memory=16g \
   –conf spark.dynamicAllocation.enabled=true \
   –conf spark.dynamicAllocation.minExecutors=10 \
   –conf spark.executor.cores=2 \
   –conf spark.driver.memory=16g \
   –conf spark.network.timeout=600s \
   –conf spark.scheduler.executorTaskBlacklistTime=3600000 \
   –conf spark.yarn.driver.memoryOverhead=8192 \
   –conf spark.yarn.executor.memoryOverhead=8192 \

 