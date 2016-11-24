****Loading text files****

spark is spark context

    Loading a text file in Scala
    val input = spark.textFile("file:///home/holden/repos/spark/README.md")

    Loading a text file in Java
    JavaRDD<String> input = spark.textFile("file:///home/holden/repos/spark/README.md")


Multipart inputs in the form of a directory containing all of the parts can be handled in two ways. We can just use the same textFile method and pass it a directory and it will load all of the parts into our RDD.

If our files are small enough, then we can use the SparkContext.wholeTextFiles() method and get back a pair RDD where the key is the name of the input file.

wholeTextFiles() can be very useful when each file represents a certain time period’s data. If we had files representing sales data from different periods, we could easily compute the average for each period,

    Example Average value per file in Scala
    val input = sc.wholeTextFiles("file://home/holden/salesFiles")
    val result = input.mapValues 
    { y => val nums = y.split(" ").map(x => x.toDouble)  nums.sum / nums.size.toDouble   }

**Spark supports reading all the files in a given directory and doing wildcard expansion on the input (e.g., part-*.txt). This is useful since large datasets are often spread across multiple files**

    Save text file results
    result.saveAsTextFile(outputFile)


****Loading Json files****

Loading the data as a text file and then parsing the JSON data is an approach that we can use in all of the supported languages. This works assuming that you have one JSON record per row; if you have multiline JSON files, you will instead have to load the whole file and then parse each file.


    Loading JSON in Scala
    import com.fasterxml.jackson.module.scala.DefaultScalaModule
    import com.fasterxml.jackson.module.scala.experimental.ScalaObjectMapper
    import com.fasterxml.jackson.databind.ObjectMapper
    import com.fasterxml.jackson.databind.DeserializationFeature
    ...
    case class Person(name: String, lovesPandas: Boolean) // Must be a top-level clas
    // Parse it into a specific case class. We use flatMap to handle errors
    // by returning an empty list (None) if we encounter an issue and a
    // list with one element if everything is ok (Some(_)).
    val result = input.flatMap(record => {
    try {
    Some(mapper.readValue(record, classOf[Person]))
    } catch {
    case e: Exception => None
    }})



    Example Loading JSON in Java
    class ParseJson implements FlatMapFunction<Iterator<String>, Person> {
    public Iterable<Person> call(Iterator<String> lines) throws Exception {
    ArrayList<Person> people = new ArrayList<Person>();
    ObjectMapper mapper = new ObjectMapper();
    while (lines.hasNext()) {
    String line = lines.next();
    try {
    people.add(mapper.readValue(line, Person.class));
    } catch (Exception e) {
    // skip records on failure
    }
    }
    return people;
    }
    }

    JavaRDD<String> input = sc.textFile("file.json");
    JavaRDD<Person> result = input.mapPartitions(new ParseJson());






    Saving JSON in Scala
    result.filter(p => P.lovesPandas).map(mapper.writeValueAsString(_)).saveAsTextFile(outputFile)




    Example Saving JSON in Java
    class WriteJson implements FlatMapFunction<Iterator<Person>, String> {
    public Iterable<String> call(Iterator<Person> people) throws Exception {
    ArrayList<String> text = new ArrayList<String>();
    ObjectMapper mapper = new ObjectMapper();
      while (people.hasNext()) {
      Person person = people.next();
      text.add(mapper.writeValueAsString(person));
     }
     return text;
     }
    }
    
    JavaRDD<Person> result = input.mapPartitions(new ParseJson()).filter(new LikesPandas());
    JavaRDD<String> formatted = result.mapPartitions(new WriteJson());
    formatted.saveAsTextFile(outfile);

