## Java Core

**Q1.** What happens if a class implements `Comparable` and you use a custom `Comparator` in sorting?
**A.** The custom `Comparator` takes precedence and overrides the natural ordering defined by `Comparable`.

**Q2.** Explain the internal working of `HashMap` in Java 8 vs Java 7.
**A.**

* Uses an array of buckets (hash table).
* Key’s hashCode determines bucket index.
* Collisions store entries in a linked list.
* **Java 8 change:** when a bucket’s list grows beyond a threshold, it converts to a balanced tree (red-black tree) to improve lookup from O(n) to O(log n).

**Q3.** How does Java ensure visibility of shared data in multithreading without `synchronized`?
**A.** Through the **Java Memory Model** and the `volatile` keyword which ensures changes are visible across threads.

**Q4.** What happens when you create a new object in Java?
**A.**

* Memory is allocated on the **heap**.
* A reference is stored on the **stack**.
* When no reference remains, the object becomes eligible for **garbage collection**.

**Q5.** Difference between `final`, effectively final, and immutable.
**A.**

* `final` – Java keyword to prevent reassignment/extension/overriding.
* **Effectively final** – a variable not declared final but never reassigned (used in lambdas).
* **Immutable** – object whose state cannot change after construction (e.g. `String`).

**Q6.** What is Fork/Join Pool?
**A.** A framework that breaks tasks into subtasks and joins results; used by Java parallel streams.

**Q7.** Can `ConcurrentHashMap` store `null` values?
**A.** No. Null keys or values are not allowed to avoid ambiguity in concurrent operations.

**Q8.** Purpose of `ThreadLocal`.
**A.** Stores data isolated to each thread—each thread gets its own copy.

---

## Spring & Spring Boot

**Q9.** How does Spring resolve circular dependencies at runtime?
**A.** By creating **proxies** and using **setter injection** or **lazy initialization**. Constructor injection alone cannot resolve circular dependencies.

**Q10.** Difference between `@Mock` and `@MockBean`.
**A.**

* `@Mock` – Mockito annotation for plain unit tests.
* `@MockBean` – Registers a Mockito mock as a Spring bean, replacing the real bean in the application context.

**Q11.** What if a bean is defined in multiple configuration files with the same name?
**A.** Ambiguity occurs. Use `@Primary` or `@Qualifier` to specify which bean to inject.

**Q12.** `@ConfigurationProperties` returns null—causes?
**A.** Missing `@EnableConfigurationProperties`, missing `@Component` on the class, or no getters/setters.

**Q13.** How does Thread scope work in Spring?
**A.** The bean’s lifecycle is tied to a single thread. Not suitable for `@Async` methods since they may run on different threads.

**Q14.** What is `NoSuchBeanDefinitionException`?
**A.** Thrown when Spring cannot find a requested bean in the application context.

**Q15.** Ensuring performance for large paginated queries in Spring Data JPA.
**A.** Use proper pagination (`Pageable`), indexes, caching, and limit the result set.

**Q16.** Example of `@ManyToOne`.
**A.** In a banking app: many `Customer` entities relate to one `Bank` entity.

**Q17.** Deleting a parent entity with `@OneToMany(cascade = CascadeType.ALL)`.
**A.** Deletes all child entities automatically.

**Q18.** Enforcing uniqueness across multiple fields in JPA.
**A.** Use `@Table(uniqueConstraints = @UniqueConstraint(columnNames = {"col1","col2"}))`.

**Q19.** Implementing **idempotency** in a POST payment API.
**A.** Accept an **Idempotency-Key** (e.g., UUID) from the client, store it, and return the stored response if the same key is received again.

**Q20.** Microservice goes down under sudden load—checks?
**A.** Check memory usage, logs, thread dumps, load balancer configuration, and external service dependencies.

**Q21.** Calling three microservices in parallel, one fails—retry strategy?
**A.** Use **Circuit Breaker** (e.g., Resilience4j/Hystrix) and/or **Saga pattern** for transaction rollback.

**Q22.** Purpose of Spring Boot DevTools.
**A.** Provides live reload, automatic restart, and enhanced development-time experience.
**Not for production** due to performance and security concerns.

**Q23.** How to store GitHub secrets securely for CI/CD?
**A.** Use cloud secret managers (e.g., Azure Key Vault, AWS Secrets Manager) and fetch secrets in pipelines.

**Q24.** Production performance degradation—profiling steps.
**A.** Check slow queries, analyze logs/metrics (e.g., JProfiler, VisualVM, Actuator metrics), optimize code or DB queries, introduce caching, reduce payloads.

---

## Coding with Java Streams (from live coding round)

**Q25.** Print the first non-repeating number in an array using Java 8 Streams.

```java
List<Integer> list = Arrays.asList(1,2,3,1,2);
Optional<Integer> firstNonRepeat = list.stream()
    .collect(Collectors.groupingBy(x -> x, LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(e -> e.getValue() == 1)
    .map(Map.Entry::getKey)
    .findFirst();
System.out.println(firstNonRepeat.orElse(null)); // 3
```

**Q26.** Sum of all numbers in a list using Streams.

```java
int sum = list.stream().reduce(0, Integer::sum);
System.out.println(sum);
```

---
