# **Multithreading & Concurrency in Java**  

Multithreading allows multiple tasks to run concurrently within a single program, improving performance and responsiveness. Java provides built-in support for multithreading through the **Thread** class, **Runnable** interface, **Executors**, and **Thread Pools**.

---

## **1. Creating Threads in Java**  
There are **two main ways** to create threads in Java:  
1. **Extending the `Thread` class**  
2. **Implementing the `Runnable` interface**  

### **1.1 Using the `Thread` Class**  
- The `Thread` class provides methods for thread creation and execution.  
- Override the `run()` method to define the thread’s task.  
- Use `.start()` to begin execution (calls `run()` asynchronously).  

```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try { Thread.sleep(1000); } catch (InterruptedException e) { e.printStackTrace(); }
        }
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();  // Starts the new thread
    }
}
```

🔹 **Extending `Thread` is useful when no other class needs to be extended**.  

---

### **1.2 Using the `Runnable` Interface (Preferred Way)**  
- Java does not support multiple inheritance, so it's better to use `Runnable`.  
- Implement `Runnable` and pass it to a `Thread` object.  

```java
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
        }
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start();
    }
}
```

🔹 **Use `Runnable` when your class already extends another class**.  

---

## **2. Thread Synchronization**
Java provides synchronization mechanisms to prevent **race conditions** when multiple threads access shared resources.

### **2.1 The `synchronized` Keyword**
- Ensures that only one thread can execute a block of code at a time.
- Can be used with **methods** or **blocks**.

#### **Synchronized Method**
```java
class SharedResource {
    synchronized void printNumbers() {  // Only one thread can access at a time
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try { Thread.sleep(500); } catch (InterruptedException e) { e.printStackTrace(); }
        }
    }
}

public class SyncExample {
    public static void main(String[] args) {
        SharedResource obj = new SharedResource();

        Thread t1 = new Thread(() -> obj.printNumbers());
        Thread t2 = new Thread(() -> obj.printNumbers());

        t1.start();
        t2.start();
    }
}
```

#### **Synchronized Block**
Instead of synchronizing the entire method, you can **synchronize only a critical section**.

```java
class SharedResource {
    void printNumbers() {
        synchronized (this) {  // Only this block is synchronized
            for (int i = 1; i <= 5; i++) {
                System.out.println(Thread.currentThread().getName() + " - " + i);
            }
        }
    }
}
```

🔹 **Use synchronization to prevent data inconsistency, but be cautious of performance overhead**.  

---

## **3. Executors & Thread Pools**
Creating new threads every time can be **expensive** in terms of CPU and memory. Instead, we use **Thread Pools** to efficiently manage a fixed number of threads.

### **3.1 Using `Executors`**
The `Executors` framework provides a way to manage **thread pools** efficiently.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ExecutorExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);  // Thread pool with 3 threads

        for (int i = 1; i <= 5; i++) {
            executor.execute(() -> System.out.println(Thread.currentThread().getName() + " executing task"));
        }

        executor.shutdown();  // Shutdown the executor after tasks completion
    }
}
```

### **3.2 Types of Thread Pools**
| Executor Type | Description |
|--------------|------------|
| `newFixedThreadPool(n)` | Creates a pool with **n** fixed threads |
| `newCachedThreadPool()` | Creates threads dynamically (auto-scaled) |
| `newSingleThreadExecutor()` | Single-threaded execution |
| `newScheduledThreadPool(n)` | Schedules tasks at fixed rates |

🔹 **Use thread pools for better performance and resource management.**  

---

## **4. Callable & Future (Return Values from Threads)**
- `Runnable` **cannot return a result**, but `Callable<T>` can.  
- `Future<T>` stores the result of `Callable<T>`.  

### **4.1 Using `Callable` and `Future`**
```java
import java.util.concurrent.*;

public class CallableExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Callable<Integer> task = () -> {
            Thread.sleep(1000);
            return 42;  // Returns a value
        };

        Future<Integer> future = executor.submit(task);  // Submit Callable task

        try {
            System.out.println("Result: " + future.get());  // Waits for task completion
        } catch (Exception e) {
            e.printStackTrace();
        }

        executor.shutdown();
    }
}
```

🔹 **Use `Callable` when you need a return value, and `Future` to retrieve the result asynchronously.**  

---

## **Summary Table**
| Concept | Description |
|---------|------------|
| **Thread Class** | Extends `Thread`, overrides `run()` |
| **Runnable Interface** | Implements `Runnable`, passes to `Thread` |
| **Synchronization** | Prevents race conditions using `synchronized` |
| **Executors** | Manages thread pools efficiently |
| **Callable & Future** | Allows returning results from threads |

---

## **Best Practices**
✅ Use **Executors** instead of manually creating threads.  
✅ Use **synchronization sparingly** to avoid performance bottlenecks.  
✅ Use **`Callable` and `Future`** when a thread needs to return a value.  
✅ Avoid **deadlocks** by ensuring proper resource locking.  

🚀 **Need more details? Let me know!**
