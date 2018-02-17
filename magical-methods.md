### Magical Methods

#### Magical Apply Method

Let us create a sampe method named `bar` to understand the concept of `apply` method.

```scala
class Foo(x:Int) {
    def bar(y:Int) = x + y
}

object MagicApply extends App {
    val foo = new Foo(10)
    println(foo.bar(20))
}
```

![](/assets/Magic_Apply_bar.png)

Let us modify the method named `bar` to `apply`

```scala
class Foo(x:Int) {
    def apply(y:Int) = x + y
}

object MagicApply extends App {
    val foo = new Foo(10)
    println(foo.apply(20))
    println(foo(20)) // Same as foo.apply(20)
}
```

![](/assets/MagicApply_apply.png)

* If a method is called `apply`, you don't have to explicitly call it
* The method apply can be used in classes and objects

#### Infix Operators

* Infix operators allows a method to be invoked to be invoked without the dot or paranthesis
* Infix operators will work if the method has one parameter
* It can somewhat work with more than one parameter, but the parameters would have to be inside paranthesis
* Mathematical operations in Scala use infix operators

```scala
class Foo(x:Int) {
    def bar(y:Int) = x + y
}

object InfixOperatorsRunner extends App {
    val foo = new Foo(10)
    println(foo.bar(20)) // Classic way
    println(foo bar 20) // Infix way
}
```

![](/assets/Infix_Operators_1.png)

Let us use infix operator for two arguments

```scala
class Foo(x:Int) {
    def bar(y:Int) = x + y
    def bar2(a:Int, b:Int) = x + a + b
    def bar_object(z:Int) = new Foo(x + z)
}

object InfixOperatorsRunner extends App {
    val foo = new Foo(10)

    // Single argument
    println(foo.bar(20)) // Classic way
    println(foo bar 20) // Infix way

    // Two arguments
    println(foo.bar2(10, 20)) // Classic way
    println(foo bar2 (10, 20)) // Infix way

    // Complex operations
    println(foo bar 5 + 10) // 15 + 10 = 25
    println(foo bar_object 4 bar 40 + 300) // 14 + 40 + 300 = 354
}
```

![](/assets/Infix_Operators_2.png)

This is similar to the below code

![](/assets/Infix_Operators_3.png)

#### Right Associative Colons

* If the method ends in a colon, you may invoke it in a right associative way
* In order to invoke it in a right associative way, it must be invoked as an infix method
* Right associativity is primarily used with `List` and `Stream` operations

```scala
object RightAssociativeColons extends App {
	class Foo(x:Int) {
		def bar(y:Int)	= x + y
	}

	val foo = new Foo(10)
	println(foo.bar(5))
}
```

![](/assets/Right_Associative_Colons_1.png)

```scala
object RightAssociativeColons extends App {
	class Foo(x:Int) {
	     def ~:(y:Int)	= x + y
	}

	val foo = new Foo(10)
	println(foo.~:(5)) // Classic way
	println(5 ~: foo) //Right Associative Colon. Infix way
}
```

![](/assets/Right_Associative_Colons_2.png)



