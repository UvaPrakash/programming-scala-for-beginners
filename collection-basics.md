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

#### Maps

* Maps are table like collection that stores keys and values
* Internally, maps are collection of tuples and can be operated on as such
* Symbols, are like Strings but guaranteed to be interned, perfect for Maps

String Interning is a method of storing only one copy of each distinct String Value, which must be immutable.

```scala
object Maps extends App {
    val m1 = Map.apply((1,"One"), (2,"Two"), (3,"Three"))
    val m2 = Map((1,"One"), (2,"Two"), (3,"Three")) // Other way of defining map
    val m3 = Map(1 -> "One", 2 -> "Two", 3 -> "Three") // Other way of defining map

    println(m3.get(1)) // Some(One)
    println(m3.apply(1)) // One
    println(m3(1)) // Same as m3.apply(1)
    println(m3.get(4)) // None
    // println(m3(4)) // Error java.util.NoSuchElementException: key not found: 4

    println(m3.toList)
    println(m3.keys) // Set
    println(m3.keySet) // Set
     println(m3.values) // MapLike
    println(m3.values.toSet) // Set
    println(m3.values.toList) // List

    val co1 = Symbol("Co")
    val co2 = 'Co
    println(co1 == co2) // true
    println(co1 eq co2) // true

    // Map with Symbols
    val elements:Map[Symbol, String] = Map('Co -> "Cobalt", 'H -> "Helium", 'Pb -> "Lead")
    println(elements.get('Co)) // Some(Cobalt)
}
```

![](/assets/Maps_1.png)

#### Arrays and Repeated Parameters

* Arrays in Scala are converted to a primitive array on the JVM
* Behaviour wise in Scala, they are similar to Lists
* Arrays are mutable
* Repeated Parameters uses an Array to hold possible extra parameters

```scala
object Arrays extends App {
    val a:Array[Int] = Array(1,2,3,4)

    println(a.head)
    println(a.tail)
    println(a.tail.toList)
    println(a.init)
    println(a.init.toList)
    println(a.last)
    println(a.apply(2))
    println(a.max)
    println(a.min)
    println(a.isEmpty)

    def repeatedParameter(x:Int, y:String, z:Any*) = {
        println(z)
        "%d %ss give you %s".format(x, y, z.mkString(", "))
    }

    println(repeatedParameter(3, "egg", "a delicious sandwich", "protein", "high cholestrol"))
    println(repeatedParameter(3, "egg", List("a delicious sandwich", "protein", "high cholestrol"):_*))
}
```

![](/assets/Arrays.png)

#### Ranges

* Ranges are a way to create a collection of numbers or characters without specifying them one by one
* You can create ranges with syntax sugar
* You can also create ranges with a factory in the Range companion object

![](/assets/Ranges_REPL.png)

```scala
object Ranges extends App {
    val r1 = 1 to 10 // include 10
    val r2 = 1 until 10 // exclude 10

    println(r1)
    println(r2)
    println(r1.head)
    println(r1.tail)

    val r3 = 2 to 10 by 2
    println(r3)

    val r4 = 10 to 2 by -2
    println(r4)

    val r5 = 'a' to 'z'
    println(r5)

    val r6 = ('a' to 'z') ++ ('A' to 'Z')
    println(r6)

    val r7 = Range(1,10) //exclude 10
    println(r7)

    val r8 = Range(1,10,2) //exclude 10, step 2
    println(r8)

    val r9 = Range.inclusive(1,10) //include 10
    println(r9)

    val r10 = Range.inclusive(10,1,-2) //include 10, step 2
    println(r10)

    // For loop
    for (i <- 1 to 10) println(i + 1)
}
```

![](/assets/Ranges.png)

