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



