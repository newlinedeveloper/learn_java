# **Java I/O and File Handling**  

Java provides a powerful **I/O (Input/Output) API** for reading and writing data from files, network streams, and memory buffers. Java I/O can be categorized into **Character Streams** (for text data) and **Byte Streams** (for binary data).  

---

# **1. Reading and Writing Files in Java**
Java provides multiple classes for reading and writing files, including:

✅ **Character Streams** (for text-based data)
- `FileReader` & `FileWriter`
- `BufferedReader` & `BufferedWriter`

✅ **Byte Streams** (for binary data like images, videos, etc.)
- `FileInputStream` & `FileOutputStream`
- `BufferedInputStream` & `BufferedOutputStream`

✅ **NIO Package** (More efficient, uses channels)
- `Files` class (`java.nio.file.Files`)
- `Path` class (`java.nio.file.Path`)

---

## **1.1 Reading a File Using `FileReader` and `BufferedReader`**
`FileReader` reads **characters**, while `BufferedReader` improves efficiency by reading larger chunks.

### **Example: Reading a File Using `FileReader`**
```java
import java.io.FileReader;
import java.io.IOException;

public class FileReaderExample {
    public static void main(String[] args) {
        try (FileReader reader = new FileReader("example.txt")) {
            int character;
            while ((character = reader.read()) != -1) {
                System.out.print((char) character);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **`FileReader` reads the file character by character.**  
❌ **Not efficient for large files** → Use `BufferedReader` instead.

---

### **Example: Reading a File Using `BufferedReader`**
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedReaderExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Reads the file line by line, making it efficient for large files.**

---

## **1.2 Writing a File Using `FileWriter` and `BufferedWriter`**
### **Example: Writing to a File Using `FileWriter`**
```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        try (FileWriter writer = new FileWriter("output.txt")) {
            writer.write("Hello, this is a test file!");
            writer.write("\nWriting to a file using Java.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **`FileWriter` writes character data to a file.**  
❌ **Does not handle large data efficiently** → Use `BufferedWriter`.

---

### **Example: Writing to a File Using `BufferedWriter`**
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedWriterExample {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
            writer.write("BufferedWriter is efficient!");
            writer.newLine();
            writer.write("It writes data in chunks.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **More efficient because it writes data in chunks.**  
✅ **Uses `newLine()` for platform-independent line breaks.**

---

## **1.3 Reading and Writing Files Using `java.nio.file.Files`**
`java.nio.file.Files` is part of **Java NIO (New I/O)** and provides a simpler way to read and write files.

### **Example: Reading a File Using `Files.readAllLines()`**
```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;
import java.util.List;

public class NIOReadExample {
    public static void main(String[] args) {
        Path path = Paths.get("example.txt");
        try {
            List<String> lines = Files.readAllLines(path);
            lines.forEach(System.out::println);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Reads an entire file into a `List<String>`.**  
✅ **More convenient than `BufferedReader`.**

---

### **Example: Writing to a File Using `Files.write()`**
```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;
import java.util.Arrays;

public class NIOWriteExample {
    public static void main(String[] args) {
        Path path = Paths.get("output.txt");
        try {
            Files.write(path, Arrays.asList("Line 1", "Line 2", "Line 3"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Writes multiple lines efficiently using `Files.write()`.**  

---

# **2. Serialization & Deserialization**
Serialization allows converting an object into a byte stream so it can be saved to a file or transferred over a network. Deserialization is the reverse process.

### **2.1 How Serialization Works**
1. The class must **implement `Serializable`**.
2. Use `ObjectOutputStream` to serialize the object.
3. Use `ObjectInputStream` to deserialize the object.

### **2.2 Example: Serializing an Object**
```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.io.Serializable;

class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        Person person = new Person("John Doe", 30);
        try (FileOutputStream fileOut = new FileOutputStream("person.ser");
             ObjectOutputStream out = new ObjectOutputStream(fileOut)) {
            out.writeObject(person);
            System.out.println("Object serialized successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Converts the `Person` object into a byte stream and saves it to `person.ser`.**

---

### **2.3 Example: Deserializing an Object**
```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;

public class DeserializationExample {
    public static void main(String[] args) {
        try (FileInputStream fileIn = new FileInputStream("person.ser");
             ObjectInputStream in = new ObjectInputStream(fileIn)) {
            Person person = (Person) in.readObject();
            System.out.println("Deserialized Person: " + person.name + ", " + person.age);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Reads the serialized object from `person.ser` and restores it.**

---

# **3. Summary Table**
| **Feature**       | **Class Used**        | **Purpose** |
|-------------------|----------------------|-------------|
| File Reading     | `FileReader`, `BufferedReader`, `Files.readAllLines()` | Read text files |
| File Writing     | `FileWriter`, `BufferedWriter`, `Files.write()` | Write text files |
| Binary File I/O  | `FileInputStream`, `FileOutputStream` | Read/write binary files |
| Serialization    | `ObjectOutputStream` | Convert object to byte stream |
| Deserialization  | `ObjectInputStream` | Convert byte stream to object |

---

# **Best Practices**
✅ Always **close file resources** or use **try-with-resources** (`try (BufferedReader br = new BufferedReader(new FileReader("file.txt")))`).  
✅ Use **BufferedReader/BufferedWriter** for efficiency.  
✅ Use **`Files.readAllLines()`** and **`Files.write()`** for modern Java applications.  
✅ Use **serialization** only when necessary (avoid storing sensitive data).  
