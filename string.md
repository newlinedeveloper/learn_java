# **String Handling in Java**
In Java, **String handling** is one of the most important features because Strings are widely used in applications. Java provides multiple ways to handle and manipulate Strings efficiently.

---

## **1. What is a String in Java?**
- A **String** in Java is an **immutable** sequence of characters.
- Strings are **objects** in Java, not primitive data types.
- Java provides the `String` class, which is part of `java.lang` package.

```java
String str = "Hello, Java!";  // Creating a String
```

---

## **2. How to Create Strings in Java**
There are two ways to create Strings:

### **A. Using String Literal (Stored in String Pool)**
```java
String s1 = "Hello";   // Stored in the String pool
String s2 = "Hello";   // References the same object in the pool
```
✅ **Efficient** because it reuses existing Strings in the **String Pool**.

---

### **B. Using `new` Keyword (Stored in Heap)**
```java
String s3 = new String("Hello");  // Creates a new object in Heap
```
❌ **Less efficient** because it always creates a **new object**.

---

## **3. String Immutability in Java**
- **Strings in Java are immutable**, meaning their values **cannot be changed** once created.
- If we modify a `String`, Java creates a **new object** instead of modifying the existing one.

### **Example: Immutability**
```java
String s = "Java";
s.concat(" Programming"); // New String is created, but not assigned
System.out.println(s);    // Output: Java (Original remains unchanged)

s = s.concat(" Programming");
System.out.println(s);    // Output: Java Programming (Now assigned)
```

👉 **Why is String Immutable?**
1. **Security** → Used in sensitive areas like passwords, database connections.
2. **Performance Optimization** → Java maintains a **String Pool** to reuse Strings.
3. **Thread Safety** → Multiple threads can use a String without synchronization issues.

---

## **4. String Comparison**
Java provides multiple ways to compare Strings.

### **A. Using `==` (Reference Comparison)**
- Checks **memory address**, not content.

```java
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");

System.out.println(s1 == s2); // true (Same reference in String Pool)
System.out.println(s1 == s3); // false (Different objects in Heap)
```

---

### **B. Using `.equals()` (Content Comparison)**
- Checks **actual content** of Strings.

```java
System.out.println(s1.equals(s3)); // true (Content is the same)
```

---

### **C. Using `compareTo()` (Lexicographical Comparison)**
- Returns:
  - `0` → If both Strings are equal.
  - `>0` → If first String is lexicographically greater.
  - `<0` → If first String is smaller.

```java
String a = "Apple";
String b = "Banana";

System.out.println(a.compareTo(b)); // Negative value (-1)
```

---

## **5. String Methods in Java**
Java provides many built-in methods in the `String` class.

| Method | Description |
|--------|------------|
| `length()` | Returns the length of the String |
| `charAt(index)` | Returns the character at the given index |
| `toUpperCase()` | Converts String to uppercase |
| `toLowerCase()` | Converts String to lowercase |
| `trim()` | Removes leading and trailing spaces |
| `substring(start, end)` | Extracts substring from the String |
| `replace(old, new)` | Replaces a character or substring |
| `split(delimiter)` | Splits a String based on a delimiter |
| `indexOf(char)` | Returns index of first occurrence of character |
| `contains(substring)` | Checks if String contains a substring |

### **Example of String Methods**
```java
public class StringMethodsExample {
    public static void main(String[] args) {
        String str = "  Java Programming  ";

        System.out.println(str.length());              // 19
        System.out.println(str.charAt(5));            // P
        System.out.println(str.toUpperCase());        // JAVA PROGRAMMING
        System.out.println(str.toLowerCase());        // java programming
        System.out.println(str.trim());               // "Java Programming"
        System.out.println(str.substring(2, 6));      // "va P"
        System.out.println(str.replace("Java", "C++"));  // C++ Programming
        System.out.println(str.contains("Java"));     // true

        String[] words = str.split(" "); // Splitting by space
        for (String word : words) {
            System.out.println(word); // Prints each word separately
        }
    }
}
```

---

## **6. StringBuilder and StringBuffer (Mutable Strings)**
Since **Strings are immutable**, modifying them frequently (e.g., loops) creates **new objects**, impacting performance.

To solve this, Java provides:
1. **`StringBuffer`** → **Thread-safe, synchronized**
2. **`StringBuilder`** → **Faster, not synchronized (Preferred in single-threaded apps)**

---

### **A. Using `StringBuilder` (Faster, Non-Synchronized)**
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Java");
        sb.append(" Programming");
        System.out.println(sb); // Java Programming
    }
}
```

---

### **B. Using `StringBuffer` (Thread-Safe, Synchronized)**
```java
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Java");
        sb.append(" Programming");
        System.out.println(sb); // Java Programming
    }
}
```

### **Performance Comparison**
| Feature | `String` | `StringBuffer` | `StringBuilder` |
|---------|---------|---------------|---------------|
| **Mutable** | ❌ No | ✅ Yes | ✅ Yes |
| **Thread-Safe** | ✅ Yes | ✅ Yes | ❌ No |
| **Performance** | **Slow** | **Medium** | **Fast** |

✅ **Use `String` for small modifications.**  
✅ **Use `StringBuilder` when performance matters.**  
✅ **Use `StringBuffer` in multi-threaded applications.**

---

## **7. String Formatting**
Java provides `String.format()` to format Strings.

```java
int age = 25;
String name = "Alice";
String formatted = String.format("Name: %s, Age: %d", name, age);
System.out.println(formatted); // Name: Alice, Age: 25
```

---

## **8. String Pool Optimization**
Java optimizes memory using the **String Pool**, which is part of the **Method Area**.

### **Example**
```java
String s1 = "Java"; 
String s2 = "Java"; // Reuses s1
String s3 = new String("Java"); // New object in Heap
```
- `s1` and `s2` refer to the **same object** in the String Pool.
- `s3` creates a **new object** in Heap.

To force String Pool usage:
```java
String s4 = new String("Java").intern();
```
Now `s4` refers to the **String Pool object**.

---

## **9. Convert Other Types to String**
- **Using `String.valueOf()`**
```java
int num = 100;
String str = String.valueOf(num);  // "100"
```
- **Using `toString()`**
```java
Integer num = 100;
String str = num.toString();  // "100"
```

---

## **10. Conclusion**
- **Strings are immutable** (modifications create new objects).
- **Use `StringBuilder` for performance-critical operations**.
- **Use `StringBuffer` in multi-threaded environments**.
- **String Pool optimizes memory usage**.

---
