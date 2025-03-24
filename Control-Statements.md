## Control Structures

### 1. Conditional Statements

#### a. if Statement
The `if` statement executes a block of code if a specified condition is true.

```java
if (condition) {
    // Code to execute if condition is true
}
```

Example:
```java
int age = 18;
if (age >= 18) {
    System.out.println("You are an adult.");
}
```

#### b. if-else Statement
Provides an alternative execution path when the condition is false.

```java
if (condition) {
    // Code to execute if condition is true
} else {
    // Code to execute if condition is false
}
```

Example:
```java
int score = 75;
if (score >= 60) {
    System.out.println("You passed.");
} else {
    System.out.println("You failed.");
}
```

#### c. if-else-if Ladder
Used for multiple conditions.

```java
if (condition1) {
    // Code if condition1 is true
} else if (condition2) {
    // Code if condition2 is true
} else if (condition3) {
    // Code if condition3 is true
} else {
    // Code if all conditions are false
}
```

Example:
```java
int score = 85;
if (score >= 90) {
    System.out.println("Grade: A");
} else if (score >= 80) {
    System.out.println("Grade: B");
} else if (score >= 70) {
    System.out.println("Grade: C");
} else if (score >= 60) {
    System.out.println("Grade: D");
} else {
    System.out.println("Grade: F");
}
```

#### d. Nested if Statements
An if statement inside another if statement.

```java
if (outerCondition) {
    // Outer if code
    if (innerCondition) {
        // Inner if code
    }
}
```

Example:
```java
int age = 25;
boolean hasLicense = true;

if (age >= 18) {
    if (hasLicense) {
        System.out.println("You can drive.");
    } else {
        System.out.println("You need to get a license first.");
    }
} else {
    System.out.println("You are too young to drive.");
}
```

#### e. switch Statement
Tests a variable against multiple values.

```java
switch (expression) {
    case value1:
        // Code for value1
        break;
    case value2:
        // Code for value2
        break;
    // More cases...
    default:
        // Default code (optional)
}
```

Example:
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    case 6:
        System.out.println("Saturday");
        break;
    case 7:
        System.out.println("Sunday");
        break;
    default:
        System.out.println("Invalid day");
}
```

Enhanced switch (Java 12+):
```java
switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    case 3 -> System.out.println("Wednesday");
    case 4 -> System.out.println("Thursday");
    case 5 -> System.out.println("Friday");
    case 6, 7 -> System.out.println("Weekend");
    default -> System.out.println("Invalid day");
}
```

### 2. Looping Statements

#### a. for Loop
Used when you know how many times you want to execute a block of code.

```java
for (initialization; condition; update) {
    // Code to be executed in each iteration
}
```

Example:
```java
for (int i = 0; i < 5; i++) {
    System.out.println("Count: " + i);
}
```

#### b. Enhanced for Loop (for-each)
Simplifies iterating over arrays and collections.

```java
for (elementType element : collection) {
    // Code using element
}
```

Example:
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println("Number: " + num);
}
```

#### c. while Loop
Executes a block of code as long as a condition is true.

```java
while (condition) {
    // Code to be executed
}
```

Example:
```java
int count = 0;
while (count < 5) {
    System.out.println("Count: " + count);
    count++;
}
```

#### d. do-while Loop
Similar to while loop, but guarantees that the code block executes at least once.

```java
do {
    // Code to be executed
} while (condition);
```

Example:
```java
int count = 0;
do {
    System.out.println("Count: " + count);
    count++;
} while (count < 5);
```

### 3. Jump Statements

#### a. break Statement
Terminates the loop or switch statement.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Exit the loop when i equals 5
    }
    System.out.println(i);
}
```

#### b. continue Statement
Skips the current iteration and continues with the next one.

```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    System.out.println(i);  // Prints only odd numbers
}
```

#### c. return Statement
Exits from the current method and returns control to the caller.

```java
public int findValue(int[] array, int target) {
    for (int i = 0; i < array.length; i++) {
        if (array[i] == target) {
            return i;  // Return index when found
        }
    }
    return -1;  // Return -1 if not found
}
```

### 4. Exception Handling

#### a. try-catch Block
Used to handle exceptions (runtime errors).

```java
try {
    // Code that might throw an exception
} catch (ExceptionType e) {
    // Code to handle the exception
}
```

Example:
```java
try {
    int result = 10 / 0;  // This will throw ArithmeticException
    System.out.println("Result: " + result);
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
}
```

#### b. try-catch-finally Block
The finally block always executes, regardless of whether an exception occurs.

```java
try {
    // Code that might throw an exception
} catch (ExceptionType e) {
    // Code to handle the exception
} finally {
    // Code that always executes
}
```

Example:
```java
FileReader reader = null;
try {
    reader = new FileReader("file.txt");
    // Read from file
} catch (IOException e) {
    System.out.println("Error reading file: " + e.getMessage());
} finally {
    try {
        if (reader != null) {
            reader.close();  // Always close the resource
        }
    } catch (IOException e) {
        System.out.println("Error closing file");
    }
}
```

#### c. try-with-resources (Java 7+)
Automatically closes resources that implement AutoCloseable.

```java
try (ResourceType resource = new ResourceType()) {
    // Code using the resource
} catch (ExceptionType e) {
    // Handle exception
}
```

Example:
```java
try (FileReader reader = new FileReader("file.txt");
     BufferedReader buffReader = new BufferedReader(reader)) {
    String line = buffReader.readLine();
    System.out.println(line);
} catch (IOException e) {
    System.out.println("Error reading file: " + e.getMessage());
}
```

### 5. Assertion
Used for testing assumptions during development.

```java
assert condition : "Error message";
```

Example:
```java
int age = -5;
assert age >= 0 : "Age cannot be negative";
```

Note: Assertions are disabled by default. Enable with the `-ea` JVM flag.

