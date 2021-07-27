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
## Classes
A class is defined using (1) the class keyword; (2) an identifier, which will be its name; (3) an optional header; and (4) an optional body. 

```kotlin
class Person() {
}
```

The header of the class is the pair of parentheses. The header may contain parameters. <br>
The pair of curly braces comprises the body of the class. Both the header and the class body are optional.<br>
To instantiate the Person class, we can write something like the following:
```kotlin
var person = Person()
// The pair of parentheses after the type name (Person) is a call to a no-arg constructor (ctor).
```
## Constructors
Kotlin classes can have more than one constructor in their definitions. 
<br>
A primary ctor is written on the header part of the class.
<br> 
A secondary ctor(s) are written in the body.

```kotlin
class Person constructor(_name: String) { ➊ 
  var name:String ➋
  init { ➌
    name = _name ➍ 
  }
}
```
➌ This is an initializer block that is similar to Java’s initializer. This gets executed whenever an instance of a class is created. You can have more than one initializer block in your class, and when that happens, initializers will be executed in the order they were defined in the class. an initializer block is a pair of curly braces prefixed by the keyword init You would normally use them when the only constructor you have is a primary constructor, because primary constructors cannot contain any code (whether statement or expressions).<br>
➍ We can access arguments that were passed to the primary ctor from an initializer block.
<br>
When the primary ctor doesn’t have (or need) annotations or visibility modifiers, we
can omit the constructor keyword, like so:
```kotlin
class Person (_name: String) {
  var name:String
  init {
    name = _name 
   }
}
```
We can further simplify and shorten the code by joining the init block and declaration of the name variable in a statement. Kotlin is smart like that.
```kotlin
class Person (_name: String) { 
  var name:String = _name
}
```
### Secondary constructors
**Employee Class, with Secondary Constructor**


```kotlin
class Employee {
  var name:String
  constructor(_name: String) {
    name = _name 
   }
}
```
we didn’t have to use the init block because the initialization of the name member variable was done in constructor body. A secondary ctor, unlike a primary ctor, can contain code.

**class Employee, with Two Secondary Constructors**
```kotlin
class Employee {
  var name:String = "" ➊ 
  var empid:String = ""
  constructor(_name: String) : this(_name, "1001") ➋ 
  constructor(_name:String, _id: String) { ➌
    name = _name
    empid = _id 
   }
}
```

➊ We have to initialize our member variables because kotlin won’t be able to tell what we are doing the initialization.
<br>
➋ a secondary constructor needs to have the constructor keyword. This ctor doesn’t have a body; it’s okay to write it like that. Furthermore, this ctor invokes another ctor—one that accepts two arguments.
<br>
➌ another secondary constructor is defined for the employee class. This one takes in two parameters: a name and an employee id.
<br>
**Simplified Employee class**
```kotlin
class Employee (_name:String, _empid:String = "1001") { 
  val name = _name
  val empid = _empid
}
```
