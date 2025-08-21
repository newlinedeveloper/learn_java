# 🚀 Java 8 Key Features (with Examples)

---

### 1. **Lambda Expressions**

* Anonymous functions → reduce boilerplate in functional programming.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// Traditional
Collections.sort(names, new Comparator<String>() {
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});

// Lambda
names.sort((a, b) -> a.compareTo(b));
```

👉 Interview Q: *Why lambdas?*
✅ More concise, enable functional programming (streams, parallel processing).

---

### 2. **Functional Interfaces (`@FunctionalInterface`)**

* Interface with exactly **one abstract method**.
* Example: `Runnable`, `Callable`, `Comparator`, `Predicate`.

```java
@FunctionalInterface
interface MyFunc {
    int add(int a, int b);
}

public class Demo {
    public static void main(String[] args) {
        MyFunc f = (x, y) -> x + y;
        System.out.println(f.add(5, 3)); // 8
    }
}
```

👉 Interview Q: *What’s special about functional interfaces?*
✅ They work with lambdas & method references.

---

### 3. **Default and Static Methods in Interfaces**

* Interfaces can have implementations (without breaking old code).

```java
interface Vehicle {
    void start();
    default void stop() { System.out.println("Stopping..."); }
    static void clean() { System.out.println("Cleaning vehicle..."); }
}

class Car implements Vehicle {
    public void start() { System.out.println("Starting car..."); }
}

public class Main {
    public static void main(String[] args) {
        Car c = new Car();
        c.start();
        c.stop();       // default method
        Vehicle.clean(); // static method
    }
}
```

---

### 4. **Streams API**

* Process collections in a **declarative** (functional) style.

```java
List<String> names = Arrays.asList("John", "Alice", "Bob", "Charlie");

// Filter + Map + Collect
List<String> result = names.stream()
        .filter(s -> s.startsWith("A"))
        .map(String::toUpperCase)
        .toList();

System.out.println(result); // [ALICE]
```

👉 Interview Q: *Difference between Streams and Collections?*
✅ Collections = data storage, Streams = data processing.

---

### 5. **Method References (`::`)**

* Shorter form of lambdas.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// Lambda
names.forEach(n -> System.out.println(n));

// Method reference
names.forEach(System.out::println);
```

---

### 6. **Optional Class**

* Avoids `NullPointerException` using safe wrappers.

```java
Optional<String> name = Optional.ofNullable("Alice");

// If present
name.ifPresent(n -> System.out.println(n.toUpperCase())); // ALICE

// Default value
System.out.println(name.orElse("Default"));
```

👉 Interview Q: *Why Optional?*
✅ Explicitly models “value may be absent” → safer null handling.

---

### 7. **New Date and Time API (`java.time`)**

* Replaces old `Date` and `Calendar`. Immutable, thread-safe.

```java
import java.time.*;

public class Main {
    public static void main(String[] args) {
        LocalDate today = LocalDate.now();
        LocalDate birthday = LocalDate.of(1990, 5, 20);

        Period p = Period.between(birthday, today);
        System.out.println("Age: " + p.getYears());
    }
}
```

👉 Interview Q: *Why new Date/Time API?*
✅ Old API (`Date`, `Calendar`) was mutable, error-prone, not thread-safe.

---

### 8. **Nashorn JavaScript Engine** (Deprecated in Java 15)

* Run JavaScript inside Java.

```java
import javax.script.*;

public class Main {
    public static void main(String[] args) throws Exception {
        ScriptEngine engine = new ScriptEngineManager().getEngineByName("nashorn");
        engine.eval("print('Hello from JS')");
    }
}
```

---

### 9. **CompletableFuture (Concurrency Enhancements)**

* Async programming made simpler.

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) throws Exception {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            return "Hello " + Thread.currentThread().getName();
        });

        System.out.println(future.get());
    }
}
```

---

### 10. **Other Enhancements**

* **Collectors API** (`Collectors.groupingBy`, `joining`).
* **Base64 encoding/decoding** (`java.util.Base64`).
* **Parallel Streams** (for multicore processing).

---

# 🎯 Likely Java 8 Interview Questions

1. What are **functional interfaces**? Give examples.
2. Difference between **map()** and **flatMap()** in Streams.
3. How does **Optional** help prevent `NullPointerException`?
4. Explain **default vs static methods** in interfaces.
5. What is the difference between **sequential and parallel streams**?
6. What are problems with old `Date` and `Calendar`, and how does **java.time** fix them?
7. Explain **CompletableFuture** with an example.
8. What’s the difference between `findFirst()` and `findAny()` in Streams?

---

⚡ Quick Recap (Java 8 brought):
👉 *Lambdas, Streams, Optional, Default methods, Method References, Date/Time API, CompletableFuture, Nashorn engine.*

---
