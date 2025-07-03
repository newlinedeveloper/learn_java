## 🔹 Core Spring

### 1. **What is the difference between `@Component`, `@Service`, and `@Repository`?**

| Annotation    | Purpose                                                        |
| ------------- | -------------------------------------------------------------- |
| `@Component`  | Generic stereotype for any Spring-managed bean.                |
| `@Service`    | Specialized for service-layer logic.                           |
| `@Repository` | Specialized for data access and enables exception translation. |

🔹 All three are detected via **component scanning**, but `@Service` and `@Repository` add semantic meaning.

---

### 2. **Explain Dependency Injection and how Spring does it.**

**Answer:**
Dependency Injection (DI) is a design pattern where dependencies are injected into a class rather than the class creating them.

Spring supports:

* **Constructor injection**
* **Field injection**
* **Setter injection**

**Example (Constructor Injection):**

```java
@Component
class CarService {
    private final Engine engine;

    @Autowired
    public CarService(Engine engine) {
        this.engine = engine;
    }
}
```

---

### 3. **What is the Spring Bean lifecycle?**

**Lifecycle stages:**

1. Bean instantiation
2. Property injection
3. `@PostConstruct` method (if defined)
4. Ready to use
5. `@PreDestroy` method (before container shuts down)

**Example:**

```java
@Component
public class MyBean {
    @PostConstruct
    public void init() {
        System.out.println("Initialized");
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("Destroyed");
    }
}
```

---

## 🔹 Spring Boot

### 4. **What is Spring Boot Auto-Configuration?**

Spring Boot automatically configures your application based on dependencies.

Example:

* If `spring-boot-starter-web` is present, it auto-configures Tomcat, Spring MVC, Jackson, etc.

You can disable or customize it using:

```java
@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })
```

---

### 5. **How do you externalize configuration using `application.properties` or `YAML`?**

You can move values out of code and into config files:

**application.properties**

```properties
app.name=MySpringApp
server.port=8081
```

**Read with `@Value`:**

```java
@Value("${app.name}")
private String appName;
```

Or use `@ConfigurationProperties` for grouping:

```java
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
}
```

---

## 🔹 REST API Development

### 6. **What is the difference between `@RequestParam`, `@PathVariable`, and `@RequestBody`?**

| Annotation      | Used For                        | Example URL/Input        |
| --------------- | ------------------------------- | ------------------------ |
| `@RequestParam` | Query parameters                | `/search?query=book`     |
| `@PathVariable` | Path values in URL              | `/users/5`               |
| `@RequestBody`  | JSON body of a POST/PUT request | `{ \"name\": \"John\" }` |

**Example:**

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable int id) { ... }

@PostMapping("/users")
public void createUser(@RequestBody User user) { ... }

@GetMapping("/search")
public List<User> search(@RequestParam String query) { ... }
```

---

### 7. **How do you handle exceptions in a Spring REST API?**

**Use `@ControllerAdvice` + `@ExceptionHandler`:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

This avoids putting try-catch blocks in every controller.

---

## 🔹 Testing

### 8. **How do you write unit tests with JUnit and Mockito?**

**Example:**

```java
@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    void testFindUser() {
        User mockUser = new User(1, "John");
        when(userRepository.findById(1)).thenReturn(Optional.of(mockUser));
        User result = userService.findById(1);
        assertEquals("John", result.getName());
    }
}
```

---

### 9. **What is the difference between unit and integration testing in Spring?**

| Type             | Scope                      | Tools / Frameworks                  |
| ---------------- | -------------------------- | ----------------------------------- |
| **Unit Testing** | Test a single class/method | JUnit, Mockito                      |
| **Integration**  | Test end-to-end behavior   | `@SpringBootTest`, TestRestTemplate |

* **Unit test:** Isolate logic with mocks.
* **Integration test:** Load Spring context and test flow between layers.

---
