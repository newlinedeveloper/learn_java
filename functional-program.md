# **Functional Programming in Java**  

Functional programming in Java was introduced in **Java 8** with the help of **Lambda Expressions**, **Streams API**, and **Functional Interfaces**. These features allow Java to better handle tasks that involve processing data in a functional style, making the code cleaner, more concise, and easier to maintain.

---

## **1. Lambda Expressions**
Lambda expressions allow you to express instances of single-method interfaces (functional interfaces) in a more concise way.

### **1.1 Syntax of Lambda Expressions**
```java
(parameters) -> expression
```

- **Without Parameters**:  
```java
() -> System.out.println("Hello, World!");
```

- **With Parameters**:  
```java
(a, b) -> a + b
```

- **With a Block of Code**:  
```java
(a, b) -> {
    int sum = a + b;
    return sum;
}
```

### **1.2 Example of Lambda Expression**
Let's say we want to filter a list of numbers that are greater than 10 and print them.

```java
import java.util.Arrays;
import java.util.List;

public class LambdaExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 5, 12, 15, 22, 8);

        // Using Lambda Expression
        numbers.forEach(n -> {
            if (n > 10) {
                System.out.println(n);
            }
        });
    }
}
```
🔹 **Advantages of Lambda Expressions**:  
- Compact and concise syntax.  
- Improves readability of the code.  
- Can be used primarily to define behavior in functional interfaces.

---

## **2. Streams API**
Streams API provides a high-level abstraction for processing sequences of elements, such as collections, arrays, or I/O resources, in a functional way.

### **2.1 Basic Example of Streams**
The `Stream` class supports functional-style operations like **map**, **filter**, **reduce**, etc.

```java
import java.util.Arrays;
import java.util.List;

public class StreamsExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);

        // Example of using Stream to filter and print
        numbers.stream()
               .filter(n -> n % 2 == 0)   // Filter even numbers
               .forEach(System.out::println);  // Print each even number
    }
}
```

### **2.2 Common Stream Operations**
- **`filter()`**: Filters elements based on a condition.
- **`map()`**: Transforms each element.
- **`reduce()`**: Reduces the elements to a single value.
- **`forEach()`**: Iterates over the elements.
- **`collect()`**: Collects the results back into a collection.
- **`sorted()`**: Sorts the elements.

### **2.3 Example: Using `map()` and `reduce()`**
```java
import java.util.Arrays;
import java.util.List;

public class StreamOperations {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Using map to square numbers and reduce to sum them
        int sumOfSquares = numbers.stream()
                                   .map(n -> n * n)  // Square each number
                                   .reduce(0, (a, b) -> a + b);  // Sum all the squared numbers

        System.out.println("Sum of squares: " + sumOfSquares);
    }
}
```

🔹 **Advantages of Streams**:  
- More declarative style.  
- Supports **lazy evaluation**, only performing actions when needed.
- Easily parallelizable using `parallelStream()` for concurrent processing.

---

## **3. Functional Interfaces**
Functional interfaces are interfaces that have **exactly one abstract method**. They can be implemented using **lambda expressions** or method references.

### **3.1 Common Functional Interfaces**
- **`Predicate<T>`**: Tests a condition and returns a `boolean`.
- **`Consumer<T>`**: Accepts a single input and returns no result (void).
- **`Supplier<T>`**: Supplies a result of type `T`.
- **`Function<T, R>`**: Applies a function to an argument of type `T` and returns a result of type `R`.

#### **3.2 Predicate Interface**
A `Predicate` tests whether a condition is true or false.

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = n -> n % 2 == 0;  // Predicate to check if even
        System.out.println(isEven.test(4));  // true
        System.out.println(isEven.test(5));  // false
    }
}
```

#### **3.3 Consumer Interface**
A `Consumer` performs an operation on an object, without returning any result.

```java
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        Consumer<String> printMessage = message -> System.out.println(message);
        printMessage.accept("Hello, World!");
    }
}
```

#### **3.4 Supplier Interface**
A `Supplier` generates or supplies a value when called.

```java
import java.util.function.Supplier;

public class SupplierExample {
    public static void main(String[] args) {
        Supplier<Double> randomValue = () -> Math.random();  // Supplier to generate a random number
        System.out.println(randomValue.get());  // Prints a random value
    }
}
```

### **3.5 Chaining Predicates, Consumers, and Functions**
- **`and()`, `or()`, `negate()` methods** for predicates.
- **`andThen()`, `compose()` methods** for functions.

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        Function<Integer, Integer> multiplyBy2 = n -> n * 2;
        Function<Integer, Integer> add5 = n -> n + 5;
        
        // Chain functions
        System.out.println(multiplyBy2.andThen(add5).apply(3));  // (3 * 2) + 5 = 11
        System.out.println(multiplyBy2.compose(add5).apply(3));  // (3 + 5) * 2 = 16
    }
}
```

---

## **Summary Table**
| **Interface**    | **Purpose**                               | **Method Signature**                          |
|------------------|-------------------------------------------|-----------------------------------------------|
| `Predicate<T>`    | Tests a condition (returns boolean)       | `boolean test(T t)`                           |
| `Consumer<T>`     | Performs an operation without returning a result | `void accept(T t)`                          |
| `Supplier<T>`     | Provides a value                          | `T get()`                                     |
| `Function<T, R>`  | Maps one value to another                 | `R apply(T t)`                                |

---

## **Benefits of Functional Programming in Java**
- **Immutability**: Functional programming promotes the use of immutable objects.
- **Conciseness**: Lambda expressions and functional interfaces provide more concise code.
- **Parallelism**: Streams allow easy parallelization of operations.
- **Higher-order functions**: Functions can accept or return other functions.

---

## **Best Practices**  
- Prefer **`Runnable` or `Callable`** when working with threads in a functional style.  
- Always use **`Streams`** for collection processing to make your code more declarative and cleaner.  
- Chain your **functional interfaces** properly to write more concise and readable code.
