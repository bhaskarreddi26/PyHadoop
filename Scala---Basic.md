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

Scala Keywords
The following list shows the reserved words in Scala. These reserved words may not be used as constant or variable or any other identifier names.

**abstract	case	catch	class**
def	do	else	extends
false	final	finally	for
forSome	if	implicit	import
lazy	match	new	Null
object	override	package	private
protected	return	sealed	super
this	throw	trait	Try
true	type	val	Var
while	with	yield	 
-	:	=	=>
<-	<:	<%	>:
#	@		
