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
## Inheritance
Kotlin classes are final by default, as opposed to Java classes that are “open” or non-final
<br>
```kotlin
//won’t compile because the Person class is final.
class Person {
}
class Employee : Person() {
}
```
Shows the Person class again, but this time, it has the open modifier, which signifies that class Person can be extended.
**Person and Employee**
```kotlin
class open class Person {
}
class Employee : Person() {
}
```

The behavior of being final as a default behavior isn’t just for classes; member functions are like that too in Kotlin. When a function is written without the open modifier, it is final.

**Method Overriding**

```kotlin
open class Person(_name:String) {
  val name = _name
  open fun talk() { ➊ 
    println("${this.javaClass.simpleName} talking")
  } 
}
class Employee(_name:String, _empid:String = "1001") : Person(_name) { 
  val empid = _empid
  override fun talk() { ➋ 
    super.talk() ➌ 
    println("Hello")
  }
  override fun toString():String{ ➍ 
    return "name: $name | id: $empid"
  } 
}
```
➊ Functions need to be specifically marked as open so that they can be overridden by subtypes.
<br>
➋ subtypes need to mark the function with the override keyword in order to make it polymorphic. IntelliJ is smart enough to prevent compilation from happening when it senses that you are defining a function on the subtype that has an exact signature on the supertype without using the override keyword.
<bR>
➌ We can call the super behavior from here; this effectively invokes the talk() function in class Person.
  <br>
➍ We’re overriding the toString() function. This behavior was inherited from the Person class, which in turn it inherited from class Any. You can think of class Any as the analog for the java. lang.Object.

**How to Make a Function Final, Again**

```kotlin
open class Person(_name:String) {
  val name = _name
  open fun talk() { 
    println("${this.javaClass.simpleName} talking")
  } 
}
open class Employee(_name:String, _empid:String = "1001") : Person(_name) { 
  val empid = _empid
  override fun talk() {
    super.talk()
    println("Employee overriding talk()")
  }
  final override fun toString():String{ ➊ 
    return "name: $name | id: $empid"
  } 
}
class Programmer(_name:String) : Employee(_name) { 
  override fun talk() { ➋
    super.talk()
    println("Programmer overriding talk()") 
  }
}
```
➊ seeing the final and override keyword on the same line does seem a bit odd, but it’s perfectly legal. What it means is that we are overriding the function and at the same time “closing” it for further inheritance. The final keyword in this function affects only subtypes of the employee class, but not the employee class itself.
  <br>
➋ This won’t compile anymore.

## Properties

  A property in a class or object is traditionally created by defining a member variable and providing accessor methods for it. These methods will usually follow some naming conventions where the name of the member variable will be prefixed by get and set.

**Person class With a Single Property**
 ```kotlin
class Person(_name:String) { ➊ 
  val name:String = _name ➋
}
fun main(args: Array<String>) {
  var person = Person("John Smith") 
  println(person.name) ➌
}
```  
➊ a constructor takes in a parameter. This allows us to set the name of the object at the point of creation.<br>
➋ We have access to parameters from via the constructor from here.<br>
➌ This may look like we are directly accessing the name member variable, but we are not. This
actually calls the get accessor method.<br>

  
**Simplified Person class**
```kotlin
class Person(val name:String)
fun main(args: Array<String>) {
  var person = Person("John Smith") 
  println(person.name)
}
```
The code here is the most concise way of defining a property in Kotlin. It’s also considered idiomatic. Notice the changes we made in the code:<br>
1. The parameter in the primary constructor now has a val declaration. This effectively makes the constructor parameter a property. We could have used var, and it would work just as well.<br>
2. We no longer need to differentiate the identifier in the constructor parameter with the member variable; hence we dropped the leading underscore in the _name variable.<br>
3. We can drop the entire body of the class since we don’t need
it anymore. The class body only contains the code to transfer
the value of the constructor parameter to the member variable. Since Kotlin will automatically define a backing field for the constructor parameter, we don’t have to do anything anymore in the class body.<br>

The code shows the most basic way to define data objects in Kotlin (Java programmers refer to them as POJOs or plain old java object). By simply using either val or var in the primary constructor parameters, we can automagically define properties with proper mutator methods.
  
### “getting” and “setting”
1. Declare the property in the body of the class, not in the primary constructor.<br>
2. Provide getter and setter methods in the class body.<br>
The full syntax for declaring a property is as follows:<br>

```kotlin
var <property name>:[<property type>][=<initializer>] [<getter>]
[<setter>]
``` 

**Custom Accessor Methods**

  ```kotlin
class Employee {
  var name: String = "" ➊
  get() { ➋
    Log("Getting lastname") ➌ 
    return field ➍
  }
  set(value) { ➎
    Log("Setting value of lastname")
    field = value ➏ 
  }
}
fun Log(msg:String) {
  println(msg)
}
fun main(args: Array<String>) { 
  var emp = Employee()
  emp.name = "John Doe" ➐ 
  println(emp.name) ➑
}
  ```
 ➊ We declare and define the property inside the class body, instead of capturing it as parameter in the primary constructor. We initialize it to an empty string first.<br>
➋ The syntax for get() looks a lot like the syntax for defining a function, except we don’t write the fun keyword before it.<br>
➌ This is where you write your custom code. This statement will be executed every time someone tries to access the name property.<br>
➍ The field keyword is a special one. It refers to the backing field, which kotlin automatically provides when we define a property called name. The name member variable isn’t a simple variable; kotlin makes an automatic backing field for it, but we don’t have direct access to that variable. We can, however, access it via the field keyword, like what we did here.<br>
➎ The value parameter corresponds to the value that will be assigned to the property after the employee object has been created (see bullet ➐).<br>
➏ after we’ve performed our custom logic, we can now set the value of the field. ➐ This will trigger our set accessor logic, see bullet ➎.<br>
➑ This will trigger our get accessor logic, see bullet ➋.<br>
 
**This is the wrong way to code getter and setter for properties.**
```kotlin
 class Employee {
  var name: String = ""
  get() {
    Log("Getting lastname") 
    return this.name ➊
   }
   set(value) {
    Log("Setting value of lastname")
    this.name = value ➋ 
  }
}
 ```
➊ ➋ This results in a recursive call, which will eventually throw StackOverflowError.<br>
The expression this.name doesn’t really access the member variable name. Instead, it calls the default accessor methods that Kotlin provides automatically when you define a property for the class

## Data Classes
we’ve seen how easily we can create the analog of POJOs in Kotlin<br>
**Comparing Two Employee Objects**
```kotlin 
class Employee(val name:String)
fun main(args: Array<String>) {
  val e1 = Employee("John Doe") 
  val e2 = Employee("John Doe")
  println(e1 == e2) // output is false 
}
```
To resolve this, we can override the equals() method and provide an implementation on how to compare Employee objects.
<br>
  Overriding the hashCode() and equals() Functions
 ```kotlin 
import java.util.*
class Employee(val name:String){
  override fun equals(obj:Any?):Boolean { ➊
    var retval = false 
    if(obj is Employee) { ➋
      retval = name == obj.name ➌ 
    }
    return retval
  }
  override fun hashCode(): Int { ➍ 
    return Objects.hash(name)
  } 
}
fun main(args: Array<String>) {
  val e1 = Employee("John Doe") 
  val e2 = Employee("John Doe")
  println(e1) ➎
  println(e1 == e2) ➏ 
}
  ```
➊ The equals() function in class Any is open, we can override it.<br>
➋ We check first if we are comparing an Employee object to another Employee object. The is keyword performs two functions: (1) it checks if obj is actually an instance of Employee, and (2) it automatically casts obj to an Employee object.<br>
➌ Obj is automatically casted to an Employee object. The is keyword already did that. now, we can safely compare the name member variables of the two objects.<br>
➍ Overriding the hashCode() function is usually needed if you intend to store this object in collections where comparisons of hash code is material (e.g., HashSet, HashMap, etc.). For our small example, it’s not necessary. But it’s a good practice to override the hashCode() function whenever you override the equals() function.<br>
➎ Invokes the toString() function of the Employee object. The toString() function is found on the supertype Any. The default implementation of toString() gives us an output of something like this "employee@ae805cc4".<br>
➏ now, this prints "true". <br>

While we can still do these things in Kotlin, we don’t have to. The only thing we need to do in Kotlin is to make Employee a data class.<br>
**Employee Data Class**
```kotlin
data class Employee(val name:String) ➊
fun main(args: Array<String>) { 
   val e1 = Employee("John Doe") 
  val e2 = Employee("John Doe")
  println(e1) ➋
  println(e1 == e2) ➌ 
 }
 ```
➊ To make any class in kotlin a data class, just use the keyword data on the class declaration.<br>
➋ We get an added bonus of a nicer toString() output with data classes. This one now prints “employee(name=John Doe)”.<br>
➌ also, the equals() comparison returns true.  <br>

##  Visibility Modifiers
The keywords public, private, and protected mean exactly the same in Kotlin as they do in Java. But, the default visibility is where the difference lies. In Kotlin, whenever you omit the visibility modifier, the default visibility is public.
<br>
Kotlin introduces the internal keyword, which means it is visible in a module. A module is simply a collection of files, it can be (1) an IntelliJ module or project; (2) an Eclipse project; (3) a Maven project; or (4) a Gradle project.

 Class marked as internal, which makes it visible only in classes and top-level functions that are within the same module and whose visibility are also marked internal.

```kotlin
internal open class Foo {
  internal fun boo() = println("boo") 
  internal fun doo() = println("doo")
}
internal fun Foo.bar() { 
  boo()
  doo() 
}
fun main(args: Array<String>) { 
   var fu = Foo()
  fu.bar()
}
```
## Access Modifiers  
The access modifiers of Kotlin are: <i>final, open, abstract, and override.</i> <br>
They affect inheritance. <br>
The abstract keyword has the same meaning in Kotlin as it does in Java. It’s applicable to classes and functions.
When you mark a class as abstract, it becomes implicitly open as well, so you don’t need to use the open modifier, it becomes redundant.<br> 
Interfaces don’t need to be declared as abstract and open, since they are implicitly, already, abstract and open.
  
## Object Declarations  
Java’s static keyword did not make the cut in Kotlin’s list of keywords. <br>
There is no static equivalent in Kotlin; in its place, Kotlin introduces the object and companion keywords.<br>
The object keyword allows us to define both a class and its instance all at the same time. More specifically, it defines only a single instance of that class, which makes this keyword a good way to define singletons in Kotlin.  

**Using the Object Keyword to Define a Singleton**
```kotlin  
object Util {
  fun foo() = println("foo")
}
fun main(args: Array<String>) { 
  Util.foo() // prints "foo"
}
```
We substitute the object keyword in place of the class keyword<br>
Object declarations can contain most of the things you can write in class, like initializers, properties, functions, and member variables. The only thing you cannot write inside an object declaration is a constructor.<br>

Initializers, Properties, Functions, and Member Variables in Object Declarations
```kotlin
object Util { 
  var name = ""
  set(value) { 
    field = value
  }
  init {
    println("Initializing Util")
  }
  fun foo() = println(name) 
}
fun main(args: Array<String>) { 
  Util.name = "Bar"
  Util.foo() // prints "Bar"
}  
```

