### Higher Order Functions

Scala supports functional programming approach. It provides rich set of built-in functions and allows you to create user defined functions also.

A function is a group of statements that perform a task.

You can create function by using `def`** **keyword. You must mention return type of parameters while defining function and return type of a function is optional. If you don't specify return type of a function, default return type is Unit.

Scala has traits from `Function0` to `Function22`

```scala
object Functions extends App {
    val f1:Function1[Int, Int] = new Function1[Int, Int] {
        def apply(x:Int):Int = x + 1    
    }
    println(f1(3)) // Same as f1.apply(3)
}
```

![](/assets/Functions_1.png)

`Function1` takes one parameter and one return value

```scala
trait Function1[-T1, +R] extends AnyRef
```

```scala
object Functions extends App {
    val f1:Function1[Int, Int] = new Function1[Int, Int] {
        def apply(x:Int):Int = x + 1    
    }

    val f0:Function0[Int] = new Function0[Int] {
        def apply() = 1
    }

    val f2:Function2[Int, String, String] = new Function2[Int, String, String] {
        def apply(x:Int, y:String):String = y + x
    }

    println(f1(3)) // Same as f1.apply(3)
    println(f0())
    println(f2(3, "Hello"))
}
```

![](/assets/Functions_2.png)

Let us refactor the above code

```scala
object Functions extends App {
    val f1 = (x:Int) => x + 1    

    val f0 = () => 1

    val f2 = (x:Int, y:String) => y + x

    println(f1(3)) // Same as f1.apply(3)
    println(f0())
    println(f2(3, "Hello"))
}
```

![](/assets/Functions_3.png)

* Functions are traits \(pure abstract\) that is instantiated anonymously
* `apply` method in the function means that you don't have to call it explicitly
* While you can return only one item, that one item can be a tuple if you need to return multiple items

```scala
object Functions extends App {
    // Returning a Tuple
    val f3 = (s:String) => (s, s.size)
    println(f3("Hello"))
}
```

![](/assets/Functions_4.png)

#### Difference between Methods and Functions

![](/assets/MethodsandFunctions_1.png)

* Methods belong to a context
* Functions are their own objects
* One difference is that methods are invoked on objects unlike functions. With functions you call them and pass arguments while with methods you invoke them on an object and pass arguments

* Another difference is that functions can be assigned to variables while methods can not be assigned to variables.

```scala
object MyObject {
    val f = (x:Int) => x + 1 // Function
    def g(x:Int) = x + 1 // Method
}

object MethodsandFunctions extends App {
    println(MyObject.f.apply(10)) // Invoking function
    println(MyObject.f(10)) // Same as f.apply(10)
    println(MyObject.g(10)) // Invoking method
}
```

![](/assets/MethodsandFunctions_2.png)

#### Partially Applied Functions

In functional programming languages, calling a function with parameters is to apply the function to the parameters. When all the parameters are passed to the function we have fully applied the function to all the parameters.

```scala
val add = (x: Int, y: Int) => x + y
```

But when we give only a subset of the parameters to the function, the result of the expression is a partially applied function.

![](/assets/PartiallyAppliedFunctions.png)

#### Converting a Method to a Function

* Methods can be converted to functions using Partially Applied Functions
* Use an underscore to turn method parameters to function parameters
* If an underscore is the last character in a method parameter, you can remove the underscore

![](/assets/ConvertingDefToFunctions_REPL.png)

```scala
class MyClass(x:Int) {
    def method1(y:Int) = x + y
}

class MyClass2(z:Int) {
    def method2(f:Int => Int) = f(z)
}

object ConvertDefToFunction extends App {
    val x = new MyClass(10)
    val f = x.method1 _ // Converting Method to Function (Partially Applied Functions)

    println(f.apply(20))
    println(f(20)) // Same as f.apply(20) // 30

    val z = new MyClass2(20)
    println(z.method2(f)) // 30
    println(z.method2(x.method1 _)) // Replacing f with x.bar _ // 30

    println(z.method2(x.method1)) // If _ is the last character in the method call we can ignore that // 30
}
```

![](/assets/ConvertingDefToFunction.png)

```scala
class MyClass(x:Int) {
    def method1(y:Int) = x + y
    def method2(z:Int, a:Int) = x + z + a
}

class MyClass2(z:Int) {
    def method3(f:Int => Int) = f(z)
    def method4(f:(Int, Int) => Int) = f(z, 10)
}

object ConvertDefToFunction extends App {
    val x = new MyClass(10)
    val z = new MyClass2(20)

    val f = x.method1 _ // Converting Method to Function (Partially Applied Functions)
    val f2 = x.method2(40, _:Int) // Converting to a Function

    println(z.method3(f2)) // 20+10+40 = 70
    println(z.method4(x.method2)) // 20+10+10 = 40
}
```

![](/assets/ConvertDefToFunction_2.png)

#### Closures

* A **closure **is a function, whose return value depends on the value of one or more variables declared outside this function
* Closures are functions that close around the environment
* It is best to enclose around something that is stable eg. val

```scala
object Main extends App { 
    val y = 3
    val multiplier = (x:Int) => x * y // Closure
    println(multiplier(3))
}
```

![](/assets/Closures.png)

#### Functions With Functions

* Functions can take other functions in as parameter, higher order functions
* Higher order function, the term is also used to describe when a method can take a function
* Functions can also return other functions, useful for applying functions in parts

```scala
object FunctionsWithFunctions extends App {
    val f = (x:Int, y:Int => Int) => y(x)
    println(f(3, (m: Int) => m+1))
    println(f(3, m => m+1))
    println(f(3, _ + 1)) // Same as above
    println(f(3, 1 +  _))
    println(f(3, 1+)) // If _ is last character then it can be removed. This will generate a warning
}
```

![](/assets/FunctionsWithFunctions_1.png)

In order to eliminate the warning we need to add the import clause `import scala.language.postfixOps`

```scala
object FunctionsWithFunctions extends App {
    val f = (x:Int, y:Int => Int) => y(x)
    println(f(3, (m: Int) => m+1))
    println(f(3, m => m+1))
    println(f(3, _ + 1)) // Same as above
    println(f(3, 1 +  _))

    import scala.language.postfixOps
    println(f(3, 1+)) // If _ is last character then it can be removed

    println("#######################")

    val g = (x:Int) => (y:Int) => x + y
    println(g.apply(2).apply(3))
    println(g(2)(3))
}
```

![](/assets/FunctionsWithFunctions_2.png)

#### Currying

* Currying is taking set of arguments and turning them into a sequence of functions returning functions
* You can convert a uncurried function into a curried function by calling `curried` on that function
* Use `Function.uncurried` to uncurry a function
* Currying is named after mathematician Haskell Curry

![](/assets/Currying_1.png)

```scala
object Currying extends App {
	val g = (x: Int) => (y: Int) => x + y
	val f = (x:Int, y:Int) => x + y
	val fc = f.curried // g and fc are same
	val f2 = Function.uncurried(fc) // f and f2 are same
	println(f2(4,5))
}
```

![](/assets/Currying_2.png)



