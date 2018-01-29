### Scala Classes

**Classes in Scala **are blueprints for creating objects. They can contain methods, values, variables, types, objects, traits, and classes** **which are collectively called members.

Let us create a sample class inside Employee.scala

```
class Employee(val firstName: String, val lastName: String)
```

We can compile the scala code using \_scalac filename \_which will create a class file.

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



