# Java File I/O (Input/Output)

File Input/Output operations are essential for most Java applications that need to interact with external files for reading, writing, or modifying data. Java provides a rich set of classes and interfaces in the `java.io` and `java.nio` packages to handle file operations efficiently and securely.

## Understanding File I/O in Java

At its core, Java File I/O revolves around streams—sequences of data flowing between your program and external sources. The Java I/O system is built upon a foundation of abstract classes that define common behaviors, with concrete subclasses implementing specific functionalities.

### Key Concepts

1. **Streams**: Ordered sequences of data with a source and destination.
2. **Bytes vs. Characters**: Java distinguishes between binary data (bytes) and text data (characters).
3. **Buffering**: A technique to improve performance by reading/writing data in chunks rather than one byte/character at a time.
4. **File Navigation**: Methods to browse directories and access file metadata.

## Types of File I/O in Java

Java provides two major approaches to file operations:

### 1. Traditional I/O (`java.io` package)

This is the original file handling mechanism available since early Java versions. It includes:

#### Byte Streams
For handling binary data, operating directly with bytes:

- `FileInputStream`: Reads raw bytes from a file
- `FileOutputStream`: Writes raw bytes to a file
- `BufferedInputStream`: Adds buffering to improve performance
- `BufferedOutputStream`: Adds buffering for output operations
- `DataInputStream`: Reads primitive Java data types
- `DataOutputStream`: Writes primitive Java data types

#### Character Streams
For handling text data, automatically handling character encoding:

- `FileReader`: Reads characters from a file
- `FileWriter`: Writes characters to a file
- `BufferedReader`: Adds buffering and convenient methods like `readLine()`
- `BufferedWriter`: Adds buffering for character output
- `PrintWriter`: Adds formatting capabilities

### 2. New I/O (`java.nio` package)

Introduced in Java 1.4 and enhanced in Java 7, this approach provides:

- More efficient operations through channels and buffers
- Memory-mapped file operations
- File locking capabilities
- Non-blocking I/O operations
- Better exception handling through the `try-with-resources` structure

Key classes include:
- `Path`: Represents a file location
- `Files`: Contains static methods for file operations
- `Channels`: Represent connections to files, sockets, etc.
- `Buffers`: Memory blocks that data is read from or written to

## Common File Operations in Java

### 1. Reading from a File

#### Using FileInputStream (Byte Stream)

```java
try (FileInputStream fis = new FileInputStream("input.dat")) {
    int byteData;
    while ((byteData = fis.read()) != -1) {
        // Process each byte of data
        System.out.print((byte) byteData);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

#### Using BufferedReader (Character Stream)

```java
try (BufferedReader reader = new BufferedReader(new FileReader("input.txt"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        // Process each line
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

#### Using Files class (NIO)

```java
try {
    List<String> allLines = Files.readAllLines(Paths.get("input.txt"));
    for (String line : allLines) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### 2. Writing to a File

#### Using FileOutputStream (Byte Stream)

```java
try (FileOutputStream fos = new FileOutputStream("output.dat")) {
    String data = "Hello, Java I/O!";
    fos.write(data.getBytes());
} catch (IOException e) {
    e.printStackTrace();
}
```

#### Using BufferedWriter (Character Stream)

```java
try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
    writer.write("Hello, Java I/O!");
    writer.newLine(); // Add a line separator
    writer.write("This is a new line.");
} catch (IOException e) {
    e.printStackTrace();
}
```

#### Using Files class (NIO)

```java
try {
    List<String> lines = Arrays.asList("Hello, Java NIO!", "This is another line.");
    Files.write(Paths.get("output.txt"), lines);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 3. File and Directory Operations

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.*;

public class FileOperationsExample {
    public static void main(String[] args) {
        // Creating a new file
        try {
            File newFile = new File("newfile.txt");
            if (newFile.createNewFile()) {
                System.out.println("File created: " + newFile.getName());
            } else {
                System.out.println("File already exists.");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Creating a directory
        File directory = new File("newDirectory");
        if (directory.mkdir()) {
            System.out.println("Directory created: " + directory.getName());
        } else {
            System.out.println("Failed to create directory or it already exists.");
        }
        
        // Listing files in a directory
        File folder = new File(".");
        File[] listOfFiles = folder.listFiles();
        if (listOfFiles != null) {
            for (File file : listOfFiles) {
                if (file.isFile()) {
                    System.out.println("File: " + file.getName());
                } else if (file.isDirectory()) {
                    System.out.println("Directory: " + file.getName());
                }
            }
        }
        
        // Using NIO for similar operations
        try {
            // Create file if it doesn't exist
            Path path = Paths.get("nio_example.txt");
            if (!Files.exists(path)) {
                Files.createFile(path);
                System.out.println("NIO file created");
            }
            
            // Create directory
            Path dirPath = Paths.get("nio_directory");
            if (!Files.exists(dirPath)) {
                Files.createDirectory(dirPath);
                System.out.println("NIO directory created");
            }
            
            // List directory contents
            try (DirectoryStream<Path> stream = Files.newDirectoryStream(Paths.get("."))) {
                for (Path entry : stream) {
                    System.out.println(entry.getFileName());
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Advanced File Operations

### Working with Random Access Files

```java
try (RandomAccessFile file = new RandomAccessFile("random.dat", "rw")) {
    // Write to file
    file.writeInt(365);
    file.writeDouble(3.14159);
    file.writeUTF("Random Access File Example");
    
    // Move file pointer to beginning
    file.seek(0);
    
    // Read from file
    System.out.println("Integer: " + file.readInt());
    System.out.println("Double: " + file.readDouble());
    System.out.println("String: " + file.readUTF());
} catch (IOException e) {
    e.printStackTrace();
}
```

### Memory-Mapped Files

```java
try {
    Path path = Paths.get("mapped.dat");
    
    // Create a file and write some data to it
    Files.write(path, new byte[10 * 1024 * 1024]); // 10 MB file
    
    // Memory-map the file
    try (FileChannel channel = FileChannel.open(path, StandardOpenOption.READ, StandardOpenOption.WRITE)) {
        MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_WRITE, 0, channel.size());
        
        // Write to the memory-mapped file
        buffer.putInt(0, 100);
        buffer.putInt(4, 200);
        
        // Force changes to be written to disk
        buffer.force();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

## Best Practices for File I/O in Java

1. **Always close resources**: Use try-with-resources to ensure streams are properly closed.
2. **Use buffered streams**: They significantly improve performance by reducing the number of physical I/O operations.
3. **Handle exceptions properly**: File operations can fail for many reasons (permissions, disk full, etc.).
4. **Choose the right stream type**: Use byte streams for binary files and character streams for text files.
5. **Consider character encodings**: Specify the encoding when dealing with text files to avoid platform-dependent issues.
6. **Use NIO for advanced operations**: NIO provides better performance for large files and more control over I/O operations.

## Java NIO vs Traditional I/O

| Feature | Traditional I/O | NIO |
|---------|----------------|-----|
| Stream orientation | Stream oriented | Buffer oriented |
| Blocking | Blocking operations | Support for non-blocking operations |
| Selectors | Not available | Available for multiplexed I/O |
| Channels | Not available | Available for direct transfers |
| Efficiency | Lower for large files | Higher with memory-mapped files |
| API complexity | Simpler | More complex |
| File locking | Limited | Advanced capabilities |

## Common File I/O Exceptions

- `FileNotFoundException`: The specified file does not exist or cannot be opened.
- `IOException`: General I/O error occurred.
- `SecurityException`: Security manager denies access to the file.
- `UnsupportedEncodingException`: The specified character encoding is not supported.
- `EOFException`: End of file reached unexpectedly.

## Conclusion

Java's File I/O capabilities offer a comprehensive toolkit for developers to work with files efficiently. From simple text file reading to advanced memory-mapped operations, the framework provides flexibility to handle various scenarios. Understanding the appropriate classes and methods for specific tasks can significantly improve application performance and reliability.

Remember that proper resource management and exception handling are crucial aspects of file operations to prevent resource leaks and ensure data integrity.
