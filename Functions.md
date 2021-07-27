# Functions

## Declaring Functions

You can write them (1) inside a class, like methods in Java—these are called member functions; (2) outside classes—these are called top-level functions; and (3) they can be written inside other functions—these are called local functions.

```Kotlin
fun functionName([parameters]) [:type] {
  statements
}
```
non-productive function
```kotlin
fun displayMessage(msg: String, count: Int) { var counter = 1
while(counter++ <= count ) {
    println(msg)
  }
}
```

**displayMessage With an Explicit Return Type**
```kotlin
fun displayMessage(msg: String, count: Int) : Unit { var counter = 1
while(counter++ <= count ) {
    println(msg)
  }
}
````

getSum, A Productive Function
```kotlin
fun getSum(values: List<Int>) : Int { // return type is Int var total = 0;
  for (i in values) total += i
  return total // return value
}
```

**Using Pairs As a Return Type**
```kotlin
fun bigSmall(a: Int, b:Int) : Pair<Int, Int> { 
  if(a > b) 
    return Pair(a,b)
  else {
    return Pair(b,a)
  }
}
 
fun main(args: Array<String>) { 
  var (x,y) = bigSmall(5,3)
  println(x)
  println(y) 
}
```
## Single Expression Functions

There are situations when we can omit (1) the return statement; (2) curly braces; and (3) the return type altogether. This second form is called single expression functions. As you may have inferred from its name, the function only contains a single expression

```kotlin
fun sumInt(a: Int, b: Int) = a + b
```
## Default Arguments
**connectToDb**
```kotlin
fun connectToDb(hostname: String = "localhost", username: String = "mysql",
  password:String = "secret") {
}
connectToDb("mycomputer","root")
```

## Named Parameters

we can name the argument at the call site.
```kotlin
connecToDb(hostname = "neptune", username = "jupiter",
password = "saturn")
```
a call like this isn’t allowed
```kotlin
connectToDb(hostname = "neptune", username = "jupiter", "saturn")

```
a call like this is allowed.
```kotlin
connectToDb("neptune",
username = "jupiter",
password = "saturn")
```
## Variable Number of Arguments
we use the vararg keyword.\
Demonstration of a Variable Argument Function<br>
it’s generic. We didn’t have to declare it as generic in order to work with variable arguments—we just chose to so that it could work with a variety of types.<br>
We need to use the spread operator * to unpack the array.

```kotlin
fun<T> manyParams(vararg va : T) {
  for (i in va) { 
    println(i) 
  }
}
fun main(args: Array<String>) {
  manyParams(1,2,3,4,5)
  manyParams("From", "Gallifrey", "to", "Trenzalore")
  manyParams(*args)
  manyParams(*"Hello there".split(" ").toTypedArray())
}
```
**Extension Functions**
 An extension function in Kotlin allows us
to add behavior to an existing class, including the ones written in Java, without using inheritance. It essentially lets us define a function that can be invoked as a member of the class, but the function is implemented outside the class. 
**Extended String Class**
```kotlin
fun main(args: Array<String>) {
  val msg = "My name is Maximus Decimus Meridius"
  println(msg.homerify()) 
  println(msg.chanthofy()) 
  println(msg.terminatorify())
}
fun String.homerify() = "$this -- woohoo!"
fun String.chanthofy() = "Chan, $this , tho"
fun String.terminatorify() = "$this -- I'll be back"
```
## Infix Functions
“Infix” notation is one of the notations used in math and logical expressions. It’s the placement of operator between operands (e.g., a + b; the plus symbol is “infixed” because it’s between the operands a and b). In contrast, operations can follow “post fixed” notation where the expression is written like so (+ a b) or they can be “post fixed,” in which our expression is written like this (a b +).

In Kotlin, member functions can be “infixed,” which allow us to write codes like the following:
```kotlin
john say "Hello World"
```
Person Class Without infix Function
```kotlin
fun main(args: Array<String>) { 
  val john = Person("John Doe") 
  john.say("Hello World")
}
class Person(val name : String) {
  fun say(message: String) = println("$name is saying $message")
}
```
Person Class With an infix Function
```kotlin
fun main(args: Array<String>) { 
  val john = Person("John Doe") 
  john say "Hello World"
}
class Person(val name : String) {
  infix fun say(message: String) = println("$name is saying $message")
}
```
A function can be converted to infix, only if
- it’s a member function (part of a class) or an extension function, and
- it accepts exactly one parameter (only). If you’re thinking of a loophole like, “I could probably define a single parameter in my function and use vararg,” that won’t work. Variable arguments are not allowed to be converted to infix functions.

## Operator Overloading
Operator overloading allows us to appropriate the use of some standard operators, like the math operators’ addition, subtraction, division, multiplication, and modulo. For example, we can write a code that allows the use of the plus sign to, say, add two Employee objects, or any other custom type.<br>

we can teach the addition operator how to add two Employee objects. 

```kotlin
class Employee(var name: String) {
  infix operator fun plus(emp: Employee) : Employee {
    this.name += "\n${emp.name}" //
    return this
  } 
}
fun main(args: Array<String>) {
  var e1 = Employee("John Doe") 
  var e2 = Employee("Jane Doe")
  var e3 = e1 plus e2
}
```
However, the function name plus isn’t an ordinary function name. It isn’t just another name that we thought about and made up. It has a special meaning to Kotlin. The plus function name is a fixed identifier that corresponds to the math operator +. And when this special function name is combined with the keywords infix and operator, it allows us to write codes like this
var e3 = e1 + e2

