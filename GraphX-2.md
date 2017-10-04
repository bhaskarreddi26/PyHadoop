![](https://cdn.edureka.co/blog/wp-content/uploads/2017/05/GraphX-Example-Spark-GraphX-Tutorial-Edureka.png) (edeurka example)

Looking at the graph, we can extract information about the people (vertices) and the relations between them (edges). The graph here represents the Twitter users and whom they follow on Twitter. For e.g. Bob follows Davide and Alice on Twitter.

     import org.apache.spark._
     import org.apache.spark.rdd.RDD
     import org.apache.spark.util.IntParam
     import org.apache.spark.graphx._
     import org.apache.spark.graphx.Edge
     import org.apache.spark.graphx.util.GraphGenerators



      val vertexArray = Array(
      (1L, ("Alice", 28)),
      (2L, ("Bob", 27)),
      (3L, ("Charlie", 65)),
      (4L, ("David", 42)),
      (5L, ("Ed", 55)),
      (6L, ("Fran", 50)))

     val edgeArray = Array(
      Edge(2L, 1L, 7),
      Edge(2L, 4L, 2),
      Edge(3L, 2L, 4),
      Edge(3L, 6L, 3),
      Edge(4L, 1L, 1),
      Edge(5L, 2L, 2),
      Edge(5L, 3L, 8),
      Edge(5L, 6L, 3))

    var vertexRDD: RDD[(Long, (String, Int))] = sc.parallelize(vertexArray)

    var edgeRDD: RDD[Edge[Int]] = sc.parallelize(edgeArray)

    var graph: Graph[(String, Int), Int] = Graph(vertexRDD, edgeRDD)


       graph.vertices.filter { case (id, (name, age)) => age > 30 }
             .collect.foreach { case (id, (name, age)) => println(s"$name is $age")}