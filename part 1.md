# Part 1: Kotlin Basics

## 1. Variables -> val vs var

In Kotlin, variables are defined using either `val` or `var`.

- `val` (value): Immutable reference. Once a value is assigned to a `val` variable, it cannot be changed. It is similar to `final` in Java.
```kotlin
  val x = 10
  // x = 20 // Error: Val cannot be reassigned
```
- `var` (variable): Mutable reference. The value of a `var` variable can be changed.
```kotlin
  var y = 10
  y = 20 // No Error: Var can be reassigned
```

## 2. Conditionals

Kotlin provides several ways to handle conditional logic, including `if`, `when`, and the Elvis operator (`?:`).

- `if`: Works like in most programming languages. It can be used as an expression to return a value.
```kotlin
  val a = 10
  val b = 20
  val max = if (a > b) a else b
```

- `when`: Acts as a more powerful `switch` statement. It can handle multiple conditions and types.
  ```kotlin
  when (x) {
      1 -> print("x is 1")
      2 -> print("x is 2")
      else -> print("x is neither 1 nor 2")
  }
  ```

- Elvis operator (`?:`): Used to provide a default value if an expression evaluates to `null`.
```kotlin
  val name: String? = null
  val length = name?.length ?: 0
```

## 3. Nullity

Kotlin aims to eliminate the NullPointerException (NPE) by introducing nullable and non-nullable types.

- Non-nullable types: Cannot hold `null` values.
```kotlin
  var nonNullString: String = "Hello"
  // nonNullString = null // Error: Null can not be a value of a non-null type String
```

- Nullable types: Can hold `null` values. Declared by appending `?` to the type.
```kotlin
  var nullableString: String? = "Hello"
  nullableString = null // No Error
```

- Safe call operator (`?.`): Calls methods or accesses properties safely on nullable types.
  ```kotlin
  val length = nullableString?.length // Returns null if nullableString is null
  ```

- The `!!` operator: Asserts that a nullable type is not `null`. Throws an NPE if the value is `null`.
  ```kotlin
  val length = nullableString!!.length // Throws NullPointerException if nullableString is null
  ```

## 4. Classes

Kotlin classes can have two types of constructors: **Primary Constructor** and **Secondary Constructor**, the primary constroctor is used to pass
in parameters **only** in creating a object, these parameters them become properties of the class, therefore one can also declare their visibility 
```kotlin
// Primary Constructor
class SmartDevice(val name: String, private val category: String) {

    var deviceStatus = "online"

    // Secondary Constructor
    constructor(name: String, category: String, statusCode: Int) : this(name, category) {
        deviceStatus = when (statusCode) {
            0 -> "offline"
            1 -> "online"
            else -> "unknown"
        }
    }

    fun turnOn() {
        println("Smart device is turned on.")
    }

    fun turnOff() {
        println("Smart device is turned off.")
    }
}

```

Kotlin has diffferrent **access modifiers**

|Modifier|Accessible in same class|Accessable in subclass|Accessable in same module|Accessable outside module|
|Private|x|-|-|-|
|protected|x|x|-|-|
|internal|x|x|x|-|
|public|x|x|x|x|

I guess you want to know what is a module?, a module is 

Inheritance: Uses the `:` symbol and calls the superclass constructor.

```kotlin
  class Student(name: String, age: Int, val studentId: String) : Person(name, age)
```

Properties: Can have custom getters and setters.

```kotlin
  var name: String = "John"
      get() = field.toUpperCase()
      set(value) {
          field = value.trim()
      }
```

kotlin also makes it easy for a developer to implement the **delegation** design pattern, we should probably talk about design patterns, maybe **part 3/4** 

```kotlin
    var name by X
    //where X is the delegate object
```

A delegate is implimented through an **interface**,
so depending weather its a **var i.e read and write** or **val i.e readonly** 
it has to implement the `ReadWriteProperty` interface or `ReadOnlyProperty` interface respectively

```kotlin

class RangeRegulator(
    initialValue: Int,
    private val minValue: Int,
    private val maxValue: Int
) : ReadWriteProperty<Any?, Int> {

    var fieldData = initialValue

    override fun getValue(thisRef: Any?, property: KProperty<*>): Int {
        return fieldData
    }

    override fun setValue(thisRef: Any?, property: KProperty<*>, value: Int) {
        if (value in minValue..maxValue) {
            fieldData = value
        }
    }
}
```

and to implement it you would instatiate it in the class using the syntax

```kotlin
    private var brightnessLevel by RangeRegulator(initialValue = 0, minValue = 0, maxValue = 100)
```

## 5 Lambda Functions

Lambda functions formally known as **fuctional pointers** from the c world, the concept of storing pointers to functions seems silly
but it is quite use full, it allows us to implement whats called **call backs**, where you can pass in a function or return a function as long as the signature of that function
is the same as the one defined to be "called back". this concept allows code to be dynamic at runtime and DRY without if else statements, because we hate if else statements, we really do!

so you can you store a function in a variable using **lambda syntax** or **function reference operator**, the difference is if you had already defined a `fun` and you want to store it in a variable
you would use use the function reference operator `::` otherwise you would use the lambda

```kotlin
// function refence operator
fun sayHi() {
    println("Hi")
}

val hi = ::sayHi
```

Now with lambdas the synax can get abit overwhealming but ideally your lambda would be short simple primary fuctions

```kotlin
val sayHi: () -> Unit = { println("Hi") }
            or
val sayHi: (String) -> Int = { it.length }
            or
val add: (Int, Int) -> Int = { a,b -> a + b }
            or
val x: () -> (int, Int) -> int { add }
```
Note that `Unit` is similar to `void` in C and if you have only one parameter it automatically gets the `it` keyword, and if you have more than one parameter you name them arbitarly. 

and you can also return and take in lambdas as arguments

in calling functions that have lamdas as parameter you can pass the lambda literally with or without trailing lamda syntax

```kotlin
fun performOperation(x: Int, operation: (Int) -> Int): Int {
    return operation(x)
}

// without trailing lambda syntax
val result1 = performOperation(5, { it * 2 })

// with trailing lambda syntax
val result2 = performOperation(5) { it * 2 }
```
