# Java Methods, Exception Handling, and File I/O

## Table of Contents
- [Methods](#methods)
  - [Method Declaration](#method-declaration)
  - [Method Parameters](#method-parameters)
  - [Return Types](#return-types)
  - [Method Overloading](#method-overloading)
  - [Recursion](#recursion)
  - [Variable Arguments (Varargs)](#variable-arguments-varargs)
  - [Method References](#method-references)
- [Exception Handling](#exception-handling)
  - [Exception Hierarchy](#exception-hierarchy)
  - [Try-Catch Blocks](#try-catch-blocks)
  - [Multiple Catch Blocks](#multiple-catch-blocks)
  - [Finally Block](#finally-block)
  - [Try-With-Resources](#try-with-resources)
  - [Throwing Exceptions](#throwing-exceptions)
  - [Creating Custom Exceptions](#creating-custom-exceptions)
  - [Exception Propagation](#exception-propagation)
  - [Best Practices](#best-practices)
- [File I/O](#file-io)
  - [File Handling Basics](#file-handling-basics)
  - [Character Streams](#character-streams)
  - [Byte Streams](#byte-streams)
  - [Buffered Streams](#buffered-streams)
  - [Reading and Writing Text Files](#reading-and-writing-text-files)
  - [Reading and Writing Binary Files](#reading-and-writing-binary-files)
  - [File and Directory Operations](#file-and-directory-operations)
  - [NIO.2 (Java 7+)](#nio2-java-7)
  - [Serialization](#serialization)

## Methods

Methods in Java are blocks of code that perform specific tasks. They help in code organization, reusability, and modular programming.

### Method Declaration

A method declaration consists of several components:

```java
[access_modifier] [static] [final] return_type method_name([parameters]) [throws exceptions] {
    // Method body
    [return statement];
}
```

Example:
```java
public static int addNumbers(int a, int b) {
    return a + b;
}
```

Components explained:
- **Access Modifier**: Controls the visibility (public, private, protected, or default)
- **Static**: Indicates the method belongs to the class rather than instances
- **Final**: Prevents method overriding in subclasses
- **Return Type**: Data type of the value returned (or void if nothing is returned)
- **Method Name**: Identifier for the method (follows camelCase convention)
- **Parameters**: Input values the method accepts
- **Throws Clause**: Declares exceptions that method might throw
- **Method Body**: Code to be executed
- **Return Statement**: Returns a value to the caller (not needed for void methods)

### Method Parameters

Methods can accept different types of parameters:

#### 1. Primitive Type Parameters
Passed by value (a copy is created):

```java
public void incrementNumber(int number) {
    number++;  // Only modifies the local copy
}

// Usage
int x = 5;
incrementNumber(x);
System.out.println(x);  // Still outputs 5
```

#### 2. Reference Type Parameters
Passed by reference value (the reference is copied, but points to the same object):

```java
public void modifyList(List<String> list) {
    list.add("New Item");  // Modifies the actual list
}

// Usage
List<String> myList = new ArrayList<>();
modifyList(myList);
System.out.println(myList.size());  // Outputs 1
```

#### 3. Final Parameters
Cannot be reassigned within the method:

```java
public void processData(final int id, final String name) {
    // id = 10;  // Would cause a compilation error
    // Process data using id and name
}
```

### Return Types

Methods can return different types of values:

#### 1. Primitive Return Types

```java
public int add(int a, int b) {
    return a + b;
}

public boolean isEven(int number) {
    return number % 2 == 0;
}
```

#### 2. Reference Return Types

```java
public String createGreeting(String name) {
    return "Hello, " + name + "!";
}

public List<Integer> getEvenNumbers(int max) {
    List<Integer> evens = new ArrayList<>();
    for (int i = 2; i <= max; i += 2) {
        evens.add(i);
    }
    return evens;
}
```

#### 3. Void Return Type
Methods that don't return a value:

```java
public void printMessage(String message) {
    System.out.println(message);
    // No return statement needed
}
```

### Method Overloading

Method overloading allows multiple methods with the same name but different parameter lists:

```java
public int add(int a, int b) {
    return a + b;
}

public int add(int a, int b, int c) {
    return a + b + c;
}

public double add(double a, double b) {
    return a + b;
}
```

The Java compiler determines which method to call based on:
1. Number of parameters
2. Types of parameters
3. Order of parameters

Note: Return type alone is not sufficient for method overloading.

### Recursion

Recursion is when a method calls itself:

```java
public int factorial(int n) {
    // Base case
    if (n <= 1) {
        return 1;
    }
    // Recursive case
    return n * factorial(n - 1);
}
```

Components of a recursive method:
1. **Base case**: Condition to stop recursion
2. **Recursive case**: Calling the method with a modified argument
3. **Progress toward base case**: Ensuring the recursion eventually terminates

Example: Fibonacci sequence
```java
public int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

### Variable Arguments (Varargs)

Variable arguments allow a method to accept a variable number of arguments:

```java
public int sum(int... numbers) {
    int total = 0;
    for (int num : numbers) {
        total += num;
    }
    return total;
}

// Usage
int result1 = sum(1, 2);           // Passes 2 arguments
int result2 = sum(1, 2, 3, 4, 5);  // Passes 5 arguments
int result3 = sum();               // Passes 0 arguments
```

Rules for varargs:
1. Only one vararg parameter is allowed per method
2. The vararg parameter must be the last parameter
3. Internally, varargs are treated as arrays

Example with mixed parameters:
```java
public void displayInfo(String name, int... scores) {
    System.out.println("Name: " + name);
    System.out.println("Scores: " + Arrays.toString(scores));
}

// Usage
displayInfo("Alice", 95, 87, 92);
```

### Method References

Java 8 introduced method references as a shorthand for lambda expressions:

```java
// With lambda expression
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));

// With method reference
names.forEach(System.out::println);
```

Types of method references:
1. **Static method reference**: `ClassName::staticMethodName`
2. **Instance method reference of a particular object**: `objectReference::instanceMethodName`
3. **Instance method reference of an arbitrary object of a particular type**: `ClassName::instanceMethodName`
4. **Constructor reference**: `ClassName::new`

Examples:
```java
// Static method reference
List<String> numbers = Arrays.asList("1", "2", "3");
List<Integer> parsed = numbers.stream()
                             .map(Integer::parseInt)
                             .collect(Collectors.toList());

// Instance method reference of a particular object
String prefix = "User: ";
List<String> userNames = names.stream()
                             .map(prefix::concat)
                             .collect(Collectors.toList());

// Instance method reference of arbitrary object
List<String> sortedNames = names.stream()
                               .sorted(String::compareToIgnoreCase)
                               .collect(Collectors.toList());

// Constructor reference
List<Person> people = names.stream()
                          .map(Person::new)
                          .collect(Collectors.toList());
```

