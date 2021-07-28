# Lambdas and Higher Order Functions
## Higher Order Functions


Higher order functions are functions that operate on other functions, either by taking them in as parameters or by returning them.
<br>
Below shows an example of a function that takes in another function as parameter.
**A Function That Accepts Another Function**

```kotlin
fun executor(action:() -> Unit) { 
  action()
}
```

Action is the name of the parameter and its type is written as ()-> Unit, which means that it’s type is function.
A function type is written with a pair of parentheses, followed by the arrow operator
(a dash plus the greater than sign) and then followed by a type that the function is supposed to return.
<br>
We can pass (or return) functions from anywhere we can pass (or return) variables.<br>
Wherever you can use a variable, you can also use a function.
<br>
In Kotlin, a function isn’t just a named collection of statement, it’s also a type. So, just like String, Int, or Float, we can declare a variable to be of type function.<br>
A function type has three components: 
<br>(1) the parenthesized parameter type list; 
<br>(2) the arrow operator; 
<br>(3) the return type.
<br>
Now that we understand how to declare a parameter to be of function type, let’s take a look at how to declare and define a variable to be of function type.

```kotlin
//How to Declare and Define a Function Type
val doThis:() -> Unit = { 
  println("action")
}
```
```kotlin
//Complete Code for doThis and executor() Examples
val doThis:() -> Unit = { ➊ 
  println("action")
}
fun executor(action:() -> Unit) { ➋ 
  action() ➌
  action.invoke() ➍
}
fun main(args: Array<String>) { 
   executor(doThis) ➎
}
```
➌ by appending a pair of parentheses on the name of the parameter, we get to invoke the function.<br>
➍ this is another way of invoking the action function, but calling it like action()is more idiomatic and, hence, preferred.<br>
➎ inside the main function, we get to call executor() and we pass doThis. note that we’re not passing doThis()with the parentheses. We don’t want to invoke doThis and then pass the resulting value to executor(). What we want is to pass doThis not as a resulting value, but as a function definition. the idea is to invoke doThis within the body of the executor()function.<br>

**Another Way of Writing the doThis and executor() Examples**
```kotlin
fun doThis() { ➊ 
  println ("action")
}
fun executor(action:() -> Unit) { 
  action()
}
fun main(args: Array<String>) { 
  executor(::doThis) ➋
}
```
➊ doThis is now defined in the usual way that we write functions, with the fun keyword and the name of the function in the header.<br>
➋ ::doThis is invoked with a double colon. this means we are resolving the function within the current package.
<br>

## Lambda and Anonymous Functions

Lambdas and anonymous functions are called function literals. These are functions that are not declared but, rather, passed immediately as an expression—more often than not, to a higher order function. Because of this they don’t need a name. 
<br>
you can actually use this without passing it to a higher order function. To invoke it, you may do something like the following—presumably inside function main or any other top-level function<br>
doThis()<br>
or something like this<br>
doThis.invoke()
<br>
Anyway, lambda expressions aren’t meant to be used like this. They really shine when used within the context of higher order functions.
<br>
Instead of declaring and defining a named lambda, we will simply pass it as an argument to the higher order function executor, as seen in

**Pass a lambda to a Higher Order Function**
```kotlin
fun main(args: Array<String>) {
  executor({ println("do this") } ➊ )
}
fun executor(action:() -> Unit) { 
  action()
}
```
➊This is the function literal. in Listing 5-5, we passed doThis, which was a property whose value was a lambda expression. in this example, we are passing the lambda expression itself directly to the higher order function. a lambda expression is enclosed in a pair of curly braces— just like the body of a function.

## Parameters in Lambda Expressions
If we were to write it as a lambda, it would look like
```kotlin
Simple Function to Display a String
fun display(msg:String) { 
  println("Hello $msg")
}
```
```kotlin
//display Function Written As lambda 
{ msg:String -> println("Hello $msg") }
```
You’ll notice that the entire function header, the keyword fun and the function name, is completely gone, and the parameter list was relocated inside the lambda expression.
<br>
The whole expression is enclosed in a pair of curly braces. <br>
In a lambda expression, the parameter list is written on the left-hand side of the arrow operator and the body of
the function is found on the right. <br>
You will also notice that the parameters in a lambda expression don’t need to be inside a pair of parentheses because the arrow operator separates the parameter list from the body of the lambda.<br>
You can omit the type declaration of String in the parameter, so it can be written like in Listing.
```kotlin
//Omitted Type Declaration in Parameter List 
{ msg -> println("Hello $msg") }
You will also notice that the parameters in a lambda expression don’t need to be inside a pair of parentheses because the arrow operator separates the parameter list from the body of the lambda.
```

In some cases where the lambda expression takes only one parameter, Kotlin allows us to omit the parameter declaration and even the arrow operator. We can rewrite  in an even shorter way.
```kotlin
//The Implicit It 
{ println("Hello $it") }
```
The it parameter name is generated if the context expects a lambda that has only one parameter and if its type can be inferred. the full code on how to declare and use a lambda expression within the context of a higher order function. 
<br>Now we have the functional programming version of the Hello World example.

```kotlin
//Full Code for the lambda Example
fun main(args: Array<String>) { 
  executor({ println("Hello $it") })
}
fun executor(display:(msg:String) -> Unit) { 
  display("World")
}
```
Writing and using lambdas with more than one parameter isn’t much different from our single parameter example, as long as you write the parameter list on left side of the arrow operator.

```kotlin
//lambdas With More Than One Parameter
fun main(args: Array<String>) { 
  doer({ x,y -> println(x + y) })
}
fun doer(sum:(x:Int,y:Int) -> Unit) { 
  sum(1,2)
}
```
There may be occasions when a higher order function will take in some other parameters together with function types. Such a function could look like:
```kotlin
//Higher Order Function With Multiple Parameters
fun executor(arg: String = "Mondo", display:(msg:String) -> Unit) { 
  display(arg)
}
//We can invoke this function with this
executor("Earth", {println("Hola $it")})
//And since executor’s first parameter has a default value, we can still invoke it like this 
executor({println("Hola $it")})
```
In cases where the lambda is expected as the last parameter in a higher order function, we can write the lambda outside the parentheses of the invoking function, like this:

```kotlin
executor() { println("Hello $it")}
````
And if the lambda is the only parameter, we can even omit the parentheses entirely, like this one:
```kotlin
executor { println("Hello $it")}
```

## Closures
When you use a lambda expression inside a function, the lambda can access its closure. The closure is comprised of the local variables in the outer scope as well as all the parameters of the enclosing function.

 ```kotlin
//lambda Accessing Its Closure
fun main(args: Array<String>) { 
  executor(listOf(1..1000).flatten()) ➊
}
fun executor(numbers:List<Int>) { 
  var sum = 0;
  numbers.forEach { ➋
    if ( it % 2 == 0 ) { 
      sum += it ➌
    } 
  }
  println("Sum of all even numbers = $sum") 
}
```

➊ We’re passing a list of Ints to the executor()function. using the rangeTo function in operator form (..) is a handy way to generate a list of integers from 1 up to 1000. but you’d have to use the flatten() function to make it a list of Ints.<br>
➋ forEach is a higher order function; it takes in a lambda, which allows us to walk through items in the list. the forEach only has one parameter, and we can access that single parameter using the implicit it parameter name.<br>
➌ the sum variable is part of the closure; it’s within the function body where the lambda is defined. Lambdas have access to their closures.<br>

## with and apply

Kotlin lambdas have the ability to call methods of a different object without additional qualifiers in the body of the lambda. These kinds of lambdas are called lambdas with receivers.

The functions with and apply are of particular interest not because they allow
us to perform multiple operations on the same object without repeating the object’s name—which is a welcome feature-but because they look like they were baked into the language, which they’re not. They simply are functions that were made special by extension functions and lambdas.

//class Event
```kotlin
import java.util.Date
data class Event(val title:String) {
  var date = Date()
  var time = ""
  var attendees = mutableListOf<String>()
  fun create() {
    print(this)
  } 
}
  
fun main(args: Array<String>) {
  val mtg = Event("Management meeting")
  mtg.date = Date(2018,1,1) 
  mtg.time = "0900H" 
  mtg.attendees.add("Ted")
  mtg.create() 
} 
```
If we were to use the with function to refactor the code, it would look like:
```kotlin
//Using the With Function 
fun main(args: Array<String>) {
  val mtg = Event("Management meeting")
  with(mtg) {
    date = Date(2018,1,1) 
    time = "0900H" 
    attendees.add("Ted")
  } 
}
```

**The apply** function can achieve the same thing; it’s almost very similar to the with function except that it returns the receiver (the object passed to it)—the with function doesn’t.

```kotlin
fun main(args: Array<String>) {
  val mtg = Event("Management meeting")
  mtg.apply { ➊ 
    date = Date() ➋ 
    time = "0900H" 
    attendees.add("Ted")
  }.create() ➌ 
}
```

➊ Apply is an extension function and the mtg object becomes its receiver.  <br>
➋ and because the mtg object is the receiver, this refers to the mtg object. <br>
➌ When the lambda returns, it returns the receiver, which is a mtg object; hence, we can chain some calls into it.
<br>  
There are many more functions in Standard.Kt like run, let, also, etc., but these two examples using with and apply should give us an idea of what lambdas are capable of.
  
