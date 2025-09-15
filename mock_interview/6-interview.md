Here’s a **well-structured Q & A learning document** distilled from the transcript you shared (**Java + Spring Boot Mock Interview – 18 yrs Experience**).
Each item lists the *question* followed by the *candidate’s answer/insight* so you can use it directly as study notes.

---

## Java & Spring Boot – Mock Interview Notes

### Background & Experience

1. **Introduce yourself and recent project**

   * 18 yrs Java/Spring experience, legacy tech (JSP, EJB, Struts, Hibernate) → migrated to Spring Boot & modular architecture.
   * Skilled in PL/SQL optimization and automation with shell scripts.

2. **Challenges migrating a legacy monolith to Spring Boot**

   * Deciding what and how to migrate.
   * Lack of familiarity with new tech stack.
   * Original app was a large monolith built on Hibernate.

3. **Recent high-availability system architecture**

   * Initial prototype used only JSON + browser local/session storage (no DB).
   * Later realized with Spring Boot + database (Spring Boot 2.6, Java).

---

### System Design & Scalability

4. **Designing for scalability & resilience**

   * Discussed **CAP theorem** (Consistency, Availability, Partition tolerance).
   * Project ran on a single VM so horizontal scalability was limited; consistency was prioritized.

5. **Cloud usage**

   * Deployed on Azure VM but not using native cloud services due to client restrictions.

---

### Algorithms & Data Structures

6. **Complex algorithm implemented**

   * Used a **MultiValueMap** (key → multiple values) to handle MAC-address/serial-number keys that could be unique or duplicate.

7. **Concurrency model**

   * Limited real-world use, but understands **ConcurrentHashMap** to avoid race conditions vs. regular HashMap.

---

### Performance & Optimization

8. **Performance tuning experience**

   * Used **VisualVM** to analyze heap dumps from AWS logs, identify memory/time hotspots.
   * Suggested SQL indexing improvements to cut query time.

9. **General Java performance tips**

   * Avoid creating objects/variables inside tight loops.
   * Review code for unnecessary allocations.

---

### Spring / Spring Boot

10. **Common Spring issues**

    * Version mismatch with classic Spring → solved by Spring Boot’s auto-dependency management.

11. **Configuration management for multiple environments**

    * Use **Spring Profiles**, `spring.profiles.active` in properties or `-Dspring.profiles.active=<profile>` at runtime.

12. **Custom Spring Boot starter**

    * No direct custom starter created, but knows using Spring Initializr and concept of starters (e.g., spring-boot-starter-jpa).

13. **Performance analysis tools**

    * JUnit + **JProfiler** for load testing and method-level timing.

14. **Asynchronous operations**

    * Implemented email sending and SFTP file monitoring using Spring’s async capabilities.
    * Faced SFTP connection/password-reset challenges.

15. **Testing frameworks**

    * **JUnit**, **Mockito**, and Selenoid for UI automation.
    * High Sonar coverage targets (up to 95% branch coverage using Cobertura/JaCoCo).

16. **Dependency Injection & Cyclic Dependencies**

    * Understands concept, but no major cyclic-dependency cases encountered.

17. **Advanced Spring Boot features**

    * Primarily uses core features; no reactive programming yet.

---

### Security & Data Handling

18. **Securing sensitive data**

    * No direct implementation of encryption at rest/in transit; projects ran in isolated environments.

19. **Password encoding/decoding**

    * No direct implementation.

---

### Java Language Topics

20. **Default methods in interfaces**

    * Provide method bodies inside interfaces; implementing classes need not override them.

21. **Streams & Lambdas**

    * Benefits: less boilerplate, no anonymous inner classes, concise code.

22. **Encapsulation**

    * Hides internal data; limits direct field access for security and maintainability.

23. **SOLID principles in practice**

    * Learned to keep interfaces single-purpose during peer review to avoid deployment issues.

24. **Handling technical disasters**

    * Production DB table accidentally deleted → restored from daily VM backups using shell scripts.

25. **Mentoring juniors**

    * Code reviews, enforcing naming conventions & Sonar rules, pair programming.

---

### CI/CD & Deployment

26. **CI/CD pipeline experience**

    * Used **TeamCity**; some Jenkins experience.
    * For older projects, PowerShell + manual VM deployments due to client restrictions.

27. **Blue-Green / Canary deployments**

    * Knows theory: deploy to a parallel environment and switch traffic to reduce downtime.

28. **Innovative solutions delivered**

    * Built end-to-end mock app with JSON before DB existed.
    * Automated React build & remote deployment via scripts (npm build → zip → SFTP → remote unzip/start).

---

### General & Miscellaneous

29. **Staying updated**

    * Reads LinkedIn articles, listens to tech podcasts, follows AI & cloud trends.

30. **Latest interesting tech learned**

    * Real-time translation headphones/devices.

---
