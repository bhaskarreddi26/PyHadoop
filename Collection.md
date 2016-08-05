 curated list of awesome Java frameworks, libraries and software.

Awesome Java
Ancients
Bean Mapping
Build
Bytecode Manipulation
Cluster Management
Code Analysis
Code Coverage
Command-line Argument Parsers
Compiler-compiler
Configuration
Constraint Satisfaction Problem Solver
Continuous Integration
CSV
Data structures
Database
Date and Time
Dependency Injection
Development
Distributed Applications
Distributed Databases
Distribution
Document Processing
Formal Verification
Functional Programming
Game Development
Geospatial
GUI
High Performance
IDE
Imagery
JSON Processing
JSON
JVM and JDK
Logging
Machine Learning
Messaging
Miscellaneous
Monitoring
Native
Natural Language Processing
Networking
ORM
Performance analysis
PDF
Reactive libraries
REST Frameworks
Science
Search
Security
Serialization
Server
Template Engine
Testing
Utility
Web Crawling
Web Frameworks
Resources
Communities
Influential Books
Podcasts
Twitter
Websites
Contributing
Ancients

In existence since the beginning of time and which will continue being used long after the hype has waned.

Apache Ant - Build process management with XML.
cglib - Bytecode generation library. ★ 641, pushed 22 days ago
GlassFish - Application server and reference implementation for Java EE sponsored by Oracle.
Hudson - Continuous integration server still in active development.
JavaServer Faces - Oracle's open-source implementation of the JSF standard, Mojarra.
JavaServer Pages - Common templating for websites with custom tag libraries.
Bean Mapping

Frameworks that ease bean mapping.

Dozer - Mapper that copies data from one object to another, using annotations, API or XML configuration.
MapStruct - Code generator which simplifies mappings between different bean types, based on a convention over configuration approach. ★ 350, pushed 21 days ago
ModelMapper - ModelMapper is an intelligent object mapping library that automatically maps objects to each other. ★ 348, pushed 7 days ago
Orika - Orika is a Java Bean mapping framework that recursively copies (among other capabilities) data from one object to another.
Selma - Stupid Simple Statically Linked Mapper. Selma is an Annotation Processor Based bean mapper. ★ 41, pushed 14 days ago
Build

Tools which handle the build cycle and dependencies of an application.

Apache Maven - Declarative build and dependency management which favors convention over configuration. It might be preferable to Apache Ant which uses a rather procedural approach and can be difficult to maintain.
Bazel - Build tool from Google that builds code quickly and reliably.
Gradle - Incremental builds which are programmed via Groovy instead of declaring XML. Works well with Maven's dependency management.
Bytecode Manipulation

Libraries to manipulate bytecode programmatically.

ASM - All purpose, low level, bytecode manipulation and analysis.
Byte Buddy - Further simplifies bytecode generation with a fluent API.
Byteman - Manipulate bytecode at runtime via DSL (rules) mainly for testing/troubleshooting.
Javassist - Tries to simplify the editing of bytecode.
Cluster Management

Frameworks which can dynamically manage applications inside of a cluster.

Apache Aurora - Apache Aurora is a Mesos framework for long-running services and cron jobs.
Singularity - Singularity is a Mesos framework that makes deployment and operations easy. It supports web services, background workers, scheduled jobs, and one-off tasks.
Code Analysis

Tools that provide metrics and quality measurements.

Checkstyle - Static analysis of coding conventions and standards. ★ 1037, pushed 1 days ago
Codacy - Continuous static analysis, code coverage, and software metrics to automate code reviews.
Error Prone - Catches common programming mistakes as compile-time errors. ★ 917, pushed 6 days ago
FindBugs - Static analysis of bytecode to find potential bugs.
jQAssistant - Static code analysis with Neo4J-based query language.
PMD - Source code analysis for finding bad coding practices. ★ 487, pushed 1 days ago
SonarQube - Integrates other analysis components via plugins and provides an overview of the metrics over time.
Code Coverage

Frameworks and tools that enable collection of code coverage metrics for test suites.

Clover - Proprietary code coverage tool by Atlassian that relies on source-code instrumentation, instead of bytecode instrumentation.
Cobertura - Relies on offline (or static) bytecode instrumentation and class loading to collect code coverage metrics; GPLv2 licensed.
JaCoCo - Framework that enables collection of code coverage metrics, using both offline and runtime bytecode instrumentation; prominently used by EclEmma, the Eclipse code-coverage plugin.
JCov - Code coverage tool used in the OpenJDK project's development toolchain.
Command-line Argument Parsers

Libraries that make it easy to parse command line options, arguments, etc.

args4j - Small library to parse command like arguments similar to javac.
JCommander - Command line arguments parsing framework with custom types and validation via implementing interfaces.
JewelCLI - Uses annotations to automatically parse and inject the values with regex validation and Enum support.
JOpt Simple - Simple parser that uses the POSIX getopt() and GNU getopt_long() syntaxes. Does not use annotations, uses a fluent API instead.
Compiler-compiler

Frameworks that help to create parsers, interpreters or compilers.

ANTLR - Complex full-featured framework for top-down parsing.
JavaCC - More specific and slightly easier to learn. Has syntactic lookahead.
Configuration

Libraries that provide external configuration.

config - Configuration library for JVM languages. ★ 1925, pushed 27 days ago
owner - Reduces boilerplate of properties. ★ 356, pushed 78 days ago
Constraint Satisfaction Problem Solver

Libraries that help on implementing optimization and satisfiability problems.

Choco - Off-the-shelf constraint satisfaction problem solver, which uses constraint programming techniques.
JaCoP - Includes an interface for the FlatZinc language, enabling it to execute MiniZinc models.
OptaPlanner - Business planning and resource scheduling optimization solver.
Sat4J - State-of-the-art SAT solver for boolean and optimization problems.
Continuous Integration

Tools which support continuously building, testing and releasing applications.

Bamboo - Atlassian's solution with good integration of their other products. You can either apply for an open-source license or buy it.
CircleCI - Hosted service that offers a free plan for small needs. Open source projects are given a free bigger plan. Designed to integrate with GitHub.
Codeship - Hosted services with a limited free plan.
fabric8 - Integration platform for containers.
Go - ThoughtWork's open-source solution.
Jenkins - Provides server-based deployment services.
TeamCity - JetBrain's CI solution with a free version.
Travis - Hosted service often used for open-source projects.
CSV

Frameworks and libraries that simplify reading/writing CSV data.

opencsv - Simple CSV parser with a commercial-friendly license.
Super CSV - Powerful CSV parser with support for Dozer, Joda-Time and Java 8.
uniVocity-parsers - One of the fastest and most feature-complete CSV. Also comes with parsers for TSV and fixed width records. ★ 191, pushed 3 days ago
Database

Everything which simplifies interactions with the database.

Apache Hive - Data warehouse infrastructure built on top of Hadoop.
Apache Phoenix - High performance relational database layer over HBase for low latency applications.
Crate - Distributed data store that implements data synchronization, sharding, scaling, and replication. In addition, it provides a SQL-based syntax to execute queries across a cluster.
eXist - A NoSQL document database and application platform. ★ 124, pushed 2 days ago
FlexyPool - Brings metrics and failover strategies to the most common connection pooling solutions. ★ 178, pushed 120 days ago
Flyway - Simple database migration tool.
H2 - Small SQL Database notable for its in-memory functionality.
HikariCP - High performance JDBC connection pool. ★ 2652, pushed 3 days ago
JDBI - Convenient abstraction of JDBC.
Jedis - A small client for interaction with redis, with methods for commands. ★ 3576, pushed 1 days ago
jOOQ - Generates typesafe code based on SQL schema.
Liquibase - Database-independent library for tracking, managing and applying database schema changes.
MapDB - Embedded database engine that provides concurrent collections backed on disk or in off-heap memory.
Presto - Distributed SQL query engine for big data. ★ 4708, pushed 2 days ago
Querydsl - Typesafe unified queries.
Redisson - Allows for distributed and scalable data structures on top of a Redis server. ★ 1135, pushed 2 days ago
Speedment - A database access library that utilizes the Java 8 Stream API for querying. ★ 520, pushed 4 days ago
Vibur DBCP - JDBC connection pool library which offers advanced performance monitoring capabilities.
Data structures

Efficient and specific data structures.

Apache Avro - Data interchange format featuring among others: dynamic typing, untagged data, absence of manually assigned IDs.
Apache Orc - Fast and efficient columnar storage format for hadoop based workloads.
Apache Parquet - Columnar storage format based on assembly algorithms from the Dremel paper by Google.
Apache Thrift - Data interchange format that originated at Facebook.
Persistent Collection - Persistent and immutable analogue of the Java Collections Framework.
Protobuf - Google's data interchange format. ★ 8709, pushed 2 days ago
SBE - Simple Binary Encoding, one of the fastest message formats around. ★ 806, pushed 8 days ago
Wire - Clean, lightweight protocol buffers. ★ 1447, pushed 18 days ago
Date and Time

Libraries related to handling date and time.

Almanac Converter - Simple conversion between different calendar systems. ★ 6, pushed 69 days ago
Joda-Time - De facto standard date/time-library before Java 8.
ThreeTenBP - Port of JSR 310 (java.time package) by the author of Joda-Time. ★ 197, pushed 8 days ago
Time4J - Advanced date and time library. ★ 76, pushed 1 days ago
Dependency Injection

Libraries that help to realize the Inversion of Control paradigm.

Apache DeltaSpike - CDI extension framework.
Dagger2 - Compile-time injection framework without reflection.
Guice - Lightweight but powerful framework that completes Dagger. ★ 3221, pushed 57 days ago
HK2 - Light-weight and dynamic dependency injection framework.
Development

Augmentation of the development process at a fundamental level.

ADT4J - JSR-269 code generator for algebraic data types. ★ 71, pushed 6 days ago
AspectJ - Seamless aspect-oriented programming extension.
Auto - Collection of source code generators. ★ 2749, pushed 19 days ago
DCEVM - Modification of the JVM that allows unlimited redefinition of loaded classes at runtime.
HotswapAgent - Unlimited runtime class and resource redefinition. ★ 408, pushed 6 days ago
Immutables - Scala-like case classes.
JHipster - Yeoman source code generator to create applications based on Spring Boot and AngularJS. ★ 3989, pushed 2 days ago
JRebel - Commercial software that instantly reloads code and configuration changes without redeploys.
Lombok - Code-generator which aims to reduce the verbosity.
Spring Loaded - Class reloading agent. ★ 1149, pushed 22 days ago
Distributed Applications

Libraries and frameworks for writing distributed and fault-tolerant applications.

Akka - Toolkit and runtime for building concurrent, distributed, and fault tolerant event-driven applications.
Apache Storm - Realtime computation system.
Apache ZooKeeper - Coordination service with distributed configuration, synchronization, and naming registry for large distributed systems.
Axon Framework - Framework for creating CQRS applications.
Hazelcast - Highly scalable in-memory datagrid.
Hystrix - Provides latency and fault tolerance. ★ 5815, pushed 1 days ago
JGroups - Toolkit for reliable messaging and creating clusters.
Lagom - Framework for creating microservice-based systems.
Orbit - Virtual Actors, adding another level of abstraction to traditional actors.
Quasar - Lightweight threads and actors for the JVM.
Distributed Databases

Databases in a distributed system that appear to applications as a single data source.

Apache Cassandra - Column-oriented and providing high availability with no single point of failure.
Apache HBase - Hadoop database for big data.
Druid - Real-time and historical OLAP data store that excel at aggregation and approximation queries.
Infinispan - Highly concurrent key/value datastore used for caching.
OpenTSDB - Scalable and distributed time series database written on top of Apache HBase.
Distribution

Tools which handle the distribution of applications in native formats.

Bintray - Version control for binaries which handles the publishing. Can also be used with Maven or Gradle and has a free plan for open-source software or several business plans.
Boxfuse - Deployment of JVM application to AWS using the principles of Immutable Infrastructure.
Capsule - Simple and powerful packaging and deployment. A fat JAR on steroids or a "Docker for Java" that supports JVM-optimized containers.
Central Repository - Largest binary component repository available as a free service to the open-source community. Default used by Apache Maven and available in all other build tools.
IzPack - Setup authoring tool for cross-platform deployments.
JitPack - Easy to use package repository for GitHub. Builds Maven/Gradle projects on demand and publishes ready-to-use packages.
Launch4j - Wraps JARs in lightweight and native Windows executables.
Nexus - Binary management with proxy and caching capabilities.
packr - Packs JARs, assets and the JVM for native distribution on Windows, Linux and Mac OS X.
Document Processing

Libraries that assist with processing office document formats.

Apache POI - Supports OOXML (XLSX, DOCX, PPTX) as well as OLE2 (XLS, DOC or PPT).
documents4j - API for document format conversion using third-party converters such as MS Word.
jOpenDocument - Processes the OpenDocument format.
Formal Verification

Formal-methods tools: proof assistants, model checking, symbolic execution etc.

CATG - Concolic unit testing engine. Automatically generates unit tests using formal methods. ★ 31, pushed 187 days ago
Checker Framework - Pluggable type systems. Includes nullness types, physical units, immutability types and more.
Daikon - Daikon detects likely program invariants and can generate JML specs based on those invariats.
Java Modeling Language (JML) - Behavioral interface specification language that can be used to specify the behavior of code modules. It combines the design by contract approach of Eiffel and the model-based specification approach of the Larch family of interface specification languages, with some elements of the refinement calculus. Used by several other verification tools.
Java Path Finder (JPF) - JVM formal verification tool containing a model checker and more. Created by NASA.
jCUTE - Concolic unit testing engine that automatically generates unit tests. Concolic execution combines randomized concrete execution with symbolic execution and automatic constraint solving. ★ 23, pushed 670 days ago
JMLOK 2.0 - Detects nonconformances between code and JML specification through the feedback-directed random tests generation, and suggests a likely cause for each nonconformance detected.
KeY - The KeY System is a formal software development tool that aims to integrate design, implementation, formal specification, and formal verification of object-oriented software as seamlessly as possible. Uses JML for specification and symbolic execution for verification.
Krakatoa - Krakatoa is a front-end of the Why platform for deductive program verification. Krakatoa deals with Java programs annotated in a variant of the Java Modeling Language (JML).
OpenJML - Translates JML specifications into SMT-LIB format and passes the proof problems implied by the program to backend solvers.
Functional Programming

Libraries that facilitate functional programming.

cyclops-react - Monad and stream utilities, comprehensions, pattern matching, functional extensions for all JDK collections, future streams, trampolines and much more. ★ 389, pushed 11 days ago
derive4j - Java 8 annotation processor and framework for deriving algebraic data types constructors, pattern-matching, morphisms. ★ 110, pushed 75 days ago
Fugue - Functional extensions to Guava.
Functional Java - Implements numerous basic and advanced programming abstractions that assist composition-oriented development.
Javaslang - Functional component library that provides persistent data types and functional control structures.
jOOλ - Extension to Java 8 which aims to fix gaps in lambda, providing numerous missing types and a rich set of sequential Stream API additions. ★ 554, pushed 9 days ago
Game Development

Frameworks that support the development of games.

jMonkeyEngine - Game engine for modern 3D development.
libGDX - All-round cross-platform, high-level framework.
LWJGL - Robust framework that abstracts libraries like OpenGL/CL/AL.
Geospatial

Libraries for working with geospatial data and algorithms.

Apache SIS - Library for developing geospatial applications.
Geo - GeoHash utilities in Java.
Geotoolkit.org - Library for developing geospatial applications. Built on top of the Apache SIS project.
GeoTools - Library that provides tools for geospatial data.
H2GIS - A spatial extension of the H2 database.
Jgeohash - Library that can assist Java developers in using the GeoHash algorithm.
JTS Topology Suite - An API of 2D spatial predicates and functions.
Mapsforge - Software for the rendering of maps based on OpenStreetMap data.
Spatial4j - General purpose spatial/geospatial ASL licensed open-source Java library.
GUI

Libraries to create modern graphical user interfaces.

JavaFX - The successor of Swing.
Scene Builder - Visual layout tool for JavaFX applications.
SWT - The Standard Widget Toolkit (SWT) is a graphical widget toolkit for use with the Java platform.
High Performance

Everything about high performance computation, from collections to specific libraries.

Agrona - Data structures and utility methods that are common in high-performance applications. ★ 400, pushed 3 days ago
Disruptor - Inter-thread messaging library.
fastutil - Fast and compact type-specific collections.
GS Collections - Collection framework inspired by Smalltalk. ★ 1518, pushed 50 days ago
HPPC - Primitive collections.
Javolution - Library for real-time and embedded systems.
JCTools - Concurrency tools currently missing from the JDK. ★ 605, pushed 3 days ago
Koloboke - Hash sets and hash maps. ★ 466, pushed 9 days ago
Trove - Primitive collections.
IDE

Integrated development environments that try to simplify several aspects of development.

Eclipse - Established, open-souce project with support for lots of plugins and languages.
IntelliJ IDEA - Supports a lot of JVM languages and provides good options for Android development. The commercial edition targets the enterprise sector.
NetBeans - Provides integration for several Java SE and EE features from database access to HTML5.
Imagery

Libraries that assist with the creation, evaluation or manipulation of graphical images.

Imgscalr - Simple and efficient hardware-accelerated image-scaling library implemented in pure Java 2D. ★ 613, pushed 300 days ago
Picasso - Image downloading and caching library for Android.
Thumbnailator - Thumbnailator is a high-quality thumbnail generation library for Java. ★ 293, pushed 144 days ago
ZXing - Multi-format 1D/2D barcode image processing library. ★ 8675, pushed 9 days ago
JSON

Libraries for serializing and deserializing JSON to and from Java objects.

Genson - Powerful and easy to use Java to JSON conversion library.
Gson - Serializes objects to JSON and vice versa. Good performance with on-the-fly usage. ★ 4210, pushed 6 days ago
Jackson - Similar to GSON but has performance gains if you need to instantiate the library more often.
JSON-io - Convert Java to JSON. Convert JSON to Java. Pretty print JSON. Java JSON serializer. ★ 157, pushed 5 days ago
LoganSquare - JSON parsing and serializing library based on Jackson's streaming API. Outpeforms GSON & Jackson's library. ★ 2211, pushed 37 days ago
JSON Processing

Libraries for processing data in JSON format.

fastjson - Very fast processor with no additional dependencies and full data binding. ★ 4946, pushed 1 days ago
Jolt - JSON to JSON transformation tool. ★ 157, pushed 54 days ago
JsonPath - Extract data from JSON using XPATH like syntax. ★ 869, pushed 35 days ago
JsonSurfer - Streaming JsonPath processor dedicated to processing big and complicated JSON data. ★ 13, pushed 173 days ago
JVM and JDK

Current implementations of the JVM/JDK.

Avian - JVM with both a JIT & AOT modes. Includes an iOS port. ★ 716, pushed 5 days ago
JDK 9 - Early access releases of JDK 9.
OpenJDK - Open-source implementation for Linux.
ParparVM - VM with non-blocking concurrent GC for iOS.
Zulu OpenJDK 9 - Early access OpenJDK 9 builds for Windows, Linux, and Mac OS X.
Zulu OpenJDK - OpenJDK builds for Windows, Linux, and Mac OS X through Java 8.
Logging

Libraries that log the behavior of an application.

Apache Log4j 2 - Complete rewrite with a powerful plugin and configuration architecture.
graylog - Open-source aggregator suited for extended role and permission management.
kibana - Analyzes and visualizes log files. Some features require payment.
Logback - Robust logging library with interesting configuration options via Groovy.
logstash - Tool for managing log files.
SLF4J - Abstraction layer which is to be used with an implementation.
tinylog - Lightweight logging framework with static logger class.
Machine Learning

Tools that provide specific statistical algorithms which allow learning from data.

Apache Flink - Fast and reliable large-scale data processing engine.
Apache Hadoop - Storage and large-scale processing of data-sets on clusters of commodity hardware.
Apache Mahout - Scalable algorithms focused on collaborative filtering, clustering and classification.
Apache Spark - Data analytics cluster computing framework.
DeepDive - Creates structured information from unstructured data and integrates it into an existing database.
Deeplearning4j - Distributed and multi-threaded deep learning library.
H2O - Analytics engine for statistics over big data.
JSAT - Algorithms for pre-processing, classification, regression, and clustering with support for multi-threaded execution. ★ 149, pushed 5 days ago
Oryx 2 - A framework for building real-time large scale machine learning applications, which also includes end-to-end applications for collaborative filtering, classification, regression, and clustering. ★ 777, pushed 9 days ago
Smile - The Statistical Machine Intelligence and Learning Engine provides a set of machine learning algorithms and a visualization library.
Weka - Collection of algorithms for data mining tasks ranging from pre-processing to visualization.
Messaging

Tools that help to send messages between clients in order to ensure protocol independency.

Aeron - Efficient reliable unicast and multicast message transport. ★ 1743, pushed 8 days ago
Apache ActiveMQ - Message broker that implements JMS and converts synchronous to asynchronous communication.
Apache Camel - Glues together different transport APIs via Enterprise Integration Patterns.
Apache Kafka - High-throughput distributed messaging system.
Hermes - Fast and reliable message broker built on top of Kafka.
JBoss HornetQ - Clear, concise, modular and made to be embedded.
JeroMQ - Implementation of ZeroMQ. ★ 1011, pushed 29 days ago
Smack - Cross-platform XMPP client library.
Miscellaneous

Everything else.

Codename One - Cross platform solution for writing native mobile (iOS, Android, etc.)
Design Patterns - Implementation and explanation of the most common design patterns. ★ 11219, pushed 9 days ago
J2ObjC - Java to Objective-C translator for porting Android libraries to iOS. ★ 4055, pushed 5 days ago
jabba - Java Version Manager inspired by nvm. ★ 78, pushed 6 days ago
Jimfs - In-memory file system. ★ 957, pushed 32 days ago
Lanterna - Easy console text GUI library similar to curses. ★ 266, pushed 15 days ago
LightAdmin - Pluggable CRUD UI library for rapid application development.
Modern Java - A Guide to Java 8 - Popular Java 8 guide. ★ 5356, pushed 42 days ago
OpenRefine - Tool for working with messy data: cleaning, transforming, extending it with web services and linking it to databases.
Monitoring

Tools that monitor applications in production.

AppDynamics - Commercial performance monitor.
JavaMelody - Performance monitoring and profiling. ★ 356, pushed 3 days ago
jmxtrans - Tool to connect to multiple JVMs and to query them for their attributes via JMX. Its query language is based on JSON, which allows non-Java programmers to access the JVMs attributes. Likewise, this tool supports different output writes, including Graphite, Ganglia, StatsD, among others.
Jolokia - JMX over REST.
Kamon - Tool for monitoring applications running on the JVM.
Metrics - Expose metrics via JMX or HTTP and can send them to a database.
New Relic - Commercial performance monitor.
SPM - Commercial performance monitor with distributing transaction tracing for JVM apps.
Takipi - Commercial in-production error monitoring and debugging.
Native

For working with platform-specific native libraries.

JNA - Work with native libraries without writing JNI. Also provides interfaces to common system libraries. ★ 2273, pushed 4 days ago
JNR - Work with native libraries without writing JNI. Also provides interfaces to common system libraries. Same goals as JNA, but faster, and serves as the basis for the upcoming Project Panama . ★ 260, pushed 50 days ago
Natural Language Processing

Libraries that specialize on processing text.

Apache OpenNLP - Toolkit for common tasks like tokenization.
CoreNLP - Stanford's CoreNLP provides a set of fundamental tools for tasks like tagging, named entity recognition, sentiment analysis and many more.
LingPipe - Toolkit for a variety of tasks ranging from POS tagging to sentiment analysis.
Mallet - Statistical natural language processing, document classification, clustering, topic modeling and more.
Networking

Libraries for network programming.

Async Http Client - Asynchronous HTTP and WebSocket client library. ★ 2829, pushed 2 days ago
Comsat - Integrates standard Java web-related APIs with Quasar fibers and actors. ★ 292, pushed 7 days ago
Finagle - Extensible RPC system used to construct high-concurrency servers. It implements uniform client and server APIs for several protocols, and is protocol agnostic, which simplifies the implementation of new protocols. ★ 4567, pushed 2 days ago
Grizzly - NIO framework. Used as a network layer in Glassfish.
Netty - Framework for building high performance network applications.
Nifty - Implementation of Thrift clients and servers on Netty. ★ 496, pushed 48 days ago
OkHttp - HTTP+SPDY client.
Undertow - Web server providing both blocking and non-blocking API’s based on NIO. Used as a network layer in WildFly.
urnlib - Java library for representing, parsing and encoding URNs as in RFC 2141. ★ 1, pushed 38 days ago
ORM

APIs which handle the persistence of objects.

Ebean - Provides simple and fast data access.
EclipseLink - Supports a number of persistence standards: JPA, JAXB, JCA and SDO.
Hibernate - Robust and widely used with an active community.
MyBatis - Couples objects with stored procedures or SQL statements.
OrmLite - Lightweight package avoiding the complexity and overhead of other ORM products.
PDF

Everything that helps with the creation of PDF files.

Apache FOP - Creates PDF from XSL-FO.
Apache PDFBox - Toolbox for creating and manipulating PDF.
DynamicReports - Simplifies JasperReports.
flyingsaucer - XML/XHTML and CSS 2.1 renderer. ★ 640, pushed 21 days ago
iText - Creates PDF files programmatically but requires a license for commercial purposes.
JasperReports - Complex reporting engine.
Performance analysis

Tools for performance analysis, profiling and benchmarking.

honest-profiler - An low-overhead, bias-free sampling profiler. ★ 380, pushed 7 days ago
jHiccup - Logs and records platform JVM stalls. ★ 253, pushed 47 days ago
JMH - Microbenchmarking tool for the JVM.
JProfiler - Commercial profiler.
LatencyUtils - Utilities for latency measurement and reporting. ★ 229, pushed 140 days ago
VisualVM - Visual interface for detailed information about running applications.
XRebel - A commercial profiler for Java Web applications.
YourKit Java Profiler - Commercial profiler.
Reactive libraries

Libraries for developing reactive applications.

Reactive Streams - Provide a standard for asynchronous stream processing with non-blocking backpressure.
Reactor - Library for building reactive fast-data applications.
RxJava - Library for composing asynchronous and event-based programs using observable sequences from the JVM. ★ 13390, pushed 1 days ago
vert.x - Polyglot event-driven application framework.
REST Frameworks

Frameworks specifically for creating RESTful services.

Dropwizard - Opinionated framework for setting up modern web applications with Jetty, Jackson, Jersey and Metrics.
Feign - HTTP client binder inspired by Retrofit, JAXRS-2.0, and WebSocket. ★ 951, pushed 4 days ago
Jersey - JAX-RS reference implementation.
Microserver — A convenient extensible Microservices plugin system for Spring & Spring Boot, with over 30 plugins and growing, that supports both micro-monolith and pure microservices styles. ★ 484, pushed 4 days ago
RAML - Modeling language to generate REST APIs with contract first.
Rapidoid - A simple, secure and extremely fast framework consisting of embedded HTTP server, GUI components and dependency injection.
rest.li - Framework for building robust, scalable RESTful architectures using type-safe bindings and asynchronous, non-blocking IO with an end-to-end developer workflow that promotes clean practices, uniform interface design and consistent data modeling. ★ 1259, pushed 4 days ago
RESTEasy - Fully certified and portable implementation of the JAX-RS specification.
RestExpress - Thin wrapper on the JBoss Netty HTTP stack to provide scaling and performance. ★ 597, pushed 4 days ago
Restlet Framework - Pioneering framework with powerful routing and filtering capabilities, unified client and server API.
RestX - Framework based on annotation processing and compile-time source generation.
Retrofit - Type-safe REST client.
Spark - Sinatra inspired framework.
Swagger - Swagger is a specification and complete framework implementation for describing, producing, consuming, and visualizing RESTful web services.
Science

Libraries for scientific computing, analysis and visualization.

DataMelt - Environment for scientific computation, data analysis and data visualization.
JScience - Provides a set of classes to work with scientific measurements and units.
GraphStream - Library for modeling and analysis of dynamic graphs.
JGraphT - Graph library that provides mathematical graph-theory objects and algorithms. ★ 655, pushed 6 days ago
JGraphX - Library for visualisation (mainly Swing) and interaction with node-edge graphs. ★ 283, pushed 18 days ago
Search

Engines which index documents for search and analysis.

Apache Solr - Enterprise search engine optimized for high volume traffic.
Elasticsearch - Distributed, multitenant-capable full-text search engine with a RESTful web interface and schema-free JSON documents.
Security

Libraries that handle security, authentication, authorization or session management.

Apache Shiro - Performs authentication, authorization, cryptography and session management.
Bouncy Castle - All-purpose cryptographic library. JCA provider, wide range of functions from basic helpers to PGP/SMIME operations.
Cryptomator - Multiplatform transparent client-side encryption of files in the cloud.
Google Keyczar - Easy to use, yet safe encryption framework with key versioning. ★ 510, pushed 2 days ago
Keycloak - Integrated SSO and IDM for browser apps and RESTful web services.
PicketLink - Umbrella project for security and identity management.
Serialization

Libraries that handle serialization with high efficiency.

FlatBuffers - Memory efficient serialization library that can access serialized data without unpacking and parsing it. ★ 5366, pushed 2 days ago
FST - JDK compatible high performance object graph serialization. ★ 540, pushed 21 days ago
Kryo - Fast and efficient object graph serialization framework. ★ 1847, pushed 9 days ago
MessagePack - Efficient binary serialization format. ★ 573, pushed 6 days ago
Server

Servers which are specifically used to deploy applications.

Apache Tomcat - Robust all-round server for Servlet and JSP.
Apache TomEE - Tomcat plus Java EE.
Jetty - Lightweight, small server, often embedded in projects.
WebSphere Liberty - Lightweight, modular server developed by IBM.
WildFly - Formerly known as JBoss and developed by Red Hat with extensive Java EE support.
Template Engine

Tools which substitute expressions in a template.

Apache Velocity - Templates for HTML pages, emails or source code generation in general.
FreeMarker - General templating engine without any heavyweight or opinionated dependencies.
Handlebars.java - Logic-less and semantic Mustache templates.
Thymeleaf - Aims to be a substitute for JSP and works for XML files in general.
Testing

Tools that test from model to the view.

Apache JMeter - Functional testing and performance measurements.
Arquillian - Integration and functional testing platform for Java EE containers.
AssertJ - Fluent assertions that improve readability.
Awaitility - DSL for synchronizing asynchronous operations. ★ 291, pushed 23 days ago
Citrus - Integration testing framework with focus on client- and serverside messaging.
Cucumber - BDD testing framework. ★ 1254, pushed 3 days ago
Gatling - Load testing tool designed for ease of use, maintainability and high performance.
GreenMail - In-memory email server for integration testing. Supports SMTP, POP3 and IMAP including SSL.
Hamcrest - Matchers that can be combined to create flexible expressions of intent.
JGiven - Developer-friendly BDD testing framework compatible with JUnit and TestNG.
JMockit - Mocks static, final methods and more.
JUnit - Common testing framework.
junit-dataprovider - A TestNG like dataprovider runner for JUnit. ★ 81, pushed 21 days ago
JUnitParams - Creation of readable and maintainable parametrised tests.
Mockito - Creation of test double objects in automated unit tests for the purpose of TDD or BDD. ★ 2416, pushed 9 days ago
Moco - Concise web services for stubs and mocks, Duke's Choice Award 2013. ★ 1227, pushed 2 days ago
PIT - Fast mutation-testing framework for evaluating fault-detection abilities of existing JUnit or TestNG test-suites.
PowerMock - Enables mocking of static methods, constructors, final classes and methods, private methods and removal of static initializers. ★ 565, pushed 1 days ago
REST Assured - Java DSL for easy testing for REST/HTTP services. ★ 1075, pushed 3 days ago
Selenide - Concise API around Selenium to write stable and readable UI tests.
Selenium - Portable software testing framework for web applications.
Spock - JUnit-compatible framework featuring an expressive Groovy-derived specification language.
TestNG - Testing framework.
Truth - Google's assertion and proposition framework. ★ 609, pushed 8 days ago
Unitils - Modular testing library for unit and integration testing.
WireMock - Stubbs and mocks web services.
J8Spec - J8Spec is a library that allows tests written in Java to follow the BDD style introduced by RSpec and Jasmine.
Utility

Libraries which provide general utility functions.

Apache Commons - Provides different general purpose functions like configuration, validation, collections, file upload or XML processing.
CRaSH - Provides a shell into a JVM that's running CRaSH. Used by Spring Boot and others.
Gephi - Cross-platform for visualizing and manipulating large graph networks.
Dex - Java/JavaFX tool capable of powerful ETL and data visualization. ★ 46, pushed 3 days ago
Guava - Collections, caching, primitives support, concurrency libraries, common annotations, string processing, I/O, and so forth. ★ 8828, pushed 1 days ago
JADE - Framework and environment for building and to debugging multi-agent systems.
javatuples - Tuples.
JavaVerbalExpressions - A library that helps to construct difficult regular expressions. ★ 1161, pushed 28 days ago
Protégé - Provides an ontology editor and a framework to build knowledge-based systems.
Web Crawling

Libraries that analyze the content of websites.

Apache Nutch - Highly extensible, highly scalable web crawler for production environment.
Crawler4j - Simple and lightweight web crawler. ★ 980, pushed 4 days ago
JSoup - Scrapes, parses, manipulates and cleans HTML.
Web Frameworks

Frameworks that handle the communication between the layers of an web application.

Apache Tapestry - Component-oriented framework for creating dynamic, robust, highly scalable web applications.
Apache Wicket - Component-based web application framework similar to Tapestry with a stateful GUI.
Blade - Lightweight, modular framework which aims to be elegant and simple. ★ 1407, pushed 7 days ago
Google Web Toolkit - Toolbox which includes a Java-to-JavaScript compiler for client-side code, XML parser, API for RPC, JUnit integration, internationalization support and widgets for the GUI.
Grails - Groovy framework with the aim to provide a highly productive environment by favoring convention over configuration, no XML and support for mixins.
Ninja - Full stack web framework.
Pippo - Small, highly modularized Sinatra-like framework.
Play - Uses convention over configuration, hot code reloading and display of errors in the browser.
PrimeFaces - JSF framework which has a free and a commercial version with support. Provides several frontend components.
Ratpack - Set of libraries that facilitate fast, efficient, evolvable and well tested HTTP applications.
Spring Boot - Microframework which simplifies the development of new Spring applications.
Spring - Provides many packages ranging from dependency injection to aspect-oriented programming to security.
Vaadin - Event-driven framework build on top of GWT. Uses server-side architecture with Ajax on the client-side.
Resources

Communities

Active discussions.

r/java - Subreddit for the Java community.
stackoverflow - Question/answer platform.
vJUG - Virtual Java User Group.
Influential Books

Books that had a high impact and are still worth reading.

Effective Java (2nd Edition)
Java 8 in Action
Java Concurrency in Practice
Thinking in Java
Podcasts

Something to listen to while programming.

The Java Council
The Java Posse - Discontinued as of 02/2015.
Twitter

Active accounts to follow. Descriptions from Twitter.

Adam Bien - Freelancer: Author, JavaONE Rockstar Speaker, Consultant, Java Champion.
Aleksey Shipilëv - Performance Geek, Benchmarking Tzar, Concurrency Bug Hunter.
Antonio Goncalves - Java Champion, JUG Leader, Devoxx France, Java EE 6/7, JCP, Author.
Arun Gupta - Java Champion, JavaOne Rockstar, JUG Leader, Devoxx4Kids-er, VP of Developer Advocacy at Couchbase.
Brian Goetz - Java Language Architect at Oracle.
Bruno Borges - Product Manager/Java Jock at Oracle.
Ed Burns - Consulting Member of the Technical Staff at Oracle.
Eugen Paraschiv - Author of the Spring Security Course.
James Weaver - Java/JavaFX/IoT developer, author and speaker.
Java EE - Official Java EE Twitter account.
Java Magazine - Official Java Magazine account.
Java - Official Java Twitter account.
Javin Paul - Well-known Java blogger.
Lukas Eder - Founder and CEO Data Geekery (jOOQ).
Mario Fusco - RedHatter, JUG coordinator, frequent speaker and author.
Mark Reinhold - Chief Architect, Java Platform Group, Oracle.
Markus Eisele - Java EE evangelist, Red Hat.
Martijn Verburg - London JUG co-leader, speaker, author, Java Champion and much more.
Martin Thompson - Pasty faced performance gangster.
OpenJDK - Official OpenJDK account.
Peter Lawrey - Peter Lawrey, Java performance expert.
Reza Rahman - Java EE/GlassFish/WebLogic evangelist, author, speaker, open source hacker.
Simon Maple - Java Champion, virtualJUG founder, LJC leader, RebelLabs author.
Stephen Colebourne - Java Champion, speaker.
Trisha Gee - Java Champion and speaker.
Websites

Sites to read.

Android Arsenal
Google Java Style
InfoQ
Java, SQL, and jOOQ
Java Algorithms and Clients
Java.net
Javalobby
JavaWorld
JAXenter
RebelLabs
The Takipi Blog
TheServerSide.com
Vanilla Java
Voxxed