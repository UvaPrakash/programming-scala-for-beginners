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

#### filter, filterNot, exists

* `filter` filters out elements that meet a predicate criteria
* `filterNot` filters out elements that do not meet the predicate criteria
* `exists` tests if something exists in a collection based on a function

```scala
object FilterFunction extends App {
    // Range
    val a = 1 to 10
    println(a.filter(x => x % 2 == 0)) // Filter even numbers
    println(a.filter(_ % 2 == 0)) // Filter even numbers
    println(a.filterNot(_ % 2 == 0)) // Filter odd numbers
    println(a.exists(_ % 2 == 0)) // Does it have even numbers

    // String
    def filterVowels(s:String) = s.toLowerCase.filter(c => Set('a','e','i','o','u').contains(c))
    println(filterVowels("Apple"))

    // Set
    val b = Set("Brown", "Red", "Blue", "Green", "Yellow", "Black")
    println(b.filter(s => filterVowels(s).size > 1))

    // Map
    val m = Map(1 -> "One", 2 -> "Two", 3 -> "Three", 4 -> "Four", 5 -> "Five")
    println(m.filterKeys(_ % 2 == 0))

    // Options
    println(Some(5).filter(_ % 2 == 0)) // None
    println(Some(6).filter(_ % 2 == 0))
}
```

![](/assets/Filter_Function.png)

#### foreach

* `foreach` is a method that takes a function which takes each element and returns `Unit`
* Its perfect to use when you want to take an element and perform a side-effect like printing on a screen
* `foreach` is available for lists, ranges, sets, maps, options etc.

```scala
object ForEachMethod extends App {
	val a = 1 to 10
	// a.foreach(x => println(x))
	// a.foreach(println(_))
	// a.foreach(println _)
	a foreach println
}
```

![](/assets/foreach_method.png)

#### flatMap





