### ✪ Core Java Questions

#### ▶ OOP Concepts

**1. What are the four pillars of Object-Oriented Programming?**

* **Encapsulation:** Wrapping data and methods together (e.g., using private variables and public getters/setters).
* **Abstraction:** Hiding implementation details using interfaces or abstract classes.
* **Inheritance:** Acquiring properties from a parent class.
* **Polymorphism:** One interface, many implementations.

**2. Explain inheritance vs composition with examples.**

* **Inheritance:** Code reuse through parent-child relationship.

```java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}
class Dog extends Animal {
    void sound() { System.out.println("Bark"); }
}
```

* **Composition:** Using objects within another object.

```java
class Engine {
    void start() { System.out.println("Engine started"); }
}
class Car {
    Engine engine = new Engine();
    void startCar() { engine.start(); }
}
```

**3. What is polymorphism and how is it implemented in Java?**

* Polymorphism allows methods to behave differently based on object type.

```java
class Shape {
    void draw() { System.out.println("Drawing Shape"); }
}
class Circle extends Shape {
    void draw() { System.out.println("Drawing Circle"); }
}
Shape shape = new Circle();
shape.draw(); // Output: Drawing Circle
```

---

#### ▶ Exception Handling

**4. What is the difference between checked and unchecked exceptions?**

* **Checked:** Must be declared or handled (`IOException`, `SQLException`).
* **Unchecked:** Runtime errors (`NullPointerException`, `ArithmeticException`).

**5. When would you create a custom exception?**

* When domain-specific errors need to be described.

```java
class InvalidUserException extends Exception {
    public InvalidUserException(String msg) { super(msg); }
}
```

---

#### ▶ Collections Framework

**6. Difference between ArrayList, LinkedList, HashMap, and TreeMap.**

* `ArrayList`: Fast random access, slow insert/delete.
* `LinkedList`: Fast insert/delete, slow access.
* `HashMap`: Key-value store, unordered.
* `TreeMap`: Sorted key-value store (uses Red-Black Tree).

**7. How does HashMap work internally?**

* Uses an array of buckets.
* Each bucket is a linked list or tree (Java 8+).
* Key's `hashCode()` and `equals()` are used for placement and lookup.

**8. What is the difference between Set, List, and Map?**

* `Set`: No duplicates.
* `List`: Ordered, allows duplicates.
* `Map`: Key-value pairs.

---

#### ▶ Multithreading & Concurrency

**9. How do you create threads in Java?**

```java
class MyThread extends Thread {
    public void run() { System.out.println("Thread running"); }
}
new MyThread().start();
```

OR

```java
Runnable r = () -> System.out.println("Runnable thread");
new Thread(r).start();
```

**10. What is the difference between synchronized block and synchronized method?**

* **Synchronized method:** Locks the whole method on the object.
* **Synchronized block:** Locks only the specific code block.

```java
synchronized (this) {
    // critical section
}
```

**11. What are volatile, ThreadLocal, and ExecutorService?**

* `volatile`: Ensures visibility of changes to variables across threads.
* `ThreadLocal`: Maintains variable per thread.
* `ExecutorService`: Manages thread pools and task execution.

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
executor.submit(() -> System.out.println("Task executed"));
```

---

#### ▶ Memory Management

**12. How does garbage collection work in Java?**

* GC automatically removes unreferenced objects from heap.
* Uses algorithms like Mark & Sweep, Generational GC.

**13. What are memory leaks and how can they be prevented?**

* Memory leaks occur when unused objects are still referenced.
* Prevention:

  * Avoid static references.
  * Use weak references when necessary.
  * Close streams/resources (`try-with-resources`).

---

