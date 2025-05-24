
### **1. Default Methods in Interfaces (Java 8)**
- Introduced in Java 8, default methods allow interfaces to have method implementations.
- Helps in backward compatibility by allowing new methods without breaking existing implementations.
- Example:
  ```java
  interface MyInterface {
      default void show() {
          System.out.println("Default method in interface");
      }
  }
  
  class MyClass implements MyInterface {
      public static void main(String[] args) {
          new MyClass().show();
      }
  }
  ```
---

### **2. Private Methods in Interfaces (Java 9)**
- Java 9 introduced private methods in interfaces to improve code reusability.
- Private methods cannot be inherited or overridden.
- Example:
  ```java
  interface MyInterface {
      private void log(String message) {
          System.out.println("Log: " + message);
      }

      default void show() {
          log("Default method called");
      }
  }
  ```

---

### **3. Default vs. Static Methods in Interfaces**
| Feature           | Default Methods | Static Methods |
|------------------|----------------|---------------|
| Defined using   | `default` keyword | `static` keyword |
| Requires an instance? | Yes | No |
| Can be overridden? | Yes | No |
| Called using | Object reference | Interface name |
| Example | `obj.method()` | `Interface.method()` |

Example:
```java
interface MyInterface {
    default void defaultMethod() { System.out.println("Default method"); }
    static void staticMethod() { System.out.println("Static method"); }
}
```

---

### **4. Variable Arguments (varargs)**
- Allows passing a variable number of arguments to a method.
- Syntax: `methodName(type... variableName)`.
- Example:
  ```java
  class VarArgsExample {
      static void printNumbers(int... nums) {
          for (int num : nums) {
              System.out.print(num + " ");
          }
      }

      public static void main(String[] args) {
          printNumbers(1, 2, 3, 4, 5);
      }
  }
  ```
---

### **5. Static Method Call on null Reference**
- A static method can be called on a `null` reference since it belongs to the class, not the object.
- Example:
  ```java
  class Test {
      static void staticMethod() { System.out.println("Static method called"); }
  }

  public class Main {
      public static void main(String[] args) {
          Test obj = null;
          obj.staticMethod(); // No NullPointerException
      }
  }
  ```
---

### **6. Equals and HashCode Contract**
- **Contract**: If two objects are equal (`equals()` returns `true`), their `hashCode()` must be the same.
- Violating this leads to issues in collections like `HashSet`, `HashMap`.
- Example:
  ```java
  class Person {
      String name;
      
      @Override
      public boolean equals(Object obj) {
          if (this == obj) return true;
          if (!(obj instanceof Person)) return false;
          return name.equals(((Person) obj).name);
      }

      @Override
      public int hashCode() {
          return name.hashCode();
      }
  }
  ```
---

### **7. Base Class vs. Abstract Class**
| Feature | Base Class | Abstract Class |
|---------|------------|----------------|
| Definition | Any parent class | A class with at least one abstract method |
| Can be instantiated? | Yes | No |
| Contains abstract methods? | No | Yes (can have concrete methods too) |
| Purpose | Code reuse | Inheritance with enforced method implementation |

Example:
```java
abstract class Animal {
    abstract void makeSound();
}

class Dog extends Animal {
    void makeSound() { System.out.println("Bark"); }
}
```

---

### **8. Marker Interface**
- An interface with no methods, used to provide metadata to classes.
- Example: `Serializable`, `Cloneable`.
- Example:
  ```java
  interface Marker {}

  class MyClass implements Marker {}
  ```
---

### **9. Volatile Keyword**
- Ensures visibility of changes to variables across threads.
- Prevents compiler and CPU from reordering instructions.
- Example:
  ```java
  class SharedResource {
      volatile boolean flag = true;
  }
  ```

---

### **10. Functional Interface Without Abstract Method?**
- A functional interface must have **exactly** one abstract method.
- If an interface has only default/static methods, it's **not** a functional interface.
- Example (Invalid Functional Interface):
  ```java
  @FunctionalInterface
  interface InvalidInterface {
      default void method1() {}
      static void method2() {}
  }
  ```

---

### **11. TreeSet with null Values**
- `TreeSet` **does not allow `null`** if it uses natural ordering (`Comparable`).
- Example:
  ```java
  TreeSet<String> set = new TreeSet<>();
  set.add(null); // Throws NullPointerException
  ```
- However, if we use a **custom comparator**, `null` can be handled.

---

### **12. finally Block Execution with return or System.exit()**
- `finally` always executes **except** when:
  - `System.exit(0)` is called.
  - The JVM crashes.
- Example:
  ```java
  class Test {
      public static void main(String[] args) {
          try {
              System.out.println("Try block");
              return;
          } finally {
              System.out.println("Finally block"); // Executes even after return
          }
      }
  }
  ```
---

### **13. Microservices Components**
1. **API Gateway**: Manages API requests (e.g., Spring Cloud Gateway).
2. **Service Discovery**: Keeps track of microservices (e.g., Eureka, Consul).
3. **Load Balancer**: Distributes traffic (e.g., Ribbon, Kubernetes LoadBalancer).
4. **Service Registry**: Stores service information (e.g., Eureka, Zookeeper).
5. **Inter-service Communication**: REST, gRPC, Kafka, RabbitMQ.
6. **Circuit Breaker**: Prevents cascading failures (e.g., Resilience4j, Hystrix).
7. **Configuration Management**: Centralized config (e.g., Spring Cloud Config).
8. **Logging & Monitoring**: Logs & metrics (e.g., ELK, Loki, Prometheus, Grafana).
9. **Security**: Authentication/Authorization (e.g., OAuth2, JWT, Spring Security).
10. **Distributed Tracing**: Tracks requests across services (e.g., Zipkin, Jaeger).

---
