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




