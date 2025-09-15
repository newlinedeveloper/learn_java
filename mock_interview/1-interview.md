## Java Core & Collections

**Q1. Introduce yourself and your recent project**

* Candidate describes \~5 years of experience in Java, Spring Boot, microservices, Kafka, AWS (S3, CloudWatch, EKS), and Kubernetes.

**Q2. Collection frameworks used in your project**

* Commonly used: `List`, `ArrayList`, `Map`, `HashSet`, `TreeSet`.

**Q3. Null values in List, Set, Map**

* **List**: Allows multiple nulls.
* **Set**: Allows only one null.
* **Map**: Allows one null key, multiple null values (depends on implementation).

**Q4. ArrayList vs LinkedList**

* **ArrayList**: Dynamic array; faster random access, slower insert/delete in middle.
* **LinkedList**: Faster insert/delete, slower random access.

**Q5. Maintaining insertion order in Set**

* Use `LinkedHashSet` to maintain insertion order.

**Q6. HashMap vs LinkedHashMap vs TreeMap**

* **HashMap**: Unordered, uses hashing.
* **LinkedHashMap**: Maintains insertion order.
* **TreeMap**: Sorted by keys (Red-Black tree).

**Q7. Why override both equals() and hashCode()?**

* To ensure consistent behavior when objects are used as keys in hash-based collections.

**Q8. Modify object after storing in HashSet**

* If a field used in hashCode changes, the object might be “lost” because its bucket changes.

**Q9. Fail-fast vs Fail-safe iterators**

* **Fail-fast**: Throw `ConcurrentModificationException` if modified during iteration.
* **Fail-safe**: Iterate over a copy; no exception but may not see latest changes.

**Q10. ConcurrentHashMap vs SynchronizedMap**

* **ConcurrentHashMap**: Segment locking, better concurrency, no null keys/values.
* **SynchronizedMap**: Locks entire map, lower performance.

**Q11. Comparable vs Comparator**

* **Comparable**: Natural ordering, implement `compareTo()`.
* **Comparator**: External ordering, implement `compare()`.

**Q12. Functional Interface**

* Interface with a single abstract method (e.g., `Runnable`, `Callable`).

**Q13. HashMap time complexity**

* Average O(1) for get/put.

**Q14. Thread-safe map with more reads than writes**

* Use `ConcurrentHashMap`.

**Q15. Hash collisions**

* Different objects can share the same hash code.

---

## Java OOP & Language

**Q16. Inheritance**

* Inheriting properties/methods from a parent class.
* Class extends class, interface implemented by class.

**Q17. Compile-time vs Runtime Polymorphism**

* **Compile-time**: Method overloading.
* **Runtime**: Method overriding.

**Q18. Encapsulation**

* Hiding internal details, exposing only what’s necessary using getters/setters.

**Q19. Abstraction without abstract class/interface**

* Not directly; need abstract class or interface.

**Q20. Overriding private or static methods**

* Private: Cannot override.
* Static: Method hiding, not overriding.

**Q21. Overloaded methods with int vs Integer and null**

* Calling with `null` invokes the `Integer` version (wrapper can hold null).

**Q22. Role of `super` keyword**

* Calls parent class methods/constructors.

**Q23. Object class role**

* Parent of all classes. Provides `equals()`, `hashCode()`, `toString()`.

---

## Spring Data JPA

**Q24. Purpose of @Entity**

* Maps a class to a database table.

**Q25. Can Entity be final?**

* No, because JPA creates proxies that require subclassing.

**Q26. @Id and @GeneratedValue**

* `@Id`: Primary key.
* `@GeneratedValue`: Auto-increment primary key.

**Q27. CrudRepository vs JpaRepository**

* `JpaRepository` extends `CrudRepository` with JPA-specific methods.

**Q28. PaginationAndSortingRepository**

* For paging and sorting queries.

**Q29. @Query annotation**

* Define custom queries.

**Q30. findById() when no record found**

* Returns `Optional.empty()`.

**Q31. JPQL vs SQL**

* JPQL operates on entities, SQL on tables.

**Q32. Native query**

* Plain SQL query executed on DB.

**Q33. Relationships**

* **One-to-Many / Many-to-One**: Student–Subjects.
* **Many-to-Many**: Teacher–Department.

**Q34. Avoid direct Many-to-Many**

* Difficult to manage in large systems; use a join table.

**Q35. Lazy vs Eager Fetching**

* Lazy: Loads association on access.
* Eager: Loads association immediately.

**Q36. Cascade types**

* Propagate operations (persist, remove) from parent to child entities.

**Q37. N+1 query problem**

* Occurs when fetching related entities causes extra queries.

**Q38. @Transactional**

* Defines transactional boundaries and rollback rules.

---

## Microservices & Spring Boot

**Q39. Why Microservices?**

* Easier deployment, scaling, independent modules vs monolithic.

**Q40. Challenges breaking monolith**

* Data partitioning, service boundaries, distributed transactions, latency.

**Q41. Key Microservices for E-commerce**

* Payment Service, Catalog Service, Order Service, Cart Service, Checkout Service.

**Q42. Microservice Communication**

* **Sync**: REST, WebClient, gRPC.
* **Async**: Kafka.

**Q43. Handling dependent service failure**

* Saga pattern, circuit breaker.

**Q44. Important Microservice Components**

* API Gateway, Service Registry (Eureka), Circuit Breaker (Hystrix/Resilience4j), AOP for logging.

---
