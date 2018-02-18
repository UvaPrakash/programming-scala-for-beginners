### Scala Options

`Option[T]` can be either **`Some[T]` **or **`None`**

object, which represents a missing value.

* Scala programmers don't like `null`
* `Options` are modelled as `Some` or `None`
* `Some` contains answer to be extracted
* Extracting the answer can be done by calling `get`, `getOrElse`, pattern matching or functions
* Scala still uses `null` to inter-operate with Java

`getOrElse()` method is used to access a value or a default when no value is present.

```scala
class Employee(val firstName: String, val middleName: Option[String], val lastName: String) {
	def this(firstName: String, middleName: String, lastName: String) =
		this(firstName, Some(middleName), lastName)

	def this(firstName: String, lastName: String) =
		this(firstName, None, lastName)

	def this() = this("Unknown", "Unknown")
}

object Options extends App {
	val middleName = Some("ABC")
	val middleName2:Option[String] = middleName
	val middleName3:Some[String] = middleName

	val noMiddleName = None
	val noMiddleName2:Option[String] = noMiddleName
	val noMiddleName3:Option[Nothing] = noMiddleName
	val noMiddleName4:None.type = noMiddleName

	val emp1 = new Employee("AAA", "BBB", "CCC")
	val emp2 = new Employee("XXX", "ZZZ")
	val emp3 = new Employee

	def getMiddleName(x: Option[String]):String = {
		x match {
			case Some(name) => name
			case None => "No middle name"
		}
	}
	
	println(middleName.getOrElse("No Middle Name")) // ABC
	println(noMiddleName.getOrElse("No Middle Name")) // No Middle Name

	println(getMiddleName(emp1.middleName)) // BBB
	println(getMiddleName(emp2.middleName)) // No middle name
	println(getMiddleName(emp3.middleName)) // No middle name
}
```

![](/assets/Options_output.png)

isEmpty\(\) is used to check if the option is `None` or not.

```scala
object Demo {
   def main(args: Array[String]) {
      val a:Option[Int] = Some(5)
      val b:Option[Int] = None 
      
      println("a.isEmpty: " + a.isEmpty) // false
      println("b.isEmpty: " + b.isEmpty) // true
   }
}
```

![](/assets/Options_2.png)

