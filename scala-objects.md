### Scala Objects

#### Singleton Objects

Methods and values that aren’t associated with individual instances of a `class` belong in _singleton objects_, denoted by using the keyword `object` instead of `class`.

No object is required to call methods declared inside singleton object. Methods declared inside Singleton Object are accessible globally.

```scala
// Singleton Object
object MyObject {
        def add(x: Int, y: Int) = x + y
}

println(MyObject.add(2,4))
```

![](/assets/Singleton_Object.png)

#### Main method in scala

Main method is an entry method to a program. Below is an example of Java's main method.

```java
public class Sample {
    public static void main(String[] args) {
        System.out.println("Hello, this is Java main method");
    }
}
```

Let us create an equivalent version of the above main method in Scala

```scala
object Sample {
    def main(args: String[]):Unit = println("Hello, this is Scala main method")
}
```

* Objects are singletons
* Objects are Scala's replacement for the keyword `static`
* Objects are meant for factories, defining pattern matching, defining defaults and main methods
* Main methods are always inside of Objects
* You can forgo the main declaration by having your object extends `App`

#### Companion Objects

Most singleton objects do not stand alone, but instead are associated with a class of the same name.

In scala, when you have a class with same name as singleton object, it is called companion class and the singleton object is called companion object.

The companion class and its companion object both must be defined in the same source file.

```scala
class CompanionClass{  
    def hello(){  
        println("Hello, this is Companion Class.")  
    }  
}  
object CompanionObject{  
    def main(args:Array[String]){  
        new CompanionClass().hello()  
        println("Hello, this is Companion Object.")  
    }  
}
```

![](/assets/Companion_Class.png)

```scala
// Companion Class
class Person(val name: String, private val superheroName: String)

// Companion Object
object Person {
	def showName(x: Person) = x.superheroName
}

object Runner extends App {
	val test = new Person("ABC", "Superman")
	println(Person.showName(test))
}
```

![](/assets/Companion_Objects.png)

* Companion objects have the same name as the class they represent
* Companion objects must be in the same file as the class they represent
* Companion objects have access to their representative class's private information
* Classes have acess to the companion object's private information



