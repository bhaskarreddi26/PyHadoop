- ML Algorithms: common learning algorithms such as classification, regression, clustering, and collaborative filtering
- Featurization: feature extraction, transformation, dimensionality reduction, and selection
- Pipelines: tools for constructing, evaluating, and tuning ML Pipelines
- Persistence: saving and load algorithms, models, and Pipelines
- Utilities: linear algebra, statistics, data handling, etc.

> **Note : As of Spark 2.0, the RDD-based APIs in the spark.mllib package have entered maintenance mode. The primary Machine Learning API for Spark is now the DataFrame-based API in the spark.ml package.**


What is “Spark ML”?

“Spark ML” is not an official name but occasionally used to refer to the MLlib DataFrame-based API. This is majorly due to the org.apache.spark.ml Scala package name used by the DataFrame-based API, and the “Spark ML Pipelines” term we used initially to emphasize the pipeline concept.

> **Note : MLlib uses the linear algebra package Breeze, which depends on netlib-java for optimised numerical processing. If native libraries1 are not available at runtime, you will see a warning message and a pure JVM implementation will be used instead.**

> **Due to licensing issues with runtime proprietary binaries, we do not include netlib-java’s native proxies by default. To configure netlib-java / Breeze to use system optimised binaries, include com.github.fommil.netlib:all:1.1.2 (or build Spark with -Pnetlib-lgpl) as a dependency of your project and read the netlib-java documentation for your platform’s additional installation instructions.**

> **To use MLlib in Python, you will need NumPy version 1.4 or newer**