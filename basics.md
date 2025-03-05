## **Java basics**

### **1. Introduction to Java**
#### **What is Java? Why use it?**
Java is a high-level, object-oriented programming language developed by Sun Microsystems (now owned by Oracle). It is platform-independent, secure, and widely used in web, mobile, and enterprise applications.

#### **Installing Java**
To run Java, you need:
- **JDK (Java Development Kit)** – For developing applications
- **JRE (Java Runtime Environment)** – To run Java applications

You can download the latest JDK from [Oracle's official site](https://www.oracle.com/java/technologies/javase-downloads.html).

#### **Setting up an IDE**
Common IDEs:
- IntelliJ IDEA
- VS Code (with Java extensions)
- Eclipse

#### **Writing and Running Your First Java Program**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
- Save the file as `HelloWorld.java`
- Compile: `javac HelloWorld.java`
- Run: `java HelloWorld`

---

### **2. Java Basics**
#### **Variables and Data Types**
```java
public class VariablesExample {
    public static void main(String[] args) {
        int age = 25;
        double price = 99.99;
        char grade = 'A';
        boolean isJavaFun = true;

        System.out.println("Age: " + age);
        System.out.println("Price: " + price);
        System.out.println("Grade: " + grade);
        System.out.println("Is Java fun? " + isJavaFun);
    }
}
```

#### **Operators**
```java
public class OperatorsExample {
    public static void main(String[] args) {
        int a = 10, b = 5;

        // Arithmetic
        System.out.println("Addition: " + (a + b));

        // Logical
        System.out.println("Logical AND: " + (a > 5 && b < 10));

        // Relational
        System.out.println("Is A greater than B? " + (a > b));
    }
}
```

#### **Control Statements**
```java
public class ControlStatements {
    public static void main(String[] args) {
        int num = 10;
        if (num > 0) {
            System.out.println("Positive number");
        } else {
            System.out.println("Negative number");
        }

        // Switch-case
        char grade = 'A';
        switch (grade) {
            case 'A':
                System.out.println("Excellent!");
                break;
            default:
                System.out.println("Good job");
        }
    }
}
```

#### **Loops**
```java
public class LoopsExample {
    public static void main(String[] args) {
        // For loop
        for (int i = 1; i <= 5; i++) {
            System.out.println("For Loop: " + i);
        }

        // While loop
        int j = 1;
        while (j <= 5) {
            System.out.println("While Loop: " + j);
            j++;
        }
    }
}
```

---

### **3. Functions & Methods**
```java
public class MethodsExample {
    // Method with parameters and return type
    public static int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        int sum = add(5, 10);
        System.out.println("Sum: " + sum);
    }
}
```

#### **Recursion**
```java
public class RecursionExample {
    public static int factorial(int n) {
        if (n == 0) return 1;
        return n * factorial(n - 1);
    }

    public static void main(String[] args) {
        System.out.println("Factorial of 5: " + factorial(5));
    }
}
```

---

### **4. Object-Oriented Programming (OOP)**
```java
class Car {
    String brand;
    int speed;

    // Constructor
    public Car(String brand, int speed) {
        this.brand = brand;
        this.speed = speed;
    }

    void display() {
        System.out.println("Car Brand: " + brand + ", Speed: " + speed);
    }
}

public class OOPExample {
    public static void main(String[] args) {
        Car car = new Car("Toyota", 120);
        car.display();
    }
}
```

---

## **Intermediate Level**

### **5. OOP Concepts in Depth**
#### **Inheritance**
```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

public class InheritanceExample {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
        dog.bark();
    }
}
```

#### **Polymorphism**
```java
class Animal {
    void sound() {
        System.out.println("Animals make sounds");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Animal myCat = new Cat();
        myCat.sound();
    }
}
```

---

### **6. Exception Handling**
```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int divideByZero = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero!");
        }
    }
}
```

---

### **7. Collections Framework**
```java
import java.util.*;

public class CollectionsExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");

        System.out.println("List: " + list);
    }
}
```

---

### **8. Multithreading**
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}

public class MultithreadingExample {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();
    }
}
```

---

## **Advanced Level**

### **9. Functional Programming**
```java
import java.util.function.Predicate;

public class FunctionalExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = num -> num % 2 == 0;
        System.out.println("Is 10 even? " + isEven.test(10));
    }
}
```

---

### **10. Java I/O and File Handling**
```java
import java.io.*;

public class FileHandlingExample {
    public static void main(String[] args) {
        try {
            FileWriter writer = new FileWriter("test.txt");
            writer.write("Hello, Java!");
            writer.close();

            BufferedReader reader = new BufferedReader(new FileReader("test.txt"));
            System.out.println("File Content: " + reader.readLine());
            reader.close();
        } catch (IOException e) {
            System.out.println("An error occurred.");
        }
    }
}
```

---
