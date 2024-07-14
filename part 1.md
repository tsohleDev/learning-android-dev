# Part 1: Kotlin Basics

## 1. Variables -> val vs var

In Kotlin, variables are defined using either `val` or `var`. It is recommended to explicitly specify the data type for clarity.

- `val` (value): Immutable reference. Once a value is assigned to a `val` variable, it cannot be changed. It is similar to `final` in Java.
  ```kotlin
  val x: Int = 10
  // x = 20 // Error: Val cannot be reassigned
  ```
- `var` (variable): Mutable reference. The value of a `var` variable can be changed.
  ```kotlin
  var y: Int = 10
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
      in 3..10 -> print("x is between 3 and 10")
      is String -> print("x is a String")
      else -> print("x is neither 1 nor 2 and is not between 3 and 10")
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

Kotlin classes are more concise and expressive compared to Java. Here are some key features:

- Class declaration: By default, classes are `final` in Kotlin. To make them inheritable, use the `open` keyword.
  ```kotlin
  open class Person(val name: String, var age: Int)
  ```

- Primary constructor: Defined in the class header.
  ```kotlin
  class Person(val name: String, var age: Int)
  ```

- Secondary constructor: Defined inside the class body.
  ```kotlin
  class Person(val name: String) {
      var age: Int = 0

      constructor(name: String, age: Int) : this(name) {
          this.age = age
      }
  }
  ```

- Inheritance: Uses the `:` symbol and calls the superclass constructor.
  ```kotlin
  class Student(name: String, age: Int, val studentId: String) : Person(name, age)
  ```

- Properties: Can have custom getters and setters.
  ```kotlin
  var name: String = "John"
      get() = field.toUpperCase()
      set(value) {
          field = value.trim()
      }
  ```
```

This Markdown file now includes more detailed explanations on variable data types and the use of `when` statements with multiple values, `is`, and `in` keywords.# Part 1: Kotlin Basics

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

Kotlin classes are more concise and expressive compared to Java. Here are some key features:

- Class declaration: By default, classes are `final` in Kotlin. To make them inheritable, use the `open` keyword.
  ```kotlin
  open class Person(val name: String, var age: Int)
  ```

- Primary constructor: Defined in the class header.
  ```kotlin
  class Person(val name: String, var age: Int)
  ```

- Secondary constructor: Defined inside the class body.
  ```kotlin
  class Person(val name: String) {
      var age: Int = 0

      constructor(name: String, age: Int) : this(name) {
          this.age = age
      }
  }
  ```

- Inheritance: Uses the `:` symbol and calls the superclass constructor.
  ```kotlin
  class Student(name: String, age: Int, val studentId: String) : Person(name, age)
  ```

- Properties: Can have custom getters and setters.
  ```kotlin
  var name: String = "John"
      get() = field.toUpperCase()
      set(value) {
          field = value.trim()
      }
  ```
