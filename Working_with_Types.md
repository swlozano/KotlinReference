# Working with Types
## Interfaces

The basic form of an interface in Kotlin, like in Java
```kotlin
interface Fax {
  fun call(number: String) = println("Calling $number") 
  fun print(doc: String) = println("Fax:Printing $doc") 
  fun answer()
}
```

What’s remarkable about Kotlin interfaces are that they can (1) contain properties and (2) have functions with implementations—in other words, concrete functions. 

**class MultiFunction Implementing Fax**
```kotlin
class MultiFunction : Fax { 
  override fun answer () {  }
}
```
```kotlin
interface A {
  fun foo() {
    println("A:foo") 
  }
}
interface B {
  fun foo() {
    println("B:foo") 
   }
}
class Child : A, B {
  override fun foo () {
    println("Child:foo") 
   }
}
fun main(args: Array<String>) { 
  var child: Child = Child() 
  child.foo()
}
```
## Invoking Super Behavior
Like Java, Kotlin’s functions can call the functions of its supertype if it has an implementation. Also, like in Java, Kotlin uses the super keyword to accomplish this. The super keyword in Kotlin means the same as it did in Java—it’s a reference to the instance of the supertype. To invoke a function on a supertype, you’ll need three things: (1) the super keyword; (2) name of the supertype enclosed in a pair of angle brackets; and (3) the name of function you want to invoke on the supertype. It looks something like the code snippet here:

```kotlin
super<NameOfSuperType>.functionName()
```

**Printable, Fax, and MultiFunction**
```kotlin
interface Printable {
  fun print(doc:String) = println("Printer:Printing $doc")
}
interface Fax {
  fun call(number: String) = println("Calling $number") 
  fun print(doc: String) = println("Fax:Printing $doc") 
  fun answer() = println("answering")
}
class MultiFunction : Printable, Fax {
  override fun print(doc:String)  {
    println(“Multifunction: printing”)
  } 
}
```
**MultiFunction, Calling Functions on Supertype**
```kotlin
class MultiFunction : Printable, Fax {
    override fun print(doc:String) { 
      super<Fax>.print(doc) 
      super<Printable>.print(doc) 
      println("Multifunction: printing")
  } 
}
```
**MultiFunction, Printable, and Fax**
```kotlin
interface Printable {
  fun print(doc:String) = println("Printer:Printing $doc")
}
interface Fax {
  fun call(number: String) = println("Calling $number") 
  fun print(doc: String) = println("Fax:Printing $doc") 
  fun answer() =      println("answering")
}
class MultiFunction : Printable, Fax {
  override fun print(doc:String) { 
    super<Fax>.print(doc) 
    super<Printable>.print(doc) 
    println("Multifunction: printing")
  } 
}
fun main(args: Array<String>) { 
  val mfc = MultiFunction() 
  mfc.print("The quick brown fox") 
  mfc.call("12345")
}
```


