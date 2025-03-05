# **Testing in Java**

Testing is crucial in Java development to ensure code quality, correctness, and maintainability. Java provides robust testing frameworks such as **JUnit** for unit testing and **Mockito** for mocking dependencies. Additionally, **Spring Boot** offers tools for **integration testing**.

---

## **1. JUnit - Unit Testing in Java**
### ✅ **What is JUnit?**
JUnit is a widely used **unit testing framework** for Java that:
- Automates the testing process.
- Uses annotations (`@Test`, `@BeforeEach`, etc.) for test setup and execution.
- Provides assertions to verify expected outcomes.

### ✅ **JUnit Dependencies (JUnit 5)**
Add JUnit 5 (Jupiter) to your Maven/Gradle project.

#### **For Maven (`pom.xml`)**
```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <scope>test</scope>
</dependency>
```

#### **For Gradle (`build.gradle`)**
```gradle
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.1'
}
```

---

### ✅ **Writing a JUnit Test Case**
Let's test a simple **Calculator** class.

#### **Step 1: Create the Calculator Class**
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}
```

#### **Step 2: Create the Test Class**
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {
    private final Calculator calculator = new Calculator();

    @Test
    void testAddition() {
        assertEquals(5, calculator.add(2, 3));
    }

    @Test
    void testSubtraction() {
        assertEquals(2, calculator.subtract(5, 3));
    }
}
```
### 🔹 **Key JUnit Assertions**
- `assertEquals(expected, actual)` → Checks if values are equal.
- `assertTrue(condition)` → Verifies if a condition is `true`.
- `assertFalse(condition)` → Ensures a condition is `false`.
- `assertThrows(Exception.class, () -> methodCall())` → Validates exceptions.

---

## **2. Mockito - Mocking Dependencies**
### ✅ **Why Use Mockito?**
- Mockito **creates mock objects** for testing without relying on actual implementations.
- Helps in **unit testing** services with dependencies (e.g., repositories, external APIs).
- Avoids **complex setup** for database access and network calls.

### ✅ **Mockito Dependency**
#### **For Maven**
```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <scope>test</scope>
</dependency>
```

#### **For Gradle**
```gradle
dependencies {
    testImplementation 'org.mockito:mockito-core:4.0.0'
}
```

---

### ✅ **Example: Mocking a Repository in a Service Class**
Let's mock a repository using **Mockito**.

#### **Step 1: Create the UserRepository and UserService**
```java
import java.util.Optional;

public interface UserRepository {
    Optional<User> findById(Long id);
}

public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUserName(Long userId) {
        return userRepository.findById(userId)
                .map(User::getName)
                .orElse("User Not Found");
    }
}
```

#### **Step 2: Write a Test Case Using Mockito**
```java
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
import java.util.Optional;
import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

class UserServiceTest {
    private final UserRepository userRepository = mock(UserRepository.class);
    private final UserService userService = new UserService(userRepository);

    @Test
    void testGetUserName() {
        User mockUser = new User(1L, "John Doe");
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));

        String result = userService.getUserName(1L);
        assertEquals("John Doe", result);

        verify(userRepository, times(1)).findById(1L);
    }
}
```
### 🔹 **Key Mockito Methods**
- `mock(Class.class)` → Creates a mock object.
- `when(mock.method()).thenReturn(value)` → Defines mock behavior.
- `verify(mock, times(n)).methodCall()` → Ensures the method was called `n` times.

---

## **3. Integration Testing in Spring Boot**
### ✅ **What is Integration Testing?**
- **Integration tests** verify how different components of an application **work together** (e.g., Controllers, Services, Repositories).
- Uses **Spring Boot Test** and **TestContainers** (for databases).

### ✅ **Spring Boot Test Dependency**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

### ✅ **Writing a REST API Integration Test**
Let's test a **Spring Boot REST API**.

#### **Step 1: Create a REST Controller**
```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {
    @GetMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return "User " + id;
    }
}
```

#### **Step 2: Write an Integration Test Using `MockMvc`**
```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@SpringBootTest
@AutoConfigureMockMvc
class UserControllerTest {
    @Autowired
    private MockMvc mockMvc;

    @Test
    void testGetUser() throws Exception {
        mockMvc.perform(get("/users/1"))
                .andExpect(status().isOk())
                .andExpect(content().string("User 1"));
    }
}
```
### 🔹 **Key Annotations for Integration Testing**
- `@SpringBootTest` → Loads the application context.
- `@AutoConfigureMockMvc` → Configures `MockMvc` for API testing.
- `mockMvc.perform(get("/url"))` → Calls an API endpoint.
- `.andExpect(status().isOk())` → Verifies HTTP 200 response.

---

# **4. Summary**
| **Testing Type**  | **Framework**  | **Usage**  |
|-------------------|---------------|------------|
| **Unit Testing**  | JUnit          | Tests individual methods and classes. |
| **Mocking**       | Mockito        | Simulates dependencies for isolated testing. |
| **Integration Testing** | Spring Boot Test | Tests interactions between multiple components (Controllers, Services, Databases). |

---
