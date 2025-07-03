## 🔹 Java 8+ Features

### ▶ Functional Programming

#### 1. **What are lambdas and where have you used them?**

**Answer:**
Lambdas are anonymous functions introduced in Java 8 that enable functional programming. They make it easier to pass behavior as arguments to methods (especially for use with streams, sorting, threading, etc.).

**Example:**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));
```

Used in:

* `forEach` to iterate.
* Thread execution (`Runnable`).
* Stream operations like `map`, `filter`.

---

#### 2. **What is the difference between map, filter, and reduce in streams?**

**Answer:**

* `map`: Transforms each element.
* `filter`: Filters elements by a condition.
* `reduce`: Aggregates the stream into a single value.

**Example:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<Integer> squares = numbers.stream()
    .map(n -> n * n)
    .collect(Collectors.toList());

List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

int sum = numbers.stream()
    .reduce(0, Integer::sum);
```

---

### ▶ Optional and Streams

#### 3. **How does `Optional` help avoid `NullPointerException`?**

**Answer:**
`Optional` is a container object which may or may not contain a non-null value. It avoids explicit null checks and encourages functional-style operations.

**Example:**

```java
Optional<String> name = Optional.ofNullable(getName());
name.ifPresent(System.out::println);
```

Instead of:

```java
if (name != null) {
    System.out.println(name);
}
```

---

#### 4. **Examples of using Stream API for collection operations**

**Example:**

```java
List<String> names = Arrays.asList("Anna", "Bob", "Charlie");

// Count names starting with 'A'
long count = names.stream()
    .filter(n -> n.startsWith("A"))
    .count();

// Sort names alphabetically
List<String> sorted = names.stream()
    .sorted()
    .collect(Collectors.toList());
```

---

### ▶ Date & Time API

#### 5. **Difference between `java.util.Date` and `java.time.LocalDateTime`**

| Feature                | `java.util.Date`    | `java.time.LocalDateTime` |
| ---------------------- | ------------------- | ------------------------- |
| Mutability             | Mutable             | Immutable                 |
| Thread safety          | Not thread-safe     | Thread-safe               |
| Time zone support      | No built-in support | Can use `ZonedDateTime`   |
| Readability/API design | Poor                | Clear and fluent API      |

**Example:**

```java
LocalDateTime now = LocalDateTime.now();
System.out.println("Current Time: " + now);
```

---

