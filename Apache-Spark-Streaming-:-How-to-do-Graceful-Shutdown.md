In my current project, I am using Spark Streaming as processing engine , Kafka as data source and Mesos as cluster /resource manager.
To be precise, i am using Direct Kafka Approach in spark for data ingestion.
Once a streaming application is up and running, there will be multiple things to do to make it stable ,consistent and seamless.
One of them is ensuring Graceful Shutdown to avoid data loss. In cases of restarting Streaming application, deploying changes, etc we have to ensure that the shutdown happens gracefully and in consistent state. It means that once the application receives shutdown signal, it should not accept any more data for processing but at the same time, it should make sure to process all the data/jobs for the current Kafka offsets in memory to get processed before bringing the application down. When the application restarts, it will read the Kafka offset from the checkpoint directory and start getting the data from kafka accordingly for processing.

In this post, i am going to share details how to do graceful shutdown of Spark Streaming application.
There are 2 ways   :
1. Explicitly calling the shutdown hook in driver program : 

       sys.ShutdownHookThread 
         {
            log.info("Gracefully stopping Spark Streaming Application")
            ssc.stop(true, true)
            log.info("Application stopped")
          }

The ssc.stop method’s 1st boolean argument is for stopping the associated spark context while the 2nd boolean argument is for graceful shutdown of streaming context.
      I tried this above approach in my spark application with version 1.5.1 but it did not work. The streaming application was shutting down gracefully but the spark context remained alive or lets say hung. The driver and executor processes were not getting exited. I had to use kill -9 command to forcefully terminate the spark context(which kills driver and executors ).
Later, i found out that this approach is old and was used for spark version before 1.4 . For new spark versions, we use the 2nd approach.

2. spark.streaming.stopGracefullyOnShutdown parameter :
        sparkConf.set(“spark.streaming.stopGracefullyOnShutdown","true")  
        Setting this parameter to True in spark configuration ensures the proper graceful shutdown in new Spark version (1.4 onwards) applications. Also we should not use 1st explicit shutdown hook approach or call the ssc.stop method in the driver along with this parameter . We can just set this parameter, and then call methods ssc.start() and ssc.awaitTermination() . No need to call ssc.stop method. Otherwise application might hung during shutdown. 
Please look at the spark source code for knowing how this parameter is used internally : https://github.com/apache/spark/blob/8ac71d62d976bbfd0159cac6816dd8fa580ae1cb/streaming/src/main/scala/org/apache/spark/streaming/StreamingContext.scala#L732

How to pass Shutdown Signal :
Now we know how to ensure graceful shutdown in spark streaming. But how can we pass the shutdown signal to spark streaming. One naive option is to use CTRL+C command at the screen terminal where we run driver program but obviously its not a good option.
One solution , which i am using is , grep the driver process of spark streaming and send a SIGTERM signal . When driver gets this signal, it initiates the graceful shutdown of the application.
We can write the command as below in some shell script  and run the script to pass shutdown signal :
ps -ef | grep spark |  grep <DriverProgramName> | awk '{print $2}'   | xargs kill  -SIGTERM
e.g. ps -ef | grep spark |  grep DataPipelineStreamDriver | awk '{print $2}'   | xargs kill  -SIGTERM

One limitation of this approach is that it can be run only on the same machine on which driver program was run and not on any other node machine of the spark cluster.
