* https://www.youtube.com/watch?v=mKEn9C5bRck

**Graph and its representations**

Graph is a data structure that consists of following two components:

1. A finite set of vertices also called as nodes.
2. A finite set of ordered pair of the form (u, v) called as edge. The pair is ordered because (u, v) is not same as (v, u) in case of directed graph(di-graph). The pair of form (u, v) indicates that there is an edge from vertex u to vertex v. The edges may contain weight/value/cost.

![](http://image.slidesharecdn.com/walldisplay3dshapes-140407062304-phpapp01/95/wall-display-3dshapes-3-638.jpg)

Graphs are used to represent many real life applications: Graphs are used to represent networks. The networks may include paths in a city or telephone network or circuit network. Graphs are also used in social networks like linkedIn, facebook. For example, in facebook, each person is represented with a vertex(or node). Each node is a structure and contains information like person id, name, gender and locale. See this for more applications of graph.

-----------------------------------------------

GraphX extends the Spark RDD abstraction by introducing the Resilient Distributed Property Graph: a directed multigraph with properties attached to each vertex and edge. To support graph computation, GraphX exposes a set of fundamental operators (e.g., subgraph, joinVertices, and mapReduceTriplets) as well as an optimized variant of the Pregel API. In addition, GraphX includes a growing collection of graph algorithms and builders to simplify graph analytics tasks.


![](http://ampcamp.berkeley.edu/big-data-mini-course/img/social_graph.png)

Social network with users and their ages modeled as vertices and likes modeled as directed edges,We begin by creating the property graph from arrays of vertices and edges. 


     import org.apache.spark.graphx._
     import org.apache.spark.rdd.RDD

      val vertexArray = Array(
            (1L, ("Alice", 28)),
            (2L, ("Bob", 27)),
            (3L, ("Charlie", 65)),
            (4L, ("David", 42)),
            (5L, ("Ed", 55)),
            (6L, ("Fran", 50))
           )
        val edgeArray = Array(
            Edge(2L, 1L, 7),
            Edge(2L, 4L, 2),
            Edge(3L, 2L, 4),
            Edge(3L, 6L, 3),
            Edge(4L, 1L, 1),
            Edge(5L, 2L, 2),
            Edge(5L, 3L, 8),
            Edge(5L, 6L, 3)
             )


Results 

import org.apache.spark.graphx._
import org.apache.spark.rdd.RDD
vertexArray: Array[(Long, (String, Int))] = Array((1,(Alice,28)), (2,(Bob,27)), (3,(Charlie,65)), (4,(David,42)), (5,(Ed,55)), (6,(Fran,50)))
edgeArray: Array[org.apache.spark.graphx.Edge[Int]] = Array(Edge(2,1,7), Edge(2,4,2), Edge(3,2,4), Edge(3,6,3), Edge(4,1,1), Edge(5,2,2), Edge(5,3,8), Edge(5,6,3))
