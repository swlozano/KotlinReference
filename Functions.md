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


