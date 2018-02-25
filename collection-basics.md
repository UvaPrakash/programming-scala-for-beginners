### Collection

#### Lists

* Lists are immutable collections, duplicates allowed, access by index, searchable
* `Nil` is an empty list
* Lists can also be created from the companion object and the `apply` method
* Lists have many of the same functional properties as other collections

![](/assets/Lists_1.png)

```scala
object Lists extends App {
	val a = List(1,2,3,4,5)
	val a2 = List.apply(1,2,3,4,5)
	val a3 = 1 :: 2 :: 3 :: 4 :: 5 :: Nil

	println(a.head) // 1
	println(a.tail) // 2,3,4,5
	println(a.init) // 1,2,3,4
	println(a.last) //5

	println(a.apply(4)) //5th element in List. Index starts from 0
	println(a.min) // 1
	println(a.max) // 5
	println(a.isEmpty) // false
	println(a.nonEmpty) // true
	println(a.updated(3, 100))

	println(a.mkString(",")) // Convert List to String
	println(a.mkString("[",",","]"))
}
```

![](/assets/Lists_2.png)

#### Sets

* Sets are collections with no duplicate elements, unordered, no search by index, but fast querying
* Sets typically are more mathematically powerful than Lists
* `apply` will return `true` or `false`



