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
