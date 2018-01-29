### Scala Methods

#### Basic Methods

In Scala, methods starts with a keyword 'def'.

Lets create a sample method for adding two numbers. Create BasicMethods.scala with the below contents.

```
// Inefficient way of writing definition
def add(num1:Int, num2: Int):Int = {
    return num1+num2
}

println(add(4,5))
```

![](/assets/Basic_Methods_1.png)

We can refactor the above code to improve readability and make it more efficient.

```
// Efficient way of writing definition
def add(num1:Int, num2: Int) = num1 + num2
println(add(4,5))
```

![](/assets/Basic_Methods_2.png)

Few points to be observed

* In Scala, there is no need to explicitly mention return statement. Whatever is the last line in the method will be returned.
* Since we have only one line here, we have removed the curly braces.
* Also the method arguments takes Int type. Adding two Int also returns an Int. Hence return type of the method is removed and type inference of Scala can decide the return type.

#### Types: Any, AnyVal and AnyRef

![](/assets/scala_types_any.png)

![](assets/unified-types-diagram.svg)

* _**Any**_** **is the utmost super type and is the parent of everything.
* _**AnyVal**_** **is the parent of Primitive types.
* _**AnyRef**_ is the same as java.lang.Object in Java.
* _**AnyRef**_ is the parent of all classes written in Java and Scala.

#### Different Return Types

* Types returned from a method are inferred
* Type inferencer will make the best judgement
* If types are different it will find a common ancestor

![](/assets/Different_Return_Types.png)

Here the if clause returns String \(AnyRef\) whereas else clause returns Int \(AnyVal\). Hence the common ancestor of those two is Any.

#### Units and Unit Convention

* Unit is similar to void in Java.
* Unit is actually an object
* Unit's full type name is scala.Unit
* Unit has one value \(\)

![](/assets/Unit_Example.png)

![](/assets/Unit_println.png)

![](/assets/Unit_Example_2.png)

Since both Unit and Int have common ancestor AnyVal hence the return type of method add is AnyVal.

