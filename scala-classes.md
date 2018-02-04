### Scala Classes

**Classes in Scala **are blueprints for creating objects. They can contain methods, values, variables, types, objects, traits, and classes** **which are collectively called members.

Let us create a sample class inside Employee.scala

```
class Employee(val firstName: String, val lastName: String)
```

We can compile the scala code using `scalac filename` which will create a class file.

![](/assets/class_compilation.png)

To examine the byte code use javap command. In javap -p refers to private which shows all classes and members.

![](/assets/javap_class.png)

Create a file EmployeeScript.scala with the below code

```
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

```
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName: String, @BeanProperty var lastName: String)
```

![](/assets/getters_and_setters.png)

#### Constructors

##### Scala Default Primary Constructor

In scala, if you don't specify primary constructor, compiler creates a constructor which is known as default primary constructor.

```
class Employee {
        println("Default Primary Constructor")
}
```

![](/assets/ScalaDefaultPrimaryConstructor.png)

##### Scala Primary Constructor

Scala provides a concept of primary constructor with the definition of class. You don't need to define explicitly constructor if your code has only one constructor. It helps to optimize code. You can create primary constructor with zero or more parameters.

```
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

```
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

