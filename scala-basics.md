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

In the below example variable 'a' is of type Int and 'b' is of type String. Whereas variable 'c' is automatically inferred by Scala as String.

![](/assets/scala_type_inference_3.png)

