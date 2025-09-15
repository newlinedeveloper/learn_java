# 📘 Java Mock Interview Q\&A Notes (3.4 Yrs Experience)

## 🔹 Introduction

**Q: Can you introduce yourself and your recent project?**
**A:** Worked at TCS (SBI project). Tech: Java, Spring Boot, PostgreSQL, GitLab. Handled UPI module in payment system.

---

## 🔹 Strings & Immutability

**Q: Difference between String, StringBuilder, and StringBuffer?**

* String → Immutable, stored in String pool.
* StringBuilder → Mutable, not thread-safe.
* StringBuffer → Mutable, thread-safe (synchronized).

**Q: Why is String immutable in Java?**

* Better memory management via String pool.
* Security (credentials, class loading).
* Thread safety.

**Q: Examples of immutable classes in Java?**

* Integer, Float, Boolean, BigDecimal.

**Q: Risks if Strings were mutable (multi-threading)?**

* Two threads modifying same String → inconsistent/overwritten values (e.g., payments).

**Q: How does `equals()` differ from `==` in Strings?**

* `==` → compares reference (memory address).
* `equals()` → compares actual String content.

**Q: What issue in authentication if `==` is used instead of `equals()`?**

* Even correct credentials may fail (as `==` checks references).

**Q: What is String Constant Pool?**

* Special memory area in heap for String literals.
* Prevents duplicate object creation by reusing existing Strings.

**Q: What happens internally when concatenating Strings with `+` vs StringBuilder?**

* `+` → Creates new String object in pool (less efficient).
* `StringBuilder` → Modifies same object (better performance).

---

## 🔹 Immutability Concepts

**Q: What is an immutable object in Java?**

* Class marked `final`.
* Fields: `private final`.
* No setters.

**Q: Advantages/Disadvantages of immutability?**

* ✅ Thread safety, security, caching.
* ❌ Frequent object creation → more garbage collection.

**Q: How does immutability improve thread safety?**

* Multiple threads can read safely, as values don’t change.
* Example: Banking transactions.

---

## 🔹 Serialization

**Q: What is Serialization in Java?**

* Process of converting object → byte stream (to send over network/store in file).

**Q: Have you used `serialVersionUID`?**

* Candidate: No.

---

## 🔹 Spring & Dependency Injection

**Q: What is Dependency Injection (DI) in Spring?**

* Framework injects required objects into classes instead of manual creation.
* Example: Repository injected into Service.

**Q: How does IoC (Inversion of Control) improve modularity/testability?**

* Spring manages bean lifecycle.
* Loose coupling, easier unit testing.

**Q: Types of Dependency Injection?**

* Constructor Injection.
* Setter Injection.
  (Candidate was unsure.)

**Q: How to implement DI without Spring?**

* Manual object creation and passing dependencies in core Java. (Candidate: No experience.)

---

## 🔹 Spring MVC & Annotations

**Q: Difference between `@Controller` and `@RestController`?**

* `@Controller` → Returns views (HTML, JSP).
* `@RestController` → Combines `@Controller + @ResponseBody` → returns JSON/XML directly.

**Q: Common HTTP request types?**

* GET, POST, PUT, DELETE, PATCH.
  (Current project: Only GET, POST used.)

**Q: Which is more secure: GET or POST?**

* POST → More secure (data not visible in URL).

**Q: Status codes examples?**

* 200 → OK.
* 201 → Created.
* 204 → No Content (for delete).
* 400 → Bad Request.
* 401 → Unauthorized.
* 404 → Not Found.
* 500 → Internal Server Error.

**Q: Difference between `@RequestMapping` and `@GetMapping`?**

* `@RequestMapping` → Generic, can handle multiple HTTP methods.
* `@GetMapping` → Specialized shortcut for GET.

---

## 🔹 Security

**Q: How do you secure REST APIs?**

* Using PGP encryption + keys.
* Access tokens.
* JWT (3 parts: Header, Payload, Signature).

**Q: Difference between Authentication & Authorization?**

* Authentication → Verifying identity (username/password).
* Authorization → Verifying access rights (what user can do).

---

## 🔹 Spring Boot & Maven

**Q: Role of `pom.xml`?**

* Defines dependencies, build configuration.

**Q: What is a Spring Boot Starter?**

* Preconfigured set of dependencies (e.g., `spring-boot-starter-web`).

**Q: Which server does Spring Boot use by default?**

* Tomcat. Can switch to Jetty by changing dependency.

**Q: Difference between `@Service` and `@Repository`?**

* `@Service` → Business logic layer.
* `@Repository` → DAO layer (interacts with DB).
  (Can be interchanged technically, but not best practice.)

**Q: Good practices for REST APIs?**

* Return proper status codes.
* Proper error messages.
* Use correct headers.
* Follow naming conventions.

---

## 🔹 Git & Collaboration

**Q: Which Git tool are you using?**

* GitLab.

**Q: How do you resolve conflicts?**

* Locally in IDE (Eclipse/IntelliJ).
* Or via GitLab UI (Resolve Conflict option).

**Q: Do you know about Git Rebase?**

* Candidate: No.
  (Interviewer explained → Rebase makes branch history identical to another branch.)

**Q: Do you know about Git Cherry Pick?**

* Candidate: No.
  (Interviewer explained → Used to pick specific commit(s) from one branch into another.)

---
