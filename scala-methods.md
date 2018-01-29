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

#### Recursion

* Recursive methods call themselves
* Recursive methods require return type signature
* Recursive methods have a limited stack space

Let us create a Factorial program to understand the concept of recursion.

Create a program recursion.scala with the below code.

```
def factorial(n:BigInt):BigInt = {
    if(n == 0 || n == 1) 1
    else n * factorial(n-1)
}

println(factorial(5))
```

![](/assets/recursion_factorial.png)

Every recurs­ive func­tion has a \_base case \_and a \_recurs­ive case. \_The base case is the smal­lest piece, the prob­lem that we can solve right away. In this case it is the factorial of 0 or 1, which equals 1. The recurs­ive case is used to sim­plify the prob­lem by call­ing the same func­tion recurs­ively, until it reaches the base case.

When running factorial\(10000\) the method throws StackOverflowError.

![](/assets/recursion_stackoverflow.png)

#### Tail Optimized Recursion

TCO- Tail Call Optimization

A tail-recursive func­tion is a func­tion that has the recurs­ive call as its very last action.

Accumulators are used to store intermediate results since we do not want intermediate results to pile on the call stack.

We will redefine the above factorial method to be a tail recursive method to avoid StackOverflowError. By using @tailrec annotation we can implement TCO.

Create a file tailRecursion.scala with the below code.

```
import scala.annotation.tailrec

@tailrec
def fact(n:BigInt, acc:BigInt):BigInt = {
if(n == 0 || n == 1) acc
else fact(n-1, acc * n)
}

def factorial(n:BigInt) = fact(n,1) // Passing default value to the Accumulator

println(factorial(10000))
```

We need to pass a default value to the accumulator. Hence we have defined factorial method.

Now running the code will print the factorial of 10000 without any StackOverflowError.

