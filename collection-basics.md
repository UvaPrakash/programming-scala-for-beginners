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

![](/assets/Sets_1.png)

```scala
object Sets extends App {
	val set1 = Set(1,2,3,4)
	val set2 = Set(1,2,3,4,5)
	val set3 = Set(1,2,3,4,5,6)
	val set4 = Set(1,2,3,4,5,6,6,7)

	println(set1)
	println(set2)
	println(set3)
	println(set4)

	println(set1 diff set4) // empty set
	println(set4 diff set1) // Set(5,6,7)
	println(set1 union set2) // Set(1,2,3,4,5)
	println(set1 intersect set2) // Set(1,2,3,4)

	println(set1 ++ set2) // Same as union Set(1,2,3,4,5)
	println(set1 ++ List(5,6)) // Set(1,2,3,4,5,6)

	println(set1 -- set2) // Empty set
	println(set1 -- List(1,2)) // Set(3,4)
	println(set1 -- Set(1,2)) // Set(3,4)

	println(set1 - 3) // Set(1,2,4)
	println(set1 + 5) // Set(1,2,3,4,5)

	println(set1.apply(4)) // true
	println(set1.contains(4)) // true
}
```

![](/assets/Sets_2.png)



