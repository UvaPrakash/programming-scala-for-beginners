### val and var

Scala allows one to declare whether the variable is mutable or immutable.

**val**- Immutable \(value cannot be updated\)

**var**- Mutable \(value can be changed\)

Here 'a' has been initialized to a value during its declaration. As it has been declared as a val, 'a' cannot be reassigned to a new value. Any attempt to do will result in reassignment to val error.

![](/assets/scala_val.png)

Unlike val, “var” can be reassigned to different values \(mutable\). However type cannot be changed.

![](/assets/scala_var.png)

### Type Inference

Scala has a built-in type inference mechanism. Without specifying the type explicitly, scala inferences the type. We can also explicitly mention the type of a variable.

![](/assets/scala_type_inference.png)

![](/assets/scala_type_inference_2.png)

In the below example variable 'a' is of type Int and 'b' is of type String. Whereas variable 'c' is automatically type inferred by Scala as String.

![](/assets/scala_type_inference_3.png)

#### Lazy Val

The difference between val and lazy val is that a val is executed when it is defined whereas a lazy val is evaluated when it is accessed for the first time.

Here the lazy val 'b' is getting executed only during its call and not during the definition.

![](/assets/lazy_val.png)

**Note: There is no such thing as lazy var**

![](/assets/lazy_var.png)

#### Types in Scala

![](assets/unified-types-diagram.svg)Source: [https://docs.scala-lang.org/tour/unified-types.html](https://docs.scala-lang.org/tour/unified-types.html)

| Data Type | Range |
| :--- | :--- |
| Byte | 8-bit signed two's complement integer \(-2^7 to 2^7-1, inclusive\) |
| Short | 16-bit signed two's complement integer \(-2^15 to 2^15-1, inclusive\) |
| Int | 32-bit signed two's complement integer \(-2^31 to 2^31-1, inclusive\) |
| Long | 64-bit signed two's complement integer \(-2^63 to 2^63-1, inclusive\) |
| Char | 16-bit unsigned Unicode character \(0 to 2^16-1, inclusive\) |
| String | sequence of chars |
| Float | 32-bit IEEE 754 single-precision float |
| Double | 64-bit IEEE 754 double-precision float |
| Boolean | true or false |

#### IF, ELSE IF, ELSE

Create a new file ifStatement.scala and paste the below code

```
val a = 1
val result = if(a<10) "Number is less than 10"
         else if(a>10) "Number is greater than 10" 
           else "Number is 10"

println(result)
```

![](/assets/if_statement.png)

#### WHILE, DO WHILE

```
// Program for printing number in reverse
// Object Oriented Style
var a = 10
var result1 = ""
while(a>0) {
        result1 = result1 + a
        if (a>1) result1 = result1 + ","
        a = a-1
}
println(result1)

// Functional Style
val result2 = (1 to 10).reverse.mkString(",")
println(result2)

// Optimized Code
println((10 to 1 by -1).mkString(","))
```

![](/assets/whileStatement.png)**Do While Statement**

```
var a = 10
var result1 = ""

do {
    result1 = result1 + a
    if(a>1) result1 = result1 + ","
    a = a - 1
} while(a>0)

println(result1)
```

![](/assets/dowhileStatement.png)

The difference between while loop and do while loop is that in case of do while loop atleast once the loop gets executed irrespective of the condition.

#### For Loops

```
// Object Oriented Style
var result = ""
for(a <- 1 to 10) {
        result = result + a
        if(a<10) result = result + ","
}

println(result)
```

![](/assets/forLoops_1.png)

Using for loops to perform operations in List

```
// Using for loops in List to add 1 to every number in List
val xs = List(1,2,3,4)
var result1 =  List[Int]()

for(a <- xs) result1 = result1 :+ (a+1)
println(result1)
```

![](/assets/forLoops_2.png)

The above code can be optimized as below.

```
// Functional Implementation
val list2 = List(1,2,3,4)
val result2 = for(b <- list2) yield (b+1)
println(result2)
```

![](/assets/forLoops_3.png)

#### String Formatting

```
// Older Java style
val str1 = String.format("This is a %s","Test")
println(str1)

// Scala style
val str2 = "This is a %s".format("test")
println(str2)

// Printing multiple values in sequence
println("Multiple string %s %s %s".format("value1","value2","value3"))

// Printing multiple values in any order
println("Multiple string %3$s %2$s %1$s".format("value1","value2","value3"))

// Printing date, time and year
import java.time._
println("We will be eating on %1$tB %1$te in the year %1$tY".format(LocalDate.now))
printf("We will be eating on %1$tB %1$te in the year %1$tY",LocalDate.now)
```

#### ![](/assets/stringFormatting.png)

#### String Interpolation

```
val a = 99
val b = 100
println(s"$a testing")
println(s"${a+b} testing")

val ticketCost = 50
val bandName = "ABC"
println(f"The $bandName%s tickets costs $$$ticketCost%1.2f")
```

![](/assets/stringInterpolation.png)

