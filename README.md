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

