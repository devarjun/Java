#Exception Handling

## Table of Contents
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
  - [Types of Exceptions](#types-of-exceptions)

## Exception Handling

Exception handling in Java provides a structured way to deal with runtime errors and exceptional conditions.

### Exception Hierarchy

Java's exception classes follow a hierarchy:

```
Throwable
├── Error
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── ...
└── Exception
    ├── IOException
    ├── SQLException
    ├── ClassNotFoundException
    ├── ...
    └── RuntimeException
        ├── NullPointerException
        ├── ArrayIndexOutOfBoundsException
        ├── ArithmeticException
        ├── ...
```

Two main categories:

1. **Checked Exceptions**: Must be either caught or declared (extends Exception)
   - IOException, SQLException, ClassNotFoundException, etc.

2. **Unchecked Exceptions**: Not required to be caught or declared
   - RuntimeException and its subclasses
   - Error and its subclasses

### Try-Catch Blocks

The basic structure for handling exceptions:

```java
try {
    // Code that might throw an exception
    int result = 10 / 0;  // Will throw ArithmeticException
} catch (ArithmeticException e) {
    // Code to handle the exception
    System.out.println("Cannot divide by zero: " + e.getMessage());
}
```

Common exception handling actions:
- Log the exception
- Present a user-friendly message
- Try an alternative approach
- Clean up resources
- Rethrow the exception (possibly wrapped)

### Multiple Catch Blocks

Multiple catch blocks can handle different exception types:

```java
try {
    FileReader file = new FileReader("nonexistent.txt");
    int character = file.read();
    int result = 10 / 0;
} catch (FileNotFoundException e) {
    System.out.println("File not found: " + e.getMessage());
} catch (IOException e) {
    System.out.println("Error reading file: " + e.getMessage());
} catch (ArithmeticException e) {
    System.out.println("Arithmetic error: " + e.getMessage());
}
```

Multi-catch block (Java 7+):
```java
try {
    // Code that might throw exceptions
} catch (FileNotFoundException | NullPointerException e) {
    // Handle both exception types the same way
    System.out.println("Error: " + e.getMessage());
}
```

Catch order matters:
- More specific exceptions should be caught before more general ones
- Subclass exceptions before superclass exceptions

```java
try {
    // Code
} catch (FileNotFoundException e) {  // More specific
    // Handle file not found
} catch (IOException e) {  // More general
    // Handle other I/O exceptions
}
```

### Finally Block

The finally block contains code that always executes, regardless of whether an exception occurs:

```java
FileReader reader = null;
try {
    reader = new FileReader("data.txt");
    // Process file
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    // This will always execute
    try {
        if (reader != null) {
            reader.close();
        }
    } catch (IOException e) {
        System.out.println("Error closing reader");
    }
}
```

The finally block executes even when:
- No exception occurs
- An exception is caught
- An exception is not caught
- A return statement executes in the try or catch block

### Try-With-Resources

Java 7 introduced try-with-resources for automatic resource management:

```java
try (
    FileReader reader = new FileReader("data.txt");
    BufferedReader buffered = new BufferedReader(reader)
) {
    String line = buffered.readLine();
    System.out.println(line);
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
// Resources automatically closed, even if an exception occurs
```

Requirements:
- Resources must implement AutoCloseable interface
- Resources are closed in reverse order of creation
- Implicit finally block runs after resources are closed

### Throwing Exceptions

Methods can throw exceptions using the throw keyword:

```java
public void validateAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
    if (age > 150) {
        throw new IllegalArgumentException("Age is too high");
    }
    // Process valid age
}
```

Method declaration with throws clause:
```java
public void readFile(String filename) throws IOException {
    FileReader reader = new FileReader(filename);  // Might throw FileNotFoundException
    BufferedReader buffered = new BufferedReader(reader);
    
    String line = buffered.readLine();  // Might throw IOException
    System.out.println(line);
    
    buffered.close();
}
```

Rethrowing exceptions:
```java
public void processFile(String filename) throws IOException {
    try {
        readFile(filename);
    } catch (FileNotFoundException e) {
        System.out.println("File not found, using default");
        readFile("default.txt");
    } catch (IOException e) {
        // Log the exception
        System.err.println("IO error: " + e.getMessage());
        // Rethrow it
        throw e;
    }
}
```

### Creating Custom Exceptions

Custom exceptions can be created for application-specific error handling:

```java
// Checked exception
public class InsufficientFundsException extends Exception {
    private final double amount;
    
    public InsufficientFundsException(double amount, String message) {
        super(message);
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}

// Unchecked exception
public class UserNotFoundException extends RuntimeException {
    private final String userId;
    
    public UserNotFoundException(String userId) {
        super("User not found with ID: " + userId);
        this.userId = userId;
    }
    
    public String getUserId() {
        return userId;
    }
}
```

Usage:
```java
public void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) {
        throw new InsufficientFundsException(amount, 
            "Cannot withdraw $" + amount + ", balance is $" + balance);
    }
    balance -= amount;
}

public User findUser(String userId) {
    User user = userRepository.findById(userId);
    if (user == null) {
        throw new UserNotFoundException(userId);
    }
    return user;
}
```

### Exception Propagation

If an exception is not caught, it propagates up the call stack:

```java
public void method3() {
    int result = 10 / 0;  // Throws ArithmeticException
}

public void method2() {
    method3();  // Exception propagates to here
}

public void method1() {
    try {
        method2();  // Exception propagates to here
    } catch (ArithmeticException e) {
        System.out.println("Caught in method1: " + e.getMessage());
    }
}
```

Call sequence: `method1` → `method2` → `method3` → exception → propagated to `method2` → propagated to `method1` → caught

Checked vs. unchecked exception propagation:
- Unchecked exceptions propagate automatically
- Checked exceptions must be caught or declared in the `throws` clause

### Best Practices

1. **Use specific exception types** rather than catching general Exception
2. **Only catch exceptions you can handle** meaningfully
3. **Include informative error messages** in exceptions
4. **Clean up resources** in finally blocks or use try-with-resources
5. **Document exceptions** in Javadoc with @throws
6. **Preserve the exception stack trace** when rethrowing
7. **Don't use exceptions for normal flow control**
8. **Don't swallow exceptions** (catch and do nothing)
9. **Create custom exceptions** for domain-specific errors
10. **Log exceptions** with appropriate context
![image](https://github.com/user-attachments/assets/b384dd90-9a69-44ba-93f4-2e11d1931bcc)

###Types of Exceptions
# Types of Exceptions in Java

In Java, exceptions are categorized into three main types:

## 1. Checked Exceptions
These are exceptions that are checked at compile-time. The compiler requires these exceptions to be either caught using try-catch blocks or declared using the `throws` clause.

Examples:
- `IOException`
- `SQLException`
- `ClassNotFoundException`
- `FileNotFoundException`

```java
try {
    FileInputStream file = new FileInputStream("file.txt");
} catch (FileNotFoundException e) {
    System.out.println("File not found: " + e.getMessage());
}
```

## 2. Unchecked Exceptions (Runtime Exceptions)
These exceptions occur at runtime and are not checked at compile-time. They are subclasses of `RuntimeException` and represent programming errors that could have been avoided.

Examples:
- `NullPointerException`
- `ArrayIndexOutOfBoundsException`
- `ArithmeticException`
- `IllegalArgumentException`
- `NumberFormatException`

```java
// Example of an unchecked exception
int[] arr = new int[5];
// This will throw ArrayIndexOutOfBoundsException at runtime
arr[10] = 50;
```

## 3. Errors
These are serious problems that are not meant to be caught or handled by applications. They usually indicate external resource failures, JVM issues, or other critical conditions.

Examples:
- `OutOfMemoryError`
- `StackOverflowError`
- `VirtualMachineError`
- `AssertionError`

```java
// This will eventually cause a StackOverflowError
public void recursiveMethod() {
    recursiveMethod(); // Infinite recursion
}
```

## Exception Hierarchy
The exception hierarchy in Java:

```
Throwable
├── Error (unchecked)
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── ...
└── Exception
    ├── IOException (checked)
    ├── SQLException (checked)
    ├── ClassNotFoundException (checked)
    └── RuntimeException (unchecked)
        ├── NullPointerException
        ├── ArithmeticException
        ├── IllegalArgumentException
        └── ...
```

## Custom Exceptions
Java allows developers to create their own exception classes by extending either `Exception` (for checked exceptions) or `RuntimeException` (for unchecked exceptions).

```java
// Custom checked exception
public class CustomCheckedException extends Exception {
    public CustomCheckedException(String message) {
        super(message);
    }
}

// Custom unchecked exception
public class CustomRuntimeException extends RuntimeException {
    public CustomRuntimeException(String message) {
        super(message);
    }
}
```
