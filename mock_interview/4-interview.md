## Java & Spring Boot Mock Interview – Key Questions & Answers

### Introduction / Project Background

* **Q: Introduce yourself and describe your recent project.**
  **A:** 3.5 years of experience in Java, Spring Boot, and microservices. Currently working in the logistics domain building a compliance system to manage vessel movements across countries. Uses Agile with 2-week sprints, daily tasks, unit and regression testing.

---

### Core Java & Concurrency

1. **Thread life cycle states** – New → Runnable → Running → Waiting/Timed Waiting/Blocked → Terminated.
2. **Runnable vs Callable** – Runnable doesn’t return a result or throw checked exceptions. Callable returns a value via `Future` and can throw checked exceptions.
3. **Ensuring thread safety without `synchronized`** – Use `AtomicInteger` for atomic operations like increment.
4. **Volatile keyword** – Ensures visibility of changes across threads by writing directly to main memory.
5. **Atomic classes vs synchronized block** – Atomic classes use lock-free operations (faster under low contention). `synchronized` uses intrinsic locks and can block threads.
6. **Multiple locks & deadlocks** – Threads can acquire multiple locks; inconsistent ordering causes deadlocks. Detect using tools like JConsole/VisualVM.
7. **wait() vs notify() vs notifyAll()** – `wait()` pauses a thread, `notify()` wakes one waiting thread, `notifyAll()` wakes all.
8. **ThreadPoolExecutor** – Creates and manages a pool of reusable worker threads.
9. **submit() vs execute()** – `execute()` runs a Runnable without a result; `submit()` returns a `Future` and can take Callable.
10. **synchronized keyword** – Ensures only one thread executes a block/method at a time and guarantees visibility.
11. **Java Memory Model (JMM)** – Defines how threads interact through memory: guarantees *visibility* and *atomicity*.

---

### Design Patterns

12. **Why design patterns?** – Provide proven, maintainable solutions and common understanding for developers.
13. **Singleton pattern** – Only one instance of a class. Make constructor private, create a static instance, provide a static getter. Use `synchronized` for thread safety and `readResolve()` to prevent breaking through serialization. Reflection can also break singleton if not handled.
14. **Factory vs Abstract Factory** – Factory provides one method to create objects. Abstract Factory provides an interface for creating families of related objects without specifying concrete classes.
15. **Builder pattern** – Helps construct complex objects step by step, avoiding telescoping constructors.

---

### Unit Testing

16. **Writing JUnit 5 tests** – Mock dependencies with `@Mock`, inject with `@InjectMocks`, use `when()` for stubbing and `assertEquals()` for assertions.
17. **JUnit 4 vs 5 `@Test`** – JUnit 5 uses `assertThrows` instead of `expected` attribute, supports more flexible extensions.
18. **@DataJpaTest** – Slice test for JPA repositories with in-memory database.
19. **Mocking external APIs** – Use MockMvc, Mockito stubbing, or WireMock to simulate external service calls.

---

### Microservices & Spring Boot

20. **Microservice principles** – Single responsibility, loose coupling, independent deployment, each service has its own database, communication via queues/Kafka, service registry for discovery.
21. **Service discovery** – Tools like Eureka or Consul register and locate microservices, also provide load balancing.
22. **API Gateway** – Acts as a single entry point, hides internal service URLs, handles routing, security, and rate limiting.
23. **Securing microservices** – Authentication/authorization (Spring Security, JWT), role-based access (`@PreAuthorize`).
24. **Spring Cloud Config Server** – Centralizes configuration stored in Git. Clients fetch configuration at runtime.
25. **Dynamic config refresh** – Use Spring Cloud Bus to push updates to clients without restarting.
26. **Resilience4j retry/fallback** – Automatic retries and fallback methods to handle failures.
27. **Handling service failure** – Use circuit breaker patterns, TTL on queue messages to avoid backlog.

---

### Inter-service Communication

28. **RestTemplate, WebClient, Feign Client**

* RestTemplate: synchronous/blocking REST calls.
* WebClient: reactive, non-blocking.
* Feign: declarative REST client using interfaces and annotations.

---

### Stream API Coding

29. **Sum of even numbers using Streams**:

```java
int sum = Arrays.stream(new int[]{1,2,3,4,5,6})
                .filter(n -> n % 2 == 0)
                .sum();
System.out.println(sum); // 12
```

---
