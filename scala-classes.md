### Scala Classes

**Classes in Scala **are blueprints for creating objects. They can contain methods, values, variables, types, objects, traits, and classes** **which are collectively called members.

Let us create a sample class inside Employee.scala

```scala
class Employee(val firstName: String, val lastName: String)
```

We can compile the scala code using `scalac filename` which will create a class file.

![](/assets/class_compilation.png)

To examine the byte code use javap command. In javap -p refers to private which shows all classes and members.

![](/assets/javap_class.png)

Create a file EmployeeScript.scala with the below code

```scala
val test = new Employee("First Name", "Last Name")
println(test.firstName)
println(test.lastName)
```

Run the EmployeeScript.scala with the class path as current directory

![](/assets/class_output.png)

* val creates accessors, access to the inner state
* var creates mutators, allowing change to inner state

#### Java Getters and Setters

* Use @scala.beans.BeanProperty
* Apply BeanProperty annotation to the property
* If applied to a val, BeanProperty will create a getter
* If applied to a var, BeanProperty will create a getter and setter

Create a script EmployeeGettersandSetters.scala

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String, @BeanProperty var lastName: String)
```

![](/assets/getters_and_setters.png)

#### Constructors

##### Scala Default Primary Constructor

In scala, if you don't specify primary constructor, compiler creates a constructor which is known as default primary constructor.

```scala
class Employee {
        println("Default Primary Constructor")
}
```

![](/assets/ScalaDefaultPrimaryConstructor.png)

##### Scala Primary Constructor

Scala provides a concept of primary constructor with the definition of class. You don't need to define explicitly constructor if your code has only one constructor. It helps to optimize code. You can create primary constructor with zero or more parameters.

```scala
class Employee(val firstName: String, val lastName: String) {
    def showDetails() = println(firstName + " " + lastName)
}

object MainObject {
    def main(args:Array[String]) {
        val test = new Employee("Martin", "Odersky")
        test.showDetails()
    }
}
```

![](/assets/Scala_Primary_Constructor.png)

![](/assets/Scala_Primary_Constructor_output.png)

##### Scala Secondary \(Auxiliary\) Constructor

You can create any number of auxiliary constructors in a class. You must call primary constructor from inside the auxiliary constructor. `this` keyword is used to call constructor from other constructor. When calling other constructor **make it first line** in your constructor.

```scala
class Employee(val firstName: String, val lastName: String) {
        var age: Int = 0
        def showDetails() = println(firstName + " " + lastName + " " + age)

        // Auxiliary Constructor
        def this(firstName: String, lastName: String, age: Int) = { this(firstName, lastName); this.age = age }
}

object MainObject {
        def main(args:Array[String]) {
                val test = new Employee("Martin", "Odersky", 59)
                test.showDetails()
        }
}
```

![](/assets/Scala_Auxiliary_Constructor.png)

![](/assets/Scala_Auxiliary_Constructor_output.png)

#### Constructor Named and Default Arguments

* Named arguments allow calls by constructor parameter name
* Named arguments allow calls in any order
* Default arguments allows to specify default values in the constructor declaration

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer" /* Default Argument */ ) {

        def showDetails() = { println(s"FirstName: $firstName LastName: $lastName Title: $title") }
}

object MainObject {
        def main(args:Array[String]) {
                val test = new Employee(lastName="Odersky", firstName="Martin") // Named Arguments
                test.showDetails()

                val test_title = new Employee("Dennis", title="Developer", lastName="Ritchie")
                test_title.showDetails()
        }
}
```

![](/assets/Constructor_Default_and_Named_Arguments_output.png)

#### Methods in Classes

* Methods are used in classes and have access to internal state
* Methods can also use default and named parameters for added functionality

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer") {

def showDetails() = { println(s"FirstName: $firstName LastName: $lastName Title: $title") }

def copy(firstName: String = this.firstName,
         lastName: String = this.lastName,
         title: String = this.title) = new Employee(firstName, lastName, title)

}

object MainObject {
        def main(args:Array[String]) {
                val test = new Employee(lastName="Odersky", firstName="Martin")
                test.showDetails

                val newTest = test.copy(title = "Developer")
                newTest.showDetails
        }
}
```

![](/assets/Methods_in_Classes_output.png)

#### Pre conditions, Exception and Exception Handling

Scala provides four set of pre-conditions- assert, assume, require, ensuring

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer") {

        require(firstName.nonEmpty, "First Name cannot be empty")
        require(lastName.nonEmpty, "Last Name cannot be empty")
        require(title.nonEmpty, "Title cannot be empty")

        def showDetails() = { println(s"FirstName: $firstName LastName: $lastName Title: $title") }
}

object MainObject {
        def main(args:Array[String]) {
                val test1 = new Employee(lastName="Odersky", firstName="Martin")
                test1.showDetails

                val test2 = new Employee("", "", "")
                test2.showDetails
        }
}
```

Here `test2` contains empty value for firstName, lastName and title. Running the above code will result in **IllegalArgumentException**![](/assets/preconditions_require_output.png)

We can handle the exception using `try catch` block.

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer") {

        require(firstName.nonEmpty, "First Name cannot be empty")
        require(lastName.nonEmpty, "Last Name cannot be empty")
        require(title.nonEmpty, "Title cannot be empty")

        if(title.contains("Senior") || title.contains("Junior"))
                throw new IllegalArgumentException("Title cannot contain Junior or Senior")

        def showDetails() = { println(s"FirstName: $firstName LastName: $lastName Title: $title") }
}

object MainObject {
        def main(args:Array[String]) {
                val test1 = new Employee(lastName="Odersky", firstName="Martin")
                test1.showDetails

                try {
                        val test2 = new Employee("Dennis", "Ritchie", "Senior Programmer")
                }
                catch {
                        case iae:IllegalArgumentException => println(iae.getMessage)
                }
                finally {
                        println("Inside finally block")
                }
        }
}
```

![](/assets/Exception_Handling_Output.png)

#### Subclasses

* `extends` is a keyword used to subclass a class from another class
* Inheritance must have "is-a" relationship
* We can have multiple classes in a single file

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer") {
}

class Department(val name: String)

class Manager(firstName: String, lastName: String, title: String, val department: Department) extends Employee(firstName, lastName, title)


object MainObject {
        def main(args:Array[String]) {
                val mathematics = new Department("Mathematics")
                val test_manager = new Manager("Alan", "Turing", "Mathematician", mathematics)

                println(test_manager.department.name)
        }
}
```

![](/assets/subclasses_output.png)

#### Method Overriding

* `override` keyword is mandatory
* Overridden methods must look the same as superclass method it is overriding
* Overridden methods are created to change the implementation of the superclass's methods
* Regardless of reference, correct method will be called

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer") {

        def fullName = s"$firstName $lastName"
}

class Department(val name: String)

class Manager(firstName: String, lastName: String, title: String, val department: Department) extends
      Employee(firstName, lastName, title) {
        override def fullName = s"$firstName $lastName ${department.name}" // Overridden Method
}

object MainObject {
        def main(args:Array[String]) {
                val mathematics = new Department("Mathematics")
                val test_manager:Manager = new Manager("Alan", "Turing", "Mathematician", mathematics)
                println(test_manager.fullName)

                val test_employee:Employee = test_manager
                println(test_employee.fullName)
        }
}
```

![](/assets/Method_Overriding_Output.png)

#### equals, toString, hashCode

* `equals` test for object equality
* Instead of calling `equals` you can call `==`
* `eq` is used to test if two objects are pointed to the same object
* `hashCode` is a near unique 32-bit integer that represents the object and used in `HashMap`, `HashSet`
* `toString` is a `String` representation of the object.

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String,
               @BeanProperty val lastName: String,
               val title: String = "Programmer") {

    override def equals(x:Any):Boolean = {
        if(!x.isInstanceOf[Employee]) false
        else {
            val other = x.asInstanceOf[Employee]
            other.firstName == this.firstName &&
            other.lastName == this.lastName &&
            other.title == this.title
        }
    }

    override def hashCode:Int = {
        var result = 19
        result = 31 * result + firstName.hashCode
        result = 31 * result + lastName.hashCode
        result = 31 * result + title.hashCode
        result
    }

    override def toString = s"Employee($firstName, $lastName, $title)"
}

object MainObject {
        def main(args:Array[String]) {
        val test = new Employee("Dennis", "Ritchie", "Programmer")
        val test1 = new Employee("Dennis", "Ritchie", "Programmer")
        val test2 = test1

        println(test == test1) // true
        println(test1 == test2) // true
        println(test eq test1) // false
        println(test1 eq test2) // true
        println(test.hashCode == test1.hashCode) // true
        println(test1.hashCode == test2.hashCode) // true
        println(test2) // by default println uses toString
        }
}
```

![](/assets/equals_output.png)

#### Case Classes

* Placing `case` keyword in front of class makes it a case class
* Case class have an automatic `equals`, `hashCode` and `toString`

How does a case class differ from normal class?

* You can do pattern matching on it
* You can construct instances of these classes without using the`new`keyword
* All constructor arguments are accessible from outside using automatically generated accessor functions
* The`toString`method is automatically redefined to print the name of the case class and all its arguments
* The`equals`method is automatically redefined to compare two instances of the same case class structurally rather than by identity.
* The`hashCode`method is automatically redefined to use the`hashCode`of constructor arguments.

```scala
case class Department(name: String) {
    override def toString = s"Department: $name"
}

object MainObject {
        def main(args:Array[String]) {
        val toys = Department("Toys") // For case classes no need to use new keyword
        val toys1 = Department("Toys")
        println(toys == toys1)
        println(toys.hashCode == toys1.hashCode)
        println(toys)
        }
}
```

![](/assets/case_classes_output.png)

#### Abstract Classes

* Abstract classes cannot be instantiated
* Abstract classes have zero or more abstract methods
* Abstract methods don't have implementations

```scala
import scala.beans.BeanProperty

abstract class Person {
    def firstName:String // Abstract method
    def lastName: String // Abstract method
}

class Employee(@BeanProperty val firstName: String,
           @BeanProperty val lastName: String,
    val title: String = "Programmer") extends Person {
    def fullName = s"$firstName $lastName"
}

object MainObject {
    def main(args:Array[String]) {
        val test = new Employee("Alan", "Turing", "Mathematician")
        println(test.fullName)
    }
}
```

![](/assets/abstract_class_output.png)

Here in Employee class abstract methods `firstName` and `lastName` are defined by default since we have used `val` for the property.

![](/assets/AbstractClass_Methods.png)

#### Parameterized Types on Classes

* Paramterized types uses square brackets just like in methods
* Parameterized types are managed by the type system

```scala
case class Box[T](t:T)

object MainObject {
    def main(args:Array[String]) {
        val res1 = Box(1)
        val res2:Box[Int] = Box(10)
        val res3:Int = res2.t
        val res4 = Box("Hello")
        val res5 = Box(Box(4.0))
        val res6:Double = res5.t.t

        println(s"res1: $res1\nres2: $res2\nres3: $res3\nres4: $res4\nres5: $res5\nres6: $res6")
    }
}
```

![](/assets/parameterized_types_classes_output_1.png)

Below is an example with two different types.

```scala
case class Couple[A, B](first: A, second: B)

object MainObject {
    def main(args:Array[String]) {
        val res1 = Couple(10, "Scala")
        val res2:Couple[Int, String] = Couple(10, "Scala")
        val res3 = Couple("One", "Two")
        val res4 = Couple("Hello", Couple(1, 10.0)) // Couple[String, Couple[Int, Double]]
        val res5 = res4.second.second

        println(s"res1: $res1\nres2: $res2\nres3: $res3\nres4: $res4\nres5: $res5")
    }
}
```

![](/assets/parameterized_types_classes_output_2.png)

#### Parameterized Methods in Classes

* Parameterized methods can be used in conjunction with Parameterized classes
* If a type is known at the class level, then it does not need to be declared at the method level

```scala
case class Couple[A, B](first: A, second: B) {
	def swap:Couple[B, A] = Couple(second, first)
}

case class Box[T](t:T) {
	def coupleWith[U](u:U):Box[Couple[T, U]] = Box(Couple(t, u))
}

object MainObject {
	def main(args:Array[String]) {
		val res1 = Box(200)
		val res2:Box[Couple[Int, String]] = res1.coupleWith("Scala")
		val res3 = res2.t.first
		val res4 = res2.t.second
		val res5 = Couple("One", 100.0)
		val res6 = res5.swap
		
		println(s"res1: $res1\nres2: $res2\nres3: $res3\nres4: $res4\nres5: $res5\nres6: $res6")
	}
}
```

![](/assets/parameterized_methods_classes_output.png)





