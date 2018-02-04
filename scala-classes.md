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

* extends is a keyword used to subclass a class from another class
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



