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



