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

**equality operators** \
```==, !=``` \
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
```
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

```
var a = 100 // Int literal 
var b = 10L // Long literal
```
You can use underscores in numeric literals to make them more readable. This feature was introduced in Java 7 and its later versions.
```
var oneMillion = 1_000_000
var creditCardNumber = 1234_5678_9012_3456
```

Literals with decimal positions are automatically Doubles. To declare a float literal, use the F postfix, like
```
var a = 3.1416 // Double literal 
var b = 2.54 // Float literal
```
Every number type can be converted to any of the number types. That means all Double, Float, Int, Long, Byte, and Short types support the following member functions:
```
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
```
var enterKey = 'a'
```
Member Functions of the Character Type
```
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
```
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
```
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
