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


-------------------------------------------------
- Correlation 

Calculating the correlation between two series of data is a common operation in Statistics.

Introduction: What Is Correlation and Why Is It Useful?

The term "correlation" refers to a mutual redepartment lationship or association between quantities. In almost any business, it is useful to express one quantity in terms of its relationship with others.

For example, sales might increase when the marketing spends more on TV advertisements, or a customer's average purchase amount on an e-commerce website might depend on a number of factors related to that customer. Often, correlation is the first step to understanding these relationships and subsequently building better business and statistical models.

**Correlation measure how two observed variables are related to each other . It has been used in many different ways in data science.**

- Correlation is used im univariate analysis to identify which feature is more predictive for classification of regression task.
- To identify multicollinearity in the feature set . Multicollinearity reduse the accuracy of model.
- Identify casual relation ship between variables.
- Their are many other extension like cca canonical correlation analysis.

-----------------------------------------------------------------

