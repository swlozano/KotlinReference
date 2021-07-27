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

