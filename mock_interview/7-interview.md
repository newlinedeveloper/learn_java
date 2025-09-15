## 📌 Java Mock Interview – Questions & Answers

### Introduction & Project

**Q: Can you please introduce yourself and your recent project?**
**A:** Worked 2.5 years in Java, Spring Boot, Microservices. Banking application with multiple services. Role: create, test, and deploy services.

---

### Microservices

**Q: How are your microservices communicating with each other?**
**A:** Using Spring Cloud OpenFeign.

**Q: How are APIs communicating?**
**A:** Via OpenFeign, using defined URLs of microservices.

**Q: How do you check health of microservices?**
**A:** Using Spring Actuator.

**Q: Important actuator endpoints?**
**A:** `/health`, `/metrics`, and logging endpoints.

**Q: Which logging tool do you use?**
**A:** Using SLF4J. (Default is Logback.)

---

### Scaling & Performance

**Q: If you had to scale a Spring Boot app to handle high traffic, what strategies would you use?**
**A:** Use Eureka server (service registry) + load balancing. Also caching.

**Q: If application faces performance issues under high load, how do you identify and address them?**
**A:** Use Actuator for monitoring. Identify load balancing issues.

---

### REST & APIs

**Q: How would you consume an external REST API in Spring Boot?**
**A:** Using RestTemplate or WebClient. (Candidate had not worked on it.)

**Q: How to accept cross-origin requests from a specific frontend domain?**
**A:** Use `@CrossOrigin` annotation. (Candidate didn’t know, used Thymeleaf earlier.)

---

### Spring Data JPA

**Q: How do you enable JPA repositories?**
**A:** Add Spring Data JPA dependency, extend `JpaRepository` in repository interfaces.

**Q: Can we write custom queries in repositories?**
**A:** Yes, using `@Query` annotation or method naming conventions. Example: `findByEmail`.

**Q: What is pagination in Spring Data JPA?**
**A:** Breaks large data into small chunks/pages for better performance.

---

### Git & Branching

**Q: What is your team’s strategy for managing branches in Git?**
**A:** Branches created by manager. Devs push to feature branch, manager merges to main.

**Q: How do you resolve merge conflicts?**
**A:** Rename conflicting files/variables locally. (Candidate had limited experience.)

---

### Maven

**Q: What is Maven?**
**A:** Build automation and dependency management tool. Uses `pom.xml`.

**Q: How to optimize Maven build for large projects?**
**A:** Use parallel build (`mvn -T`). (Candidate didn’t know, interviewer explained.)

---

### Java Collections

**Q: Have you used PriorityQueue?**
**A:** Knows it works like a queue but with priority ordering.

**Q: Difference between Collection and Collections?**
**A:**

* `Collection` → interface (List, Set, Queue).
* `Collections` → utility class with static methods (sort, reverse, etc.).

**Q: What happens if you sort a list containing null values using `Collections.sort`?**
**A:** Throws `NullPointerException`.

**Q: Difference between `Collections.sort` and `Stream.sorted`?**
**A:**

* `Collections.sort` sorts in-place on a list.
* `Stream.sorted` returns a new sorted stream (Java 8 feature).

**Q: Internal algorithm of `Collections.sort`?**
**A:** Uses modified merge sort called **TimSort**.

---

### Java OOP & Patterns

**Q: Which patterns have you used?**
**A:** Singleton, Builder (via Lombok).

**Q: Explain Builder pattern.**
**A:** Used for creating objects step by step. In Lombok: `@Builder`.

**Q: How does Java decide which method to call in method overloading?**
**A:** Based on parameter types and number.

**Q: What happens if two packages have same class name?**
**A:** No compile-time error, but need fully-qualified names to avoid ambiguity.

**Q: Can you modify a final object reference in Java?**
**A:** No, final references cannot be reassigned.

**Q: What if you override equals but not hashCode in a HashMap key?**
**A:** Breaks contract → inconsistent behavior (HashMap may not find object).

---

### Threads & Concurrency

**Q: How to safely access shared resource in multithreading?**
**A:** Use `synchronized` keyword.

**Q: Have you used `volatile`?**
**A:** Yes, ensures visibility of variable updates across threads.

**Q: Have you used `@Async`?**
**A:** No.

---

### Exceptions

**Q: What happens if exception occurs in static initialization block?**
**A:** Class fails to load → `ExceptionInInitializerError`.

**Q: Difference between checked and unchecked exceptions?**
**A:**

* Checked → compile-time (IOException, SQLException).
* Unchecked → runtime (NullPointerException, ArithmeticException).

**Q: Scenario to use checked exception?**
**A:** For invalid data / I/O operations.

**Q: Purpose of finally block?**
**A:** Always executes, used for cleanup (e.g., closing connections).

---

### Method Overloading & Overriding

**Q: Issues when both overloading & overriding are used in same class hierarchy?**
**A:** Can cause confusion in method resolution. Overloading depends on parameters, overriding depends on runtime type.

---


Do you want me to also **make a PDF version of these notes** for easy revision?
