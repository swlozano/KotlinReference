# Collections and Arrays
Kotlin has some library functions like arrayOf, emptyArray, and arrayOfNulls that we can use to facilitate array creation.
## Arrays
```kotlin
//Using the emptyArray Function
var arr = emptyArray<String>(); 
arr += "1"
arr += "2"
arr += "3"
arr += "4" arr += "5"
```

```kotlin
//Using the arrayOfNulls Function
var arr2 = arrayOfNulls<String>(2) 
arr2.set(0, "1")
arr2.set(1, "2")
```

```kotlin
//Get and Set Methods of Array
var arr2 = arrayOfNulls<String>(2)
// arr2.set(0, "1") // arr2.set(1, "2")
arr2[0] = "1" 
arr2[1] = "2"
println(arr2[0]) // same as arr2.get(0) println(arr2[1])
````

```kotlin
//Using the arrayOf Function 
var arr4 = arrayOf("1", "2", "3")
````
Arrays can be created using the Array constructor. The constructor takes in two arguments, the first of which is the size of the array to be created and the second argument is a lambda function that can return an initial value of each element.
```kotlin
//Using the Array Constructor
var arr3 = Array<String>(5, {it.toString()})
```
The specialized classes like ByteArray, IntArray, ShortArray, and LongArray represent arrays of primitive types (like the ones in Java). These types let you work with arrays without the boxing and unboxing overhead of Arrays that uses the object counterparts
of the number primitives. 

```kotlin
//Special Array Types
var z = intArrayOf(1,2,3) 
var y = longArrayOf(1,2,3)
var x = byteArrayOf(1,2,3) 
var w = shortArrayOf(1,2,3)
println(Arrays.toString(z)) 
println(Arrays.toString(y)) 
println(Arrays.toString(x)) 
println(Arrays.toString(w))
```
I used the Arrays.toString() function so that we’ll get a human-readable output when printing the contents. If you simply print the array without the helper function, it looks like gibberish, like this
<br>
println(z) // outputs [Ljava.lang.String;@6ad5c04e

```kotlin
//Using a for Loop to Process Each Array Element
for (i in z) { 
    println("$i zee")
}
//Or you could use the forEach function, like so. 
y.forEach { i -> println("$i why") }
````

```kotlin
//Using the forEachIndexed Function to Traverse the Array
x.forEachIndexed { 
    index, element -> println("$index : $element")
}
```

## Collections

Collections Framework

![Image of Yaktocat](https://github.com/swlozano/KotlinReference/blob/7ca6e7011a8ae31a5887ef7966e27630cf06d0dd/Collectios%20Framework.png)

Kotlin doesn’t have a dedicated syntax for creating lists or sets, but it does provide us with library functions to facilitate creation. 

**Kotlin Collections and Their Creation Functions**
![Kotlin Collections and Their Creation Functions](https://github.com/swlozano/KotlinReference/blob/342ce04d6fb5be412fb35b4a95ed528298bddbb4/Kotlin%20Collections%20and%20Their%20Creation%20Functions.png)


## Lists

A list is a type of collection that has a specific iteration order. It means that if we added a couple of elements to the list, and then we stepped through it, the elements would come out in a very specific order—it’s the order by which they were added or inserted. They won’t come out in a random order or reverse chronology, but precisely in the sequence they were added. It implies that each element in the list has a placement order, an index number that indicates its ordinal position. The first element to be added will have its index at 0, the second will be 1, the third will be 2, and so on. So, just like an array, it is zero-based

```kotlin
//Basic Usage of Lists 
fun main(args: Array<String>) {
    val fruits = mutableListOf<String>("Apple") ➊ 
    fruits.add("Orange") ➋
    fruits.add(1, "Banana") ➌ 
    fruits.add("Guava")
    println(fruits) 
    // prints [Apple, Banana, Orange, Guava] 
    fruits.remove("Guava") ➍
    fruits.removeAt(2) ➎ 
    println(fruits.first() == "Strawberries") ➏
    println(fruits.last() == "Banana") ➐ 
    println(fruits) // prints [Apple, Banana]
}
```
➍ you can remove elements by name. When an element is removed, the element next to it will take its place. the ordinal position of all the elements that comes after it will change accordingly.<br>
➎ you can also remove elements by specifying its position on the list.<br>
➏ you can ask if the first() element is equal to “strawberries”.<br>
➐ you can also test if the last() element is equal to “Banana”.<br>


## Sets

Sets are very similar to lists, both in operation and in structure, so all of the things
we’ve learned about lists apply to sets as well. Sets differ from lists in the way they put constraints on the uniqueness of elements. They doesn’t allow duplicate elements or
the same elements within a set. It may seem obvious to many what the “same” means, but Kotlin, like Java, has a specific meaning for “sameness.” When we say that two objects are the same, it means that we’ve subjected the objects to a test for structural equality. Both Java and Kotlin define a method called equals(), which allows us to determine equivalence relationships between objects. This is generally what we mean by “sameness.” 

```kotlin
//Basic Usage for Sets
val nums = mutableSetOf("one", "two") ➊ 
nums.add("two") ➋ 
nums.add("two") ➌ 
nums.add("three") ➍
println(nums) // prints [one, two, three]
val numbers = (1..1000).toMutableSet() ➎ 
numbers.add(6)
numbers.removeIf { i -> i % 2 == 0 } ➏
println(numbers)
```

➊ Creates a mutable set and initializes it by passing a variable argument to the creator function. ➋ this doesn’t do anything. it won’t add “two” to the set because the element “two” is already in
the set. <br>
➌ no matter how many times you try to add “two,” the set will reject it because it already exists.<br>
➍ this, on the other hand, will be added because “three” doesn’t exist in the elements yet.<br>
➎ Creates a mutable set from a range. this is a handy way of creating a set (or a list) with many numeric elements.<br>
➏ this demonstrates how to use a lambda to remove all the even numbers in the set.<br>

## Maps
Unlike lists or sets, maps aren’t a collection of individual values; rather, they are a collection of pairs of values. Think of a map like a dictionary or a phone book. Its contents are organized using a key-value pair. For each key in a map, there is one and only one corresponding value. In a dictionary example, the key would be the term, and its value would be the meaning or the definition of the term.
The keys in a map are unique. Like sets, maps do not allow duplicate keys. However, the values in a map are not subjected to the same uniqueness constraints; two or more pairs in map may have the same value.

Basic Operations on a Map 
```kotlin
val dict = hashMapOf("foo" to 1) ➊
dict["bar"] = 2 ➋
val snapshot: MutableMap<String, Int> = dict ➌
snapshot["baz"] = 3 ➍
println(snapshot) ➎ 
println(dict) ➏ 
println(snapshot["bar"]) // prints 2 ➐
```

➊ Ca mutable map<br>
➋ adds a new key and value to the map<br>
➌ assigns the dict map to a new variable. this doesn’t create a new map. it only adds an object reference to the existing map.<br>
➍ adds another key-value pair to the map<br>
➎ prints {bar = 2, baz = 3, foo=1}<br>
➏ also prints {bar = 2, baz = 3, foo=1}, because both snapshot and dict points to the same map. ➐ Gets the value from the map using the key<br>

**Common Operations on Collections**
![Common Operations on Collections](https://github.com/swlozano/KotlinReference/blob/7c03bb4ec1b83dc4ee4f1fc8649cf342c15960eb/Common%20Operations%20on%20Collections.png)

## Collections Traversal

```kotlin
//Using while and for Loops for Collections
val basket = listOf("apple", "banana", "orange") 
var iter = basket.iterator()
while (iter.hasNext()) {
    println(iter.next()) 
}
for (i in basket) {
  println(i)
}
```
```kotlin
//Using forEach fruits.forEach { println(it) } ➊
nums.forEach { println(it) } ➋ // for maps
dict.forEach { println(it) } ➌
dict.forEach { t, u -> println("$t | $u") } ➍
```
➊ the lambda expression of the forEach has an implicit it parameter. the it parameter is the value of the current element. What this statement means is for each item in fruits, do what’s inside the lambda, which in our case is just println().<br>
➋ same thing works for sets<br>
➌ same thing works for maps<br>
➍ this is a variation of bullet 3 above, but this one allows us to work with the key and value separately.<br>

## Filter and Map

```kotlin
//filter
val ints = (1..100).toList()
val evenInts = ints.filter { it % 2 == 0 }
```
```kotlin
//Using the Map Function
val squaredInts = evenInts.map { it * it}
println("Sum of squares of even nos <= 100 is ${squaredInts.sum()}")
````
