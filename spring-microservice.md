# **Spring Boot & Microservices**

Spring Boot is a **framework** built on **Spring** that simplifies the development of Java applications. It provides **auto-configuration, embedded servers**, and an **opinionated setup** for building REST APIs and microservices.

---

# **1. Introduction to Spring Boot**  

## ✅ **Why Use Spring Boot?**
- **Auto-configuration**: No need for complex XML configuration.
- **Embedded Servers**: Uses **Tomcat, Jetty, or Undertow** (no need to deploy WAR files).
- **Microservices Friendly**: Supports **REST, Spring Cloud, Eureka, and API Gateway**.
- **Spring Data JPA**: Simplifies **database access** with repositories.
- **Spring Security**: Built-in **authentication & authorization** support.

---

## **2. Creating a Spring Boot Application**  
You can create a Spring Boot application using:
1. **Spring Initializr** (Online tool) → [start.spring.io](https://start.spring.io/)  
2. **Maven or Gradle** (CLI or IDE)  

### 📌 **Spring Boot Maven Dependency**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
- **spring-boot-starter-web** → For building REST APIs.
- **spring-boot-starter-data-jpa** → For database access.
- **spring-boot-starter-security** → For authentication & authorization.

---

# **3. REST API Development with Spring Boot**
Spring Boot makes it easy to develop REST APIs using the `@RestController` annotation.

### ✅ **Example: Basic REST API**
```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class HelloController {
    
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot!";
    }
}
```
- `@RestController` → Marks this class as a REST API.
- `@RequestMapping("/api")` → Defines the base URL.
- `@GetMapping("/hello")` → Handles **GET** requests.

---

## **4. Spring Data JPA**
Spring Data JPA simplifies database interactions by providing an **abstraction layer over Hibernate**.

### ✅ **Step 1: Add Spring Data JPA Dependency**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```
- **H2**: An in-memory database (useful for development).

---

### ✅ **Step 2: Configure Database in `application.properties`**
```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
```

---

### ✅ **Step 3: Create an Entity Class**
```java
import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    @Column(unique = true, nullable = false)
    private String email;

    // Getters & Setters
}
```
- `@Entity` → Marks this class as a database table.
- `@Table(name = "users")` → Specifies the table name.
- `@Id` & `@GeneratedValue` → Defines primary key and auto-increment.

---

### ✅ **Step 4: Create a JPA Repository**
```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```
- `JpaRepository<User, Long>` → Provides built-in CRUD operations.

---

### ✅ **Step 5: Create a REST API for User Operations**
```java
import org.springframework.web.bind.annotation.*;
import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {
    private final UserRepository userRepository;

    public UserController(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }

    @GetMapping
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
}
```
✅ **Uses `JpaRepository` to interact with the database**  
✅ **Creates `POST` and `GET` APIs for users**

---

# **5. Spring Security & Authentication**
Spring Security provides **authentication & authorization** mechanisms using JWT, OAuth, and Role-based access control (RBAC).

### ✅ **Adding Spring Security Dependency**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### ✅ **Basic Authentication Example**
By default, Spring Security adds **HTTP Basic Authentication**.  
Use `application.properties` to define a **username & password**.
```properties
spring.security.user.name=admin
spring.security.user.password=admin123
```

### ✅ **Securing API Endpoints**
```java
import org.springframework.web.bind.annotation.*;

import org.springframework.security.access.prepost.PreAuthorize;

@RestController
@RequestMapping("/secure")
public class SecureController {

    @GetMapping("/admin")
    @PreAuthorize("hasRole('ADMIN')")
    public String adminAccess() {
        return "Welcome Admin!";
    }

    @GetMapping("/user")
    @PreAuthorize("hasRole('USER')")
    public String userAccess() {
        return "Welcome User!";
    }
}
```
- `@PreAuthorize("hasRole('ADMIN')")` → Restricts access to **ADMIN** users.
- `@PreAuthorize("hasRole('USER')")` → Restricts access to **USER** role.

---

# **6. Microservices Architecture**
Microservices architecture **breaks a monolithic application** into smaller, independent services. Each service:
- **Has its own database**
- **Communicates via REST APIs** (or gRPC)
- **Can be deployed independently**

### ✅ **Microservices Components**
1. **Service Discovery (Eureka)** → Registers & discovers services.
2. **API Gateway (Spring Cloud Gateway)** → Routes requests to microservices.
3. **Circuit Breaker (Resilience4j/Hystrix)** → Handles failures gracefully.
4. **Inter-Service Communication (Feign Client)** → Simplifies REST calls.

---

## **Example: Eureka Service Discovery**
### ✅ **Step 1: Add Eureka Server Dependency**
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

### ✅ **Step 2: Create a Eureka Server**
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

### ✅ **Step 3: Configure Eureka in `application.properties`**
```properties
server.port=8761
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```
- **Port 8761** is the default Eureka Server port.
- **Disables self-registration (for standalone servers).**

---
