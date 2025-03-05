# **Java Collections Framework (JCF)**
The **Java Collections Framework (JCF)** provides a set of interfaces and classes for handling groups of objects efficiently.  

### **Key Interfaces in JCF**  
1. **List** → Ordered collection, allows duplicates.  
2. **Set** → Unique elements, unordered (except TreeSet).  
3. **Map** → Key-value pairs, keys are unique.  
4. **Queue** → FIFO (First-In-First-Out) order.  

---

## **1. List (ArrayList, LinkedList)**
A `List` in Java **preserves insertion order** and allows **duplicate elements**.  

### **1.1 ArrayList (Dynamic Array)**
- **Uses a resizable array** to store elements.  
- **Fast random access (O(1))** but **slow insertion/deletion (O(n))**.  
- **Not synchronized** (not thread-safe).  

```java
import java.util.*;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Apple");  // Duplicates allowed
        
        System.out.println(list);  // Output: [Apple, Banana, Apple]
        
        list.remove("Banana");  // Remove element
        System.out.println(list.contains("Apple")); // true
    }
}
```

### **1.2 LinkedList (Doubly Linked List)**
- Elements are **linked via nodes**.  
- **Fast insertion/deletion (O(1))** at the beginning/middle.  
- **Slower access (O(n))** compared to `ArrayList`.  

```java
import java.util.*;

public class LinkedListExample {
    public static void main(String[] args) {
        List<Integer> list = new LinkedList<>();
        list.add(10);
        list.add(20);
        list.add(30);

        System.out.println(list.get(1)); // Output: 20
    }
}
```
🔹 **Use `ArrayList` for fast read access, and `LinkedList` for fast insert/delete operations.**  

---

## **2. Set (HashSet, TreeSet)**
A `Set` stores **unique elements only** (no duplicates).

### **2.1 HashSet (Unordered, No Duplicates)**
- **Uses a Hash Table** for storage.  
- **Fast operations (O(1))**, but **unordered elements**.  
- Allows **one null value**.  

```java
import java.util.*;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Java");
        set.add("Python");
        set.add("Java");  // Duplicate, ignored

        System.out.println(set);  // Output: [Java, Python] (order may vary)
    }
}
```

### **2.2 TreeSet (Sorted, No Duplicates)**
- **Uses a Red-Black Tree** (self-balancing BST).  
- Elements are **sorted in natural order**.  
- **Slower than HashSet (O(log n))**.  

```java
import java.util.*;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<Integer> set = new TreeSet<>();
        set.add(20);
        set.add(10);
        set.add(30);

        System.out.println(set);  // Output: [10, 20, 30] (sorted)
    }
}
```
🔹 **Use `HashSet` for fast lookups, and `TreeSet` for sorted elements.**  

---

## **3. Map (HashMap, TreeMap)**
A `Map` stores **key-value pairs**.  
- **Keys are unique**, but values can be duplicated.  

### **3.1 HashMap (Unordered, Fast Access)**
- **Uses a Hash Table**, stores entries in **random order**.  
- **Fast operations (O(1))**.  
- Allows **one null key, multiple null values**.  

```java
import java.util.*;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("Alice", 30);
        map.put("Bob", 25);
        map.put("Alice", 35);  // Overwrites previous value

        System.out.println(map.get("Alice"));  // Output: 35
    }
}
```

### **3.2 TreeMap (Sorted by Key)**
- **Uses a Red-Black Tree**, maintains keys in **sorted order**.  
- **Slower than HashMap (O(log n))**.  

```java
import java.util.*;

public class TreeMapExample {
    public static void main(String[] args) {
        Map<Integer, String> map = new TreeMap<>();
        map.put(2, "Banana");
        map.put(1, "Apple");
        map.put(3, "Cherry");

        System.out.println(map);  // Output: {1=Apple, 2=Banana, 3=Cherry}
    }
}
```
🔹 **Use `HashMap` for fast lookups, and `TreeMap` for sorted key-value pairs.**  

---

## **4. Queue (PriorityQueue, Deque)**
A `Queue` follows **FIFO (First In, First Out)**.

### **4.1 PriorityQueue (Min-Heap)**
- **Elements are stored in sorted order** based on priority.  
- **Default: Min-Heap (smallest element first)**.  

```java
import java.util.*;

public class PriorityQueueExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.add(30);
        pq.add(10);
        pq.add(20);

        System.out.println(pq.poll());  // Output: 10 (smallest element)
    }
}
```
For **Max-Heap**, use a custom comparator:
```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
```

---

### **4.2 Deque (Double-Ended Queue)**
- Allows **insertion/removal from both ends**.  
- Implemented by **ArrayDeque** (faster than LinkedList).  

```java
import java.util.*;

public class DequeExample {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<>();
        deque.addFirst("Front");
        deque.addLast("Back");

        System.out.println(deque.pollFirst()); // Output: Front
        System.out.println(deque.pollLast());  // Output: Back
    }
}
```
🔹 **Use `PriorityQueue` for priority-based tasks and `Deque` for efficient double-ended operations.**  

---

## **Summary Table**
| Collection | Ordered? | Duplicates? | Performance |
|------------|---------|------------|-------------|
| **ArrayList** | ✅ Yes | ✅ Yes | Fast read (O(1)), Slow insert/delete (O(n)) |
| **LinkedList** | ✅ Yes | ✅ Yes | Fast insert/delete (O(1)), Slow read (O(n)) |
| **HashSet** | ❌ No | ❌ No | Fast operations (O(1)) |
| **TreeSet** | ✅ Yes (Sorted) | ❌ No | O(log n) operations |
| **HashMap** | ❌ No | ✅ Yes (values) | O(1) operations |
| **TreeMap** | ✅ Yes (Sorted by Key) | ✅ Yes (values) | O(log n) operations |
| **PriorityQueue** | ✅ Yes (Heap order) | ✅ Yes | O(log n) insert/delete |
| **Deque** | ✅ Yes | ✅ Yes | O(1) for both ends |

---

## **Final Thoughts**
- **Use `ArrayList` for fast random access.**
- **Use `LinkedList` when frequent insertions/deletions are required.**
- **Use `HashSet` for uniqueness without sorting.**
- **Use `TreeSet` if sorted unique elements are needed.**
- **Use `HashMap` for quick lookups, `TreeMap` for sorted key-value pairs.**
- **Use `PriorityQueue` for handling priority-based tasks.**
- **Use `Deque` for efficient double-ended operations.**
