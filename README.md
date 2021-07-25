# KotlinReference
Guia rápida  de Kotlin para desarrolladores Android. 

## Kotlin Basics

### Literals
Kotlin provides literals for the basic types (numbers, character, Boolean, String).


```kotlin
var intLiteral = 5
var doubleLiteral = .02
var stringLiteral = "Hello" var charLiteral = '1'
var boolLiteral = true
```

### Variables
A variable in Kotlin is created by declaring an identifier using the var keyword followed by the type, like in the statement

```kotlin
var foo: Int
foo = 10
println(foo)
```
or
```kotlin
var foo: Int = 10 
println(foo)
```
or
```kotlin
var foo = 10 
println(foo)
```

### Keywords
Keywords are reserved terms that have special meaning to the compiler, and as such, they cannot be used as identifiers for any program elements such as classes, variable names, function names, and interfaces.

Hard keywords 

```kotlin
as, break, class, continue, do, else, false, while, this, throw, try, super, and when.
```

Soft keywords
```kotlin
file, finally, get, import, receiver, set, constructor, delegate, get, by, and where.
```

Modifier keywords
```Kotlin
  abstract, actual, annotation, companion, enum, final, infix, inline, lateinit, operator, and open
```

### Whitespace
whitespace is not significant and can be safely ignored. 

```kotlin
fun main(args: Array<String>) { 
  println( "Hello")
}
```
or
```kotlin
fun main(args: Array<String>) {println("Hello")}
```

### Operators

**mathematical operators** \
```+, -, *, /, %```

**the equal symbol** \
```= ```\
is used for the assignment statement

**assignment operators** \
```+=, -=, *=, /=, %=```

**logical operations** \
```&&, ||, !```\
logical operators\
```'and', 'or', 'not' ```

**equality operators** 
```kotlin
==, !=
```
you can use these operators to compare any type
```kotlin
fun main(args: Array<String>) {
  var a = "Hello"
  var b = "Hello"
  if (a == b) { 
    // this evaluates to true println("$a is equal to $b")
  } 
}
```
### referential equality\
```kotlin
===, !===
``` 
valuates to true if and only if a and b point to the same object
```kotlin
  var p1 = Person("John") var p2 = Person("John")
  if(p1 === p2) { 
  // false println("p1 == p2")
  }
```
p1 and p2 do not point to the same object; hence, the triple equals will not evaluate to true

**Comparison operators**
```kotlin
<, >, <=, >=
```
**index access**
```kotlin
[ ][,]
```
```kotlin
fun main(args: Array<String>) {
  val fruits = listOf("Apple", "Banana", "Orange") 
  println(fruits.get(2)) // Banana 
  println(fruits[2]) // Banana
}
```
### KDoc Comments
KDoc is like Javadoc, it starts with /** and it ends with */. This form of commenting is very similar to the multiline comment , but this is used to provide API documentation to Kotlin codes. 

```kotlin
/**
   This is an example documentation using KDoc syntax
   @author Ted Hagos
   @constructor
   */
   class Person(val name: String) {
      /**
      This is another KDoc comment
      @return
      */
      fun foo(): Int{
      } 
   }
```
### Numbers and Literal Constants
```kotlin
var a = 10L // a is a Long literal, note the L postfix var b = 20
var a = b // this won't work
var a = b.toLong() // this will work
```

```kotlin
var a = 100 // Int literal 
var b = 10L // Long literal
```
You can use underscores in numeric literals to make them more readable. This feature was introduced in Java 7 and its later versions.
```kotlin
var oneMillion = 1_000_000
var creditCardNumber = 1234_5678_9012_3456
```

Literals with decimal positions are automatically Doubles. To declare a float literal, use the F postfix, like
```kotlin
var a = 3.1416 // Double literal 
var b = 2.54 // Float literal
```
Every number type can be converted to any of the number types. That means all Double, Float, Int, Long, Byte, and Short types support the following member functions:
```kotlin
• toByte() : Byte
• toShort() : Short
• toInt() : Int
• toLong() : Long
• toFloat() : Float
• toDouble() : Double
• toChar() : Char
```
### Characters
Characters in Kotlin cannot be treated directly as numbers. 
```kotlin
var enterKey = 'a'
```
Member Functions of the Character Type
```kotlin
val a = 'a'
println(a.isLowerCase()) // true 
println(a.isDigit()) // false
println(a.toUpperCase()) // A
val b: String = a.toString() // converts it to a String
```

### Escape sequences

use escape sequences such as \t, \b, \n, \r, \", \", \\, and \$ and if you need to encode any other character, you can use the Unicode syntax (e.g., \uFF00).

### Booleans
Booleans are represented by the literals true and false. 

### Arrays
Working With the Array Type
```kotlin
fun main(args: Array<String>) {
    var emptyArray = arrayOfNulls<String>(2) 
    emptyArray[0] = "Hello" 
    emptyArray[1] = "World"
    for (i in emptyArray.indices) println(emptyArray[i]) 
    for (i in emptyArray) println(i) 
    var arrayOfInts = arrayOf(1,2,3,4,5,6) 
    arrayOfInts.forEach { e -> println(e) } 
    var arrayWords = "The quick brown fox".split(" ").toTypedArray() 
    arrayWords.forEach { item -> println(item) }
}
```

### Strings and String Templates
var str: String = "Hello World\n"

#### raw string
using triple quote delimiter

```kotlin
var rawStr = """Amy Pond, there's something you'd better understand about me 'cause it's important, and one day your life may depend on it:
I am definitely a mad man with a box!
"""
```

#### about Kotlin strings
```kotlin
  val str = "The quick brown fox"
  for (i in str) println(i)
  println(str[2]) // returns 'e'
  var strNum = 10 + "" // this won't work anymore
  var strNum = 10.toString() // we have to explicitly convert now
```
#### Using String.format and printf
```kotlin
var name = "John Doe"
var email = "john.doe@gmail.com" var phone = "(01)777-1234"
var concat = String.format("name: %s | email: %s | phone: %s", name, email, phone)
println(concat)
// prints
// name: John Doe | email: john.doe@gmail.com | phone: (01)777-1234
```
```kotlin
var concat = "name: $name | email: $email | phone: $phone" println(concat)
// prints
// name: John Doe | email: john.doe@gmail.com | phone: (01)777-1234
```
#### Using Template Expressions
```kotlin
fun main(args:Array<String>) {
    var name = "John Doe"
    println("Hello $name")
    println("The name '$name' is ${name.length} characters long")
    println("Hello ${foo()}")
}
fun foo(): String { 
  return "Boo"
}
```
### Controlling Program Flow
#### Using ifs

The basic form of the if construct is 
```kotlin
if (expression) statement
```

```kotlin
val theQuestion = "Doctor who" 
val answer = "Theta Sigma"
val correctAnswer = ""
if (answer == correctAnswer) { 
  println("You are correct")
}
```

**else if**

```kotlin
val d = Date()
val c = Calendar.getInstance()
val day = c.get(Calendar.DAY_OF_WEEK)
if (day == 1) { 
  println("Today is Sunday")
}
else if (day == 2) {
  println("Today is Monday") 
}
else if ( day == 3) { 
  println("Today is Tuesday")
}
```
```kotlin
val theQuestion = "Doctor who" 
val answer = "Theta Sigma"
val correctAnswer = ""
var message = if (answer == correctAnswer) { 
  "You are correct"
} else{
  "Try again" 
}
```
omit the curly braces on the blocks, since the blocks contain only single statements.
```kotlin
var message = if (answer == correctAnswer) "You are correct" else "Try again"
```
### The when Statement
```kotlin
val d = Date()
val c = Calendar.getInstance()
val day = c.get(Calendar.DAY_OF_WEEK)
when (day) {
  1 -> println("Sunday")
  2 -> println("Monday")
  3 -> println("Tuesday")
  4 -> println("Wednesday")
}
```
when construct can also be used as an expression
```kotlin
val d = Date()
val c = Calendar.getInstance()
val day = c.get(Calendar.DAY_OF_WEEK)
var dayOfweek = when (day) { 
  1 -> "Sunday"
  2 -> "Monday"
  3 -> "Tuesday"
  4 -> "Wednesday"
  else -> "Unknown" 
}
```
How to Write Branches Inside the When Construct

```kotlin
fun main(args: Array<String>) {
    print("What is the answer to life? ")
    var response:Int? = readLine()?.toInt() 
    val message = when(response){
        42 -> "So long, and thanks for the all fish" 
        43, 44, 45 -> "either 43,44 or 45" 
        in 46 .. 100 -> "forty six to one hundred" 
        else -> "Not what I'm looking for"
    }
    println(message)
}
```
### The while Statement

The while and do . . while statements work exactly as they do in Java

```kotlin
fun main(args: Array<String>) { 
  var count = 0
  val finish = 5
  while (count++ < finish) { 
    println("counter = $count") 
  }
}
```
### for loops
```kotlin
  for (int i = 0; i < 10; i++) { 
    statements
  }
```

**Basic for Loop**
```kotlin
fun main(args: Array<String>) {
  val words = "The quick brown fox".split(" ")
  for(word in words) { 
    println(word)
  }
}
```

#### Ranges
If you need to work with numbers on the for loop, you can use Ranges. 
```kotlin
  var zeroToTen = 0..10
  if (9 in zeroToTen) println("9 is in zeroToTen")
```
**Using Ranges in for Loop**

```kotlin
fun main(args: Array<String>) { 
  for (i in 1..10) {
    println(i)
  }
}
```
### Exception Handling
Kotlin’s exception handling is very similar to Java: it also uses the try-catch-finally construct
```kotlin
fun main(args: Array<String>) {
  var fileReader: FileReader
  try {
    fileReader = FileReader("README.txt") var content = fileReader.read() println(content)
  }
  catch (ffe: FileNotFoundException) { 
    println(ffe.message)
  }
  catch(ioe: IOException) { 
    println(ioe.message)
  }
}
```
### Handling Nulls

Handling of null values is such a big concern in Java that Kotlin made a very deliberate decision to introduce the concept of a Nullable type.
```kotlin
var str: String = "Hello" 
str = null // won't work
```
To make a String (or any type) Nullable, we use the question mark symbol as postfix to the type, like
```kotlin
var str: String? = "Hello"
```
#### safe-call operator
It’s called the safe-call operator, which is written as the question mark symbol followed by a dot ?.
```kotlin
  arr?.forEach { i -> println(i) }
```
What the safe call does is to first check if arr is null; if it is, it won’t go through the forEach operation. 

**Safe Call Operator**
```kotlin
fun main(args: Array<String>) {
  var a = arrayOf(1,2,3)
  printArr(null)
}
fun printArr(arr: Array<Int>?) { 
    arr?.forEach { i -> println(i) }
}
```

### Chapter Summary

* Kotlin’s program elements are not that different from Java; it also has operators, blocks, statements, expressions, etc. In Kotlin, however, some constructs that are considered statements in Java are expressions in Kotlin, and some that were considered expressions in Java are statements in Kotlin (e.g., the assignment operation).
* Kotlin’s basic types are not the same as primitive types of Java. Everything in Kotlin is an object.
* There are two ways to declare a variable in Kotlin. When the var keyword is used, the variable is mutable. When the val keyword is used, the variable is immutable.
* Strings in Kotlin have iterators. Also, they’re easier to compose and combine with the help of template expressions.
* When variables are declared in Kotlin, they are by default non- Nullable, unless we declare them otherwise.
* Kotlin doesn’t have a switch statement, but it’s got a when construct.
* In Kotlin, we don’t have to write try-catch anymore because it basically uses unchecked Exceptions.
