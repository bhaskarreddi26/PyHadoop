**Flight Data Analysis using Spark GraphX**

* https://www.javacodegeeks.com/2016/03/get-started-using-apache-spark-graphx-scala.html

Problem Statement: To analyze Real-Time Flight data using Spark GraphX, provide near real-time computation results and visualize the results using Google Data Studio.

**Use Case – Computations to be done:**

* Compute the total number of flight routes
* Compute and sort the longest flight routes
* Display the airport with the highest degree vertex
* List the most important airports according to PageRank
* List the routes with the lowest flight costs

We will use Spark GraphX for the above computations and visualize the results using Google Data Studio.

**[Download dataset](https://drive.google.com/file/d/0B7Yoht-ttAeuaWdGZkRsSkVkN00/view)**


![](https://cdn.edureka.co/blog/wp-content/uploads/2017/05/Flow-Diagram-Spark-GraphX-Edureka.gif)


The property graph isa directed multigraph which can have multiple edges in parallel. Every edge and vertex has user defined properties associated with it. The parallel edges allow multiple relationships between the same vertices.


![](https://www.javacodegeeks.com/wp-content/uploads/2016/03/image01_flight-relationship.png)