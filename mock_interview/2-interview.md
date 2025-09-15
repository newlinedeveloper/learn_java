# Java Mock Interview – Q\&A Notes

### 1. REST & Spring Boot Basics

**Q:** Best practices for writing REST APIs?
**A:** Use `@RestController`, follow MVC, use `@PostMapping` with `@RequestBody` for creates, `@GetMapping` for reads, and keep controllers thin.

**Q:** Difference between `@RequestMapping` vs `@GetMapping`/`@PostMapping`?
**A:** `@RequestMapping` can be applied at class or method level and supports all HTTP methods. `@GetMapping`, `@PostMapping` are specialized shortcuts.

**Q:** Can two `@RequestMapping` methods share the same URL?
**A:** Yes, if the HTTP methods differ.

**Q:** Using `@RequestParam` and `@PathVariable` together?
**A:** Possible, but they serve different purposes (`key=value` in query string vs part of the path).

**Q:** Difference between returning a `ResponseEntity` vs a plain object?
**A:** `ResponseEntity` lets you set HTTP status codes and headers; plain objects do not.

**Q:** Internal working of `@Autowired`?
**A:** Spring’s IoC container performs dependency injection, creating a single bean instance and wiring it by type (field or constructor injection).

**Q:** `@Repository` vs `@Service`?
**A:** `@Repository` marks DAO classes and enables exception translation.
`@Service` marks service-layer classes containing business logic.

**Q:** Spring Boot Actuator purpose?
**A:** Provides production-ready endpoints (health, metrics, heap/thread dumps). Secure or restrict sensitive endpoints.

**Q:** Common Spring annotations?
**A:** `@RestController`, `@Entity`, `@Id`, `@GeneratedValue`, `@RequestMapping`.
Uncommon but important: `@Qualifier`, `@Bean`, `@Primary`, `@Async`, `@Cacheable`, `@PreAuthorize`, `@PostAuthorize`.

---

### 2. Java 8 & Functional Programming

**Q:** What is a Lambda expression?
**A:** Anonymous function with no method name/signature. Reduces boilerplate compared to anonymous classes.

**Q:** `this` in Lambda vs Anonymous class?
**A:** In a lambda, `this` refers to the enclosing class; in an anonymous inner class, it refers to the inner class itself.

**Q:** Functional interfaces & examples?
**A:** Interfaces with exactly one abstract method.

* `Predicate<T>` – returns boolean.
* `Consumer<T>` – accepts input, no output.
* `Supplier<T>` – produces output, no input.
* `Function<T,R>` – transforms input to output.

**Q:** What if a functional interface has 2 abstract methods?
**A:** Compilation error; lambda expressions require exactly one.

**Q:** Difference between `map()` and `flatMap()`?
**A:** `map` transforms each element 1-to-1, returning a `Stream<T>`.
`flatMap` flattens nested streams (e.g., `Stream<Stream<T>>` to `Stream<T>`).

**Q:** Real-world flatMap usage?
**A:** Flattening a list of lists, extracting words from a list of sentences.

**Q:** Why introduce default & static methods in interfaces?
**A:** To add new behavior to interfaces without breaking existing implementations.

**Q:** Conflict when two interfaces define same default method?
**A:** Implementing class must override and explicitly resolve.

**Q:** Java Time API advantages over `Date`/`Calendar`?
**A:** Immutable, thread-safe, clearer API design, better methods.

**Q:** What makes a class immutable?
**A:** Declare class `final`, fields `private final`, provide getters only, and defensively copy mutable fields like `Date`.

---

### 3. Core Java & OOP

**Q:** Singleton class steps?
**A:** Private constructor, private static instance, public static `getInstance()`.

**Code Example:**

```java
public final class Singleton {
    private static final Singleton INSTANCE = new Singleton();
    private Singleton() {}
    public static Singleton getInstance() {
        return INSTANCE;
    }
}
```

**Q:** Difference between Comparator and Comparable?
**A:** `Comparable` (implements `compareTo`) defines natural ordering inside the class.
`Comparator` is external, allows multiple custom orderings.

**Q:** Advantages of `enum` over constants?
**A:** Type safety, can include fields/methods, can implement interfaces (but cannot extend classes).

**Q:** Example payment methods with enums?
**A:**

```java
enum PaymentType { CREDIT_CARD, UPI, NET_BANKING; }
```

Use in a `switch` to handle payment logic.

---

### 4. Optional & Null Safety

**Q:** Purpose of `Optional`?
**A:** Avoid `NullPointerException` using methods like `isPresent()`, `orElse()`.
Not recommended as a return type of getters (breaks bean conventions).

---

### 5. Testing

**Q:** JUnit 4 vs JUnit 5?
**A:** JUnit 5 introduces Jupiter API, dependency injection, new annotations (`@BeforeEach`, `@AfterEach`), parameterized tests.

**Q:** Test class visibility?
**A:** JUnit 4 requires public class; JUnit 5 does not.

---

### 6. SOLID & Design

**Q:** Single Responsibility Principle?
**A:** Each class should have one reason to change—focus on a single functionality.

**Q:** Purpose of design patterns?
**A:** Provide tested, reusable solutions that improve scalability, readability, and maintainability.

---

### 7. Git & Tools

**Q:** Common Git commands?
**A:** `git init`, `git commit -m`, `git pull`, `git fetch`, `git merge`.

**Q:** Debugging production issues?
**A:** Check ELK stack logs, add debug logs, replicate locally, verify environment differences.

---

### 8. Agile vs Waterfall

**Q:** Difference?
**A:** Agile delivers in sprints with iterative feedback; Waterfall is sequential with limited mid-project changes.

---

### 9. Stream API Coding Example

*Sum of integers in a list using Stream & reduce*:

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
int sum = nums.stream().reduce(0, Integer::sum);
System.out.println(sum);
```

---
