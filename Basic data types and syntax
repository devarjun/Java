# Java Basics: Syntax, Data Types, and Control Structures

## Basic Syntax

### 1. Class Structure
Every Java program requires at least one class:

```java
public class HelloWorld {
    // Class body goes here
}
```

- `public`: Access modifier that makes the class accessible from any other class
- `class`: Keyword to define a class
- `HelloWorld`: Name of the class (should match the filename: HelloWorld.java)

### 2. Main Method
The entry point for execution in a Java application:

```java
public static void main(String[] args) {
    // Code to be executed goes here
}
```

- `public`: Access modifier
- `static`: Makes the method accessible without creating an object
- `void`: Return type (returns nothing)
- `main`: Method name
- `String[] args`: Command-line arguments passed as an array of strings

### 3. Statements and Expressions
- Statements are complete units of execution that end with a semicolon
- Expressions are combinations of variables, operators, and method calls that evaluate to a single value

```java
int sum = 5 + 3;  // Statement with an expression (5 + 3)
System.out.println("Hello, World!");  // Method call statement
```

### 4. Comments
Java supports three types of comments:

```java
// Single-line comment

/* 
   Multi-line comment
   spans multiple lines
*/

/**
 * Documentation comment (Javadoc)
 * Used to generate documentation
 * @author Your Name
 */
```

## Data Types

### 1. Primitive Data Types

Java has eight primitive data types:

| Data Type | Size    | Range                                                  | Default Value |
|-----------|---------|--------------------------------------------------------|---------------|
| `byte`    | 8 bits  | -128 to 127                                            | 0             |
| `short`   | 16 bits | -32,768 to 32,767                                      | 0             |
| `int`     | 32 bits | -2^31 to 2^31-1                                        | 0             |
| `long`    | 64 bits | -2^63 to 2^63-1                                        | 0L            |
| `float`   | 32 bits | ~±3.40282347E+38F (6-7 decimal digits precision)       | 0.0f          |
| `double`  | 64 bits | ~±1.79769313486231570E+308 (15 decimal digits precision)| 0.0d         |
| `char`    | 16 bits | 0 to 65,535 (represents Unicode characters)            | '\u0000'      |
| `boolean` | 1 bit   | true or false                                          | false         |

#### Examples:

```java
byte smallNumber = 127;
short mediumNumber = 32000;
int standardNumber = 2000000;
long largeNumber = 9223372036854775807L;  // Note the 'L' suffix
float decimalNumber = 3.14f;  // Note the 'f' suffix
double preciseDecimal = 3.14159265359d;  // 'd' suffix is optional
char singleCharacter = 'A';
boolean isTrue = true;
```

### 2. Reference Data Types

Reference types store references to objects and include:

#### a. Classes
```java
String message = "Hello, Java!";  // String is a class
Scanner input = new Scanner(System.in);  // Creating an object of Scanner class
```

#### b. Arrays
```java
int[] numbers = new int[5];  // Array of 5 integers
numbers[0] = 10;  // Assigning value to first element

String[] names = {"Alice", "Bob", "Charlie"};  // Array initialization
```

#### c. Interfaces
```java
List<String> list = new ArrayList<>();  // List is an interface, ArrayList is a class
```

#### d. Enums
```java
enum Day { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }
Day today = Day.MONDAY;
```

### 3. Type Casting

#### a. Implicit Casting (Widening)
```java
int intValue = 100;
long longValue = intValue;  // Automatic casting from int to long
float floatValue = longValue;  // Automatic casting from long to float
```

#### b. Explicit Casting (Narrowing)
```java
double doubleValue = 9.78;
int intValue = (int) doubleValue;  // Manual casting, intValue will be 9
```

### 4. Variables and Constants

#### a. Variable Declaration and Initialization
```java
int count;  // Declaration
count = 10;  // Initialization

int age = 25;  // Declaration and initialization in one step
```

#### b. Constants (using final keyword)
```java
final double PI = 3.14159;  // Cannot be changed after initialization
final String DATABASE_URL = "jdbc:mysql://localhost:3306/mydb";
```

