## **Exception Handling in Java**  

Exception handling in Java is a mechanism that allows us to handle runtime errors gracefully and prevent program crashes. Java provides the `try`, `catch`, `finally`, and `throw` keywords to manage exceptions effectively.

---

## **1️⃣ try, catch, finally**  

### **🔹 Basic Structure**  

```java
try {
    // Code that may cause an exception
} catch (ExceptionType e) {
    // Handle exception
} finally {
    // Code that will always execute
}
```

### **🔹 Example**
```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;  // Division by zero (ArithmeticException)
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("Exception caught: " + e.getMessage());
        } finally {
            System.out.println("This block always executes.");
        }
    }
}
```
**📝 Output:**  
```
Exception caught: / by zero  
This block always executes.
```
**🛠 Explanation:**  
- The `try` block contains code that may generate an exception.  
- The `catch` block handles the exception.  
- The `finally` block **always executes**, whether an exception occurs or not.

---

## **2️⃣ Throwing and Handling Exceptions**  

### **🔹 Using `throw` to Manually Throw Exceptions**  
The `throw` keyword is used to **explicitly throw an exception**.

#### **Example: Throwing an Exception**
```java
public class ThrowExample {
    static void validateAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be 18 or above.");
        } else {
            System.out.println("Access granted.");
        }
    }

    public static void main(String[] args) {
        validateAge(16);  // This will throw an exception
    }
}
```
**📝 Output:**  
```
Exception in thread "main" java.lang.IllegalArgumentException: Age must be 18 or above.
```

---

### **🔹 Using `throws` to Declare Exceptions**  
The `throws` keyword indicates that a method **might throw an exception**, and the caller must handle it.

#### **Example: Method Declaring Exception**
```java
public class ThrowsExample {
    static void divide(int a, int b) throws ArithmeticException {
        if (b == 0) {
            throw new ArithmeticException("Cannot divide by zero.");
        }
        System.out.println("Result: " + (a / b));
    }

    public static void main(String[] args) {
        try {
            divide(10, 0);
        } catch (ArithmeticException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```
**📝 Output:**  
```
Exception caught: Cannot divide by zero.
```

**🛠 Explanation:**  
- `throws` allows us to **propagate** exceptions to the caller.  
- The `try-catch` block in `main` handles the exception.

---

## **3️⃣ Custom Exceptions (User-Defined Exceptions)**  
Java allows us to create **custom exceptions** by extending the `Exception` class.

### **🔹 Creating a Custom Exception**
```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class CustomExceptionExample {
    static void checkAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be at least 18.");
        }
        System.out.println("Eligible to vote.");
    }

    public static void main(String[] args) {
        try {
            checkAge(15);  // This will trigger the custom exception
        } catch (InvalidAgeException e) {
            System.out.println("Custom Exception caught: " + e.getMessage());
        }
    }
}
```
**📝 Output:**  
```
Custom Exception caught: Age must be at least 18.
```

**🛠 Explanation:**  
- We **define a custom exception** (`InvalidAgeException`) by extending `Exception`.  
- The constructor calls `super(message)` to pass the error message to `Exception`.  
- In the `checkAge()` method, we throw the custom exception if the condition is met.  

---

## **💡 Key Takeaways**
| Concept | Explanation |
|---------|------------|
| **try-catch-finally** | Used to handle exceptions in Java. |
| **throw** | Manually throws an exception inside a method. |
| **throws** | Declares that a method might throw an exception. |
| **Custom Exceptions** | User-defined exceptions by extending `Exception` or `RuntimeException`. |
