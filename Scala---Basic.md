Object − Objects have states and behaviors. An object is an instance of a class. Example − A dog has states - color, name, breed as well as behaviors - wagging, barking, and eating.

* Class − A class can be defined as a template/blueprint that describes the behaviors/states that are related to the class.

* Methods − A method is basically a behavior. A class can contain many methods. It is in methods where the logics are written, data is manipulated and all the actions are executed.

* Fields − Each object has its unique set of instance variables, which are called fields. An object's state is created by the values assigned to these fields.

* Closure − A closure is a function, whose return value depends on the value of one or more variables declared outside this function.

* Traits − A trait encapsulates method and field definitions, which can then be reused by mixing them into classes. Traits are used to define object types by specifying the signature of the supported methods.

* We can execute a Scala program in two modes: one is ****interactive mode and another is script mode****.

****Interactive Mode****

       \>scala
       scala> println("Hello, Scala!");


****Script Mode****

         object HelloWorld {
             /* This is my first java program.  
              * This will print 'Hello World' as the output
              */
              def main(args: Array[String]) {
                println("Hello, world!") // prints Hello World
             }
          }

Save the file as − HelloWorld.scala

      \> scalac HelloWorld.scala
      \> scala HelloWorld


* Case Sensitivity − Scala is case-sensitive, which means identifier Hello and hello would have different meaning in Scala.

* Class Names − For all class names, the first letter should be in Upper Case. If several words are used to form a name of the class, each inner word's first letter should be in Upper Case.

       Example − class MyFirstScalaClass.

* Method Names − All method names should start with a Lower Case letter. If multiple words are used to form the name of the method, then each inner word's first letter should be in Upper Case.

       Example − def myMethodName()

* Program File Name − Name of the program file should exactly match the object name. When saving the file you should save it using the object name (Remember Scala is case-sensitive) and append ‘.scala’ to the end of the name. (If the file name and the object name do not match your program will not compile).

      Example − Assume 'HelloWorld' is the object name. Then the file should be saved as 'HelloWorld.scala'.

* def main(args: Array[String]) − Scala program processing starts from the main() method which is a mandatory part of every Scala Program.

**Alphanumeric Identifiers**
An alphanumeric identifier starts with a letter or an underscore, which can be followed by further letters, digits, or underscores. The '$' character is a reserved keyword in Scala and should not be used in identifiers.

Following are legal alphanumeric identifiers −

               age, salary, _value,  __1_value

* Scala Packages
A package is a named module of code. For example, the Lift utility package is net.liftweb.util. The package declaration is the first non-comment line in the source file as follows −

         package com.liftcode.stuff

Scala packages can be imported so that they can be referenced in the current compilation scope. The following statement imports the contents of the scala.xml package −

        import scala.xml._

You can import a single class and object, for example, HashMap from the scala.collection.mutable package −

        import scala.collection.mutable.HashMap

You can import more than one class or object from a single package, for example, TreeMap and TreeSet from the 
 
       scala.collection.immutable package −

       import scala.collection.immutable.{TreeMap, TreeSet}


****What is the difference between a var and val definition in Scala?****

As so many others have said, the object assigned to a val cannot be replaced, and the object assigned to a var can. However, said object can have its internal state modified. For example:

     class A(n: Int) {
       var value = n
     }

     class B(n: Int) {
       val value = new A(n)
     }

         object Test {
            def main(args: Array[String]) {
                val x = new B(5)
                 x = new B(6) // Doesn't work, because I can't replace the object created on the line above with this new one.
                x.value = new A(6) // Doesn't work, because I can't replace the object assigned to B.value for a new one.
               x.value.value = 6 // Works, because A.value can receive a new object.
             }
           }
So, even though we can't change the object assigned to x, we could change the state of that object. At the root of it, however, there was a var.

Now, immutability is a good thing for many reasons. First, if an object doesn't change internal state, you don't have to worry if some other part of your code is changing it. For example:

          x = new B(0)
          f(x)
          if (x.value.value == 0)
          println("f didn't do anything to x")
         else
         println("f did something to x")

This becomes particularly important with multithreaded systems. In a multithreaded system, the following can happen:

       x = new B(1)
       f(x)
       if (x.value.value == 1) {
        print(x.value.value) // Can be different than 1!
        }

If you use val exclusively, and only use immutable data structures (that is, avoid arrays, everything in  scala.collection.mutable, etc.), you can rest assured this won't happen. That is, unless there's some code, perhaps even a framework, doing reflection tricks -- reflection can change "immutable" values, unfortunately.

That's one reason, but there is another reason for it. When you use var, you can be tempted into reusing the same var for multiple purposes. This has some problems:

It will be more difficult for people reading the code to know what is the value of a variable in a certain part of the code.
You may forget to re-initialize the variable in some code path, and end up passing wrong values downstream in the code.
Simply put, using val is safer and leads to more readable code.

We can, then, go the other direction. If val is that better, why have var at all? Well, some languages did take that route, but there are situations in which mutability improves performance, a lot.

For example, take an immutable Queue. When you either enqueue or dequeue things in it, you get a new Queue object. How then, would you go about processing all items in it?

I'll go through that with an example. Let's say you have a queue of digits, and you want to compose a number out of them. For example, if I have a queue with 2, 1, 3, in that order, I want to get back the number 213. Let's first solve it with a mutable.Queue:

        def toNum(q: scala.collection.mutable.Queue[Int]) = {
            var num = 0
            while (!q.isEmpty) {
               num *= 10
               num += q.dequeue
             }
            num
      }

This code is fast and easy to understand. Its main drawback is that the queue that is passed is modified by toNum, so you have to make a copy of it beforehand. That's the kind of object management that immutability makes you free from.

Now, let's covert it to an immutable.Queue:

          def toNum(q: scala.collection.immutable.Queue[Int]) = {
            def recurse(qr: scala.collection.immutable.Queue[Int], num: Int): Int = {
           if (qr.isEmpty)
             num
            else {
              val (digit, newQ) = qr.dequeue
              recurse(newQ, num * 10 + digit)
          }
           }
         recurse(q, 0)
      }

Because I can't reuse some variable to keep track of my num, like in the previous example, I need to resort to recursion. In this case, it is a tail-recursion, which has pretty good performance. But that is not always the case: sometimes there is just no good (readable, simple) tail recursion solution.

Note, however, that I can rewrite that code to use an immutable.Queue and a var at the same time! For example:

        def toNum(q: scala.collection.immutable.Queue[Int]) = {
          var qr = q
          var num = 0
           while (!qr.isEmpty) {
           val (digit, newQ) = qr.dequeue
           num *= 10
           num += digit
           qr = newQ
          }
          num
        }

This code is still efficient, does not require recursion, and you don't need to worry whether you have to make a copy of your queue or not before calling toNum. Naturally, I avoided reusing variables for other purposes, and no code outside this function sees them, so I don't need to worry about their values changing from one line to the next -- except when I explicitly do so.

Scala opted to let the programmer do that, if the programmer deemed it to be the best solution. Other languages have chosen to make such code difficult. The price Scala (and any language with widespread mutability) pays is that the compiler doesn't have as much leeway in optimizing the code as it could otherwise. Java's answer to that is optimizing the code based on the run-time profile. We could go on and on about pros and cons to each side.

Personally, I think Scala strikes the right balance, for now. It is not perfect, by far. I think both Clojure and Haskell have very interesting notions not adopted by Scala, but Scala has its own strengths as well. We'll see what comes up on the future.



