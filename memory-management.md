### **Java Memory Management Explained**
Java memory management is **automatic**, meaning the JVM (Java Virtual Machine) manages memory allocation and deallocation. It ensures efficient memory use and prevents memory leaks through **Garbage Collection (GC)**.

---

## **1. Java Memory Areas**
Java divides memory into multiple regions to optimize performance.

### **A. Heap Memory** (Stores Objects and Instance Variables)
- **Used for storing objects** and instance variables.
- Every object created using `new` is stored here.
- **Garbage Collector (GC)** reclaims unused objects.
- Divided into **Young Generation**, **Old Generation**, and **Permanent Generation (Metaspace in Java 8+).**

### **B. Stack Memory** (Stores Local Variables & Method Calls)
- Each thread has its own **stack**.
- Stores **method calls**, **local variables**, and **references to objects in the Heap**.
- **Faster than Heap** because it follows LIFO (Last-In, First-Out).

### **C. Method Area (Class Area)**
- Stores **class metadata**, static variables, and static methods.
- Shared among all threads.
- Exists as long as the JVM is running.

### **D. Program Counter (PC) Register**
- Each thread has its own **PC register**.
- Keeps track of the **currently executing instruction** in a method.

### **E. Native Method Stack**
- Used for **native methods** (written in C/C++).
- Exists only when native code is executed.

---

## **2. Heap Memory Breakdown**
### **Young Generation (New Objects)**
- Stores **new objects**.
- Has three parts:
  1. **Eden Space** → Where new objects are created.
  2. **Survivor Space S0, S1** → Stores surviving objects after GC.
- When an object survives multiple GC cycles, it moves to the **Old Generation**.

### **Old Generation (Long-lived Objects)**
- Stores **long-lived** objects that survive multiple GC cycles.
- When memory is full, **Major GC (Full GC)** runs to clean up memory.

### **Metaspace (Java 8+)**
- Replaced **Permanent Generation** (PermGen).
- Stores **class metadata** (class names, methods, fields, etc.).
- Dynamically grows, unlike PermGen, which had a fixed size.

---

## **3. Memory Allocation in Java**
### **1. Compile-Time Memory Allocation**
- **Method area and Stack memory are allocated at compile-time**.
- Local variables and method calls are stored in the Stack.

### **2. Runtime Memory Allocation**
- **Objects are stored in the Heap at runtime**.
- When a class is loaded, static variables and methods go to the Method Area.

---

## **4. Java Garbage Collection (GC)**
Garbage Collection **automatically removes unused objects** from memory.

### **Types of Garbage Collectors**
1. **Serial GC** (Best for small applications)
   - Uses **single-threaded** garbage collection.
   - `-XX:+UseSerialGC`
   
2. **Parallel GC** (Best for multi-core CPUs)
   - Uses **multiple threads** to speed up GC.
   - `-XX:+UseParallelGC`
   
3. **CMS (Concurrent Mark-Sweep) GC** (Low-latency applications)
   - Runs **concurrently with application threads** to reduce pause time.
   - `-XX:+UseConcMarkSweepGC`
   
4. **G1 (Garbage First) GC** (Default GC in Java 9+)
   - Splits Heap into **regions** and cleans **most garbage first**.
   - `-XX:+UseG1GC`
   
5. **ZGC (Low-latency GC for large heaps)**
   - Handles very **large heap sizes** (up to **16 TB**).
   - `-XX:+UseZGC`

---

## **5. Java Garbage Collection Process**
1. **Mark Phase** → Identifies unused objects.
2. **Sweep Phase** → Removes unused objects from memory.
3. **Compact Phase** → Defragments memory for efficiency.

---

## **6. Example: Java Memory Management in Action**
```java
class Demo {
    static int staticVar = 100;  // Stored in Method Area
    int instanceVar = 200;       // Stored in Heap

    // Instance method (uses Stack & Heap)
    void show() {
        int localVar = 300;  // Stored in Stack
        System.out.println("Local variable: " + localVar);
    }

    // Static method (Stored in Method Area)
    static void display() {
        System.out.println("Inside static method");
    }
}

public class Main {
    public static void main(String[] args) {
        // Accessing static method (Method Area)
        Demo.display();

        // Creating an object (Heap memory)
        Demo obj = new Demo();
        obj.show();

        // Object becomes eligible for garbage collection
        obj = null;

        // Requesting GC manually (Not guaranteed)
        System.gc();
    }

    // Finalize method runs before GC removes an object
    protected void finalize() {
        System.out.println("Garbage Collected!");
    }
}
```
### **Memory Allocation Breakdown**
| Memory Region  | Stores |
|---------------|-------------------------------|
| **Method Area** | `staticVar`, `display()` |
| **Heap** | `obj`, `instanceVar` |
| **Stack** | `localVar`, method calls |

---

## **7. Key Takeaways**
✔ **Heap stores objects**, and **Stack stores method calls & local variables**.  
✔ **Static variables & methods are stored in the Method Area**.  
✔ **Garbage Collector automatically removes unused objects**.  
✔ **Java provides different GC algorithms** for performance tuning.  
✔ **Explicit GC call (`System.gc()`) is not recommended**.  

---


### **Purpose of Creating Static Methods in Java**
Static methods are **class-level** methods that do not depend on instance variables. They are mainly used for:

1. **Utility or Helper Methods**  
   - Example: `Math.pow()`, `Collections.sort()`
   - These methods perform general operations and don’t need object-specific data.

2. **Code Optimization**  
   - No need to create objects just to use a method.
   - Saves memory by avoiding unnecessary object creation.

3. **Global State Access**  
   - Can be used to maintain a shared state across all instances.
   - Example: A counter shared among all objects.

4. **Factory Methods**  
   - Can be used to create and return instances of a class.
   - Example: `Integer.valueOf(100)`

---

## **How Static Methods Are Stored in Memory?**
Java memory is divided into different **regions**, and static methods are stored in the **Method Area** of JVM.

### **Java Memory Layout**
Java manages memory in five main sections:

1. **Method Area (Class Area)**
   - Stores **class-level** data like static methods, static variables, and class metadata.
   - Shared among all instances of a class.
   - Static methods are loaded **once** when the class is loaded.

2. **Heap Area**
   - Stores **instance variables and objects**.
   - Instance methods operate on objects stored in the heap.
   - Garbage Collector manages memory in this area.

3. **Stack Area**
   - Stores **local variables and method calls**.
   - Each thread has its own stack.
   - Both static and instance methods use the stack for execution.

4. **PC Register**
   - Keeps track of the current instruction for each thread.

5. **Native Method Stack**
   - Stores data for native methods (methods written in C/C++).

---

## **Memory Flow of Static vs. Instance Methods**
Let's look at an example and analyze how memory is managed:

```java
class Example {
    static int staticVar = 10;  // Stored in Method Area

    // Static method (stored in Method Area)
    static void staticMethod() {
        System.out.println("Inside static method");
    }

    int instanceVar = 20;  // Stored in Heap

    // Instance method (stored in Method Area, but uses Heap)
    void instanceMethod() {
        System.out.println("Inside instance method");
    }
}

public class Main {
    public static void main(String[] args) {
        // Static members accessed without creating an object
        Example.staticMethod();
        System.out.println(Example.staticVar);

        // Creating an object
        Example obj = new Example();
        obj.instanceMethod();
        System.out.println(obj.instanceVar);
    }
}
```
---
### **How Java Allocates Memory**
1. **Class Loading Stage**
   - `Example.class` is loaded into the **Method Area**.
   - `staticVar` and `staticMethod()` are stored in the **Method Area**.

2. **Main Method Execution**
   - `staticMethod()` is directly accessed from the **Method Area** (no object needed).
   - `staticVar` is accessed from the **Method Area**.

3. **Object Creation (`new Example()`)**
   - `obj` is created in the **Heap**.
   - `instanceVar` is stored in the **Heap**.
   - `instanceMethod()` executes and uses the **Stack** for method calls.

---

### **Static vs. Instance Memory Usage**
| Feature | **Static** | **Instance** |
|---------|-----------|-------------|
| **Storage Location** | Method Area | Heap |
| **Loaded** | Once per class | Every time an object is created |
| **Accessed** | `ClassName.method()` | `objectName.method()` |
| **Lifetime** | Until class is unloaded | Until object is garbage collected |

---

## **Java Memory Management & Garbage Collection**
- **Static members are not garbage collected** because they belong to the class, not objects.
- **Instance members are garbage collected** when no references exist.
- **Garbage Collector (GC)** removes unused objects from the **Heap**.

---

### **Key Takeaways**
✔ **Static methods** are stored in the **Method Area** and loaded **once** per class.  
✔ **Instance methods** operate on object-specific data and are stored in the **Heap**.  
✔ Java **Garbage Collector** automatically cleans up unused objects in the Heap.  
