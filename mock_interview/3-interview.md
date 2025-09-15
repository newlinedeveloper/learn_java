## Java Core

**Q1. Introduce yourself & project**
(Not technical – skipped in notes)

**Q2. Heap vs Stack usage**

* **Heap**: Stores objects created with `new`.
* **Stack**: Stores method frames, local variables, and references (e.g., static/class-level variables).

**Q3. Can two different objects share the same reference?**

* **No**. Each object has a unique memory address.

**Q4. Recursion without base condition – which memory overflows first?**

* **Stack memory** overflows first → `StackOverflowError`.

**Q5. Garbage Collection & Need**

* Reclaims memory of unreferenced objects to improve performance.

**Q6. Types of Garbage Collectors**

* **Serial**: Single-threaded.
* **Parallel**: Multi-threaded.
* **G1**: Region-based collector.

**Q7. Can memory leaks occur despite GC?**

* Yes, if objects remain referenced (e.g., static collections, unremoved listeners).

**Q8. Troubleshooting OutOfMemoryError**

* Check infinite loops/recursion, review heap dumps, identify unclosed resources.

**Q9. Ways to Create Objects**

* `new` keyword
* `Class.forName().newInstance()` (reflection)
* `clone()` method
* Deserialization

**Q10. Java Generics – purpose**

* Provides compile-time type safety and eliminates explicit casting.

**Q11. Can you create an instance of a generic type parameter?**

* **No**, due to type erasure at runtime.

---

## Spring Boot

**Q12. What is Spring Boot?**

* Simplifies Spring app development by removing boilerplate configuration.

**Q13. Why prefer Spring Boot for Microservices?**

* Embedded servers, auto-configuration, easy deployment, minimal setup.

**Q14. @SpringBootApplication purpose**

* Combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.

**Q15. Explain those three annotations**

* **@Configuration**: Marks class as source of bean definitions.
* **@EnableAutoConfiguration**: Auto-configures beans based on classpath.
* **@ComponentScan**: Scans for components, services, etc.

**Q16. What is Auto-Configuration? How to disable?**

* Automatically configures beans.
* Disable with `@SpringBootApplication(exclude = {ClassName.class})`.

**Q17. Spring Boot Starters**

* Predefined dependencies for specific features (e.g., `spring-boot-starter-web`).

**Q18. Custom Starter Steps**

* Create auto-config class, list it in `spring.factories`, package & publish.

**Q19. application.properties vs application.yml**

* Both store config.
* `.properties`: key=value pairs.
* `.yml`: hierarchical, cleaner.
* If both exist, **properties** has higher priority.

**Q20. Profiles & Activation**

* `@Profile` selects beans/config for env (dev, qa, prod).
* Activate via `spring.profiles.active` in properties or CLI.

**Q21. What if no profile is active?**

* Uses `application.properties` default configuration.

**Q22. Packaging as JAR/WAR**

* Use `spring-boot-maven-plugin` and `mvn clean package` to create executable JAR.

**Q23. Ways to Run Spring Boot App**

* From IDE
* Command line: `java -jar app.jar`

---

## Testing

**Q24. JUnit 4 vs JUnit 5**

* JUnit 5 supports `@BeforeEach`, `@AfterEach`, nested tests, and extensions (`@ExtendWith`).

**Q25. Mockito @Mock vs @InjectMocks**

* **@Mock**: Creates mock objects.
* **@InjectMocks**: Injects mocks into the tested class.

**Q26. Mocking Repository Example**

```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    @Mock UserRepository repo;
    @InjectMocks UserService service;
}
```

**Q27. Testing Exceptions with Mockito/JUnit**

```java
assertThrows(CustomException.class,
    () -> service.method());
```

**Q28. @SpringBootTest**

* Loads full application context for integration testing.

**Q29. @DataJpaTest**

* Loads only JPA components, rolls back transactions after each test.

**Q30. Control Embedded Server Startup**

* `@SpringBootTest(webEnvironment = WebEnvironment.NONE)` disables server.

**Q31. Testcontainers**

* Library to run real Docker containers (e.g., DB) for integration tests.

**Q32. Handling flaky CI/CD tests**

* Check environment configs, mock setup, version mismatches.

**Q33. Test Coverage**

* Percentage of code executed by tests. Tools: SonarQube, JaCoCo.

**Q34. Unit vs Integration Testing**

* **Unit**: Tests individual methods/classes.
* **Integration**: Tests combined modules (e.g., REST API + DB).

**Q35. Best Testing Practices**

* Write unit tests for every service.
* Maintain 80–85% coverage.
* Mock external dependencies.

---

## Miscellaneous

**Q36. CI/CD Pipeline Failures**

* Check Maven paths, environment configs, dependency versions, or mocking issues.

**Q37. Other Test Frameworks**

* TestNG is an alternative to JUnit.

---
