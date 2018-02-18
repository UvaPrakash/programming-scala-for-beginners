### Scala Tuples

A tuple is a collection of elements in ordered form. Unlike an array or list, a tuple can hold objects with different types but they are also **immutable**.

* Tuples are typed
* Tuples go all the way from Tuple1 to Tuple22
* Tuples are immutable
* Tuple2 has a swap method

![](/assets/Tuples_1.png)

```scala
object Tuples extends App {
	val t = (1, "Hello", 40.00)
	// Index starts with 1
	println(t._1)
	println(t._2)
	println(t._3)

	val t1:(Int, String, Double) = t
	val t2:Tuple3[Int, String, Double] = t //Tuple3 is a tuple of 3 elements. Scala has Tuple1 to Tuple22
}
```

![](/assets/Tuples_@.png)

#### Swapping elements

```scala
object TuplesSwap extends App {
	val t = new Tuple2("Hello", "World")
	val swap_tuple = t.swap
	println("After Swapping: " + swap_tuple)
	println("Before Swapping: " + t)
}
```

![](/assets/Tuples_3.png)



