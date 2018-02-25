### Collections with Functions

#### Map

* Map takes a function and applies that function to every element in a collection
* Map can be applied to List, Set, Maps, Streams, Strings even Options

```scala
object MapFunction extends App {
	// List
	val a = List(1,2,3,4,5,6)
	val f = (x: Int) => x + 1
	
	println(a.map(f))
	println(a.map((x:Int) => x * 2))
	println(a.map(x => x * 2)) // Removing the type
	println(a.map(_ * 2))
	println(a.map(2 * _))

	import scala.language.postfixOps
	println(a.map(2 *))

	// Set
	val b = Set("Brown", "Red", "Blue", "Green", "Yellow", "Black")
	println(b.map(x => x.size))
	println(b.map(_.size))
	println(b.map(x => (x, x.size)))
	
	// Map
	val fifaTeam = Map('Germany -> 4, 'Brazil -> 5, 'Italy -> 3, 'Argentina -> 2)
	println(fifaTeam.map(t => (Symbol.apply("Team " + t._1.name), t._2)))
	
	// String
	println("Hello".map(c => c + 1))
	println("Hello".map(c => (c + 1).toChar))

	// Options
	println(Some(4).map(1+))
	// println(None.map(1+)) // error: ambiguous reference to overloaded definition // match expected type Nothing => ?

	println(None.asInstanceOf[Option[Int]].map(1+))
	val age:Option[Int] = None
	println(age.map(1+))
}
```

![](/assets/Map_Function.png)



