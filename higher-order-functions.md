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
* apply method in the function means that you don't have to call it explicitly
* While you can return only one item, that one item can be a tuple if you need to return multiple items

```scala
object Functions extends App {
	// Returning a Tuple
	val f3 = (s:String) => (s, s.size)
	println(f3("Hello"))
}
```

![](/assets/Functions_4.png)



