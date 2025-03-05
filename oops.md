# **OOP Concepts in Depth (Java)**  
Object-Oriented Programming (OOP) in Java is based on **four pillars**:  
1. **Encapsulation**  
2. **Inheritance**  
3. **Polymorphism**  
4. **Abstraction**  

---

## **1. Inheritance and Method Overriding**
### **What is Inheritance?**
Inheritance allows a class (**child class**) to acquire the properties and behaviors of another class (**parent class**).  
- Promotes **code reusability**.  
- Establishes a **hierarchical relationship** between classes.  

### **Types of Inheritance in Java**
| Type | Description |
|------|------------|
| **Single Inheritance** | One child inherits from one parent |
| **Multilevel Inheritance** | A class inherits from another class, which itself inherits from another |
| **Hierarchical Inheritance** | Multiple classes inherit from a single parent class |
| **Multiple Inheritance (via Interface)** | Java **does not** support multiple class inheritance, but it allows multiple interfaces |

#### **Example: Single Inheritance**
```java
class Animal {  
    void eat() { System.out.println("Eating..."); }  
}

class Dog extends Animal {  
    void bark() { System.out.println("Barking..."); }  
}

public class InheritanceExample {  
    public static void main(String args[]) {  
        Dog d = new Dog();  
        d.eat();  // Parent method
        d.bark(); // Child method
    }  
}
```
**Output:**  
```
Eating...
Barking...
```

---

## **2. Method Overriding**
Method Overriding allows a child class to **modify the behavior** of an inherited method.

### **Rules for Overriding:**
1. **Method name, return type, and parameters must be the same**.  
2. **Access modifier should be the same or more accessible**.  
3. **Cannot override `final` methods**.  
4. **Cannot override static methods** (Static methods belong to the class, not an instance).  

### **Example: Method Overriding**
```java
class Parent {
    void show() {
        System.out.println("Parent class method");
    }
}

class Child extends Parent {
    @Override
    void show() {
        System.out.println("Child class method");
    }
}

public class OverrideExample {
    public static void main(String[] args) {
        Parent obj = new Child();  // Dynamic method dispatch
        obj.show();
    }
}
```
**Output:**  
```
Child class method
```

---

## **3. `super` Keyword**
- Used to refer to the **parent class constructor/method**.  
- Helps in **accessing overridden methods**.  
- Must be the **first statement** inside a constructor.

### **Example: Using `super` to Call Parent Method**
```java
class Parent {
    void display() {
        System.out.println("Parent display");
    }
}

class Child extends Parent {
    void display() {
        super.display();  // Calls Parent's display()
        System.out.println("Child display");
    }
}

public class SuperExample {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.display();
    }
}
```
**Output:**  
```
Parent display
Child display
```

### **Example: Using `super` for Parent Constructor**
```java
class Animal {
    Animal() {
        System.out.println("Animal Constructor");
    }
}

class Dog extends Animal {
    Dog() {
        super();  // Calls Animal constructor
        System.out.println("Dog Constructor");
    }
}

public class SuperConstructorExample {
    public static void main(String[] args) {
        Dog d = new Dog();
    }
}
```
**Output:**  
```
Animal Constructor
Dog Constructor
```

---

## **4. Polymorphism**
Polymorphism means **"many forms"**. It allows a single interface to represent different behaviors.

### **Types of Polymorphism**
1. **Compile-time (Method Overloading)**  
2. **Runtime (Method Overriding - Dynamic Binding)**  

### **Method Overloading (Compile-time Polymorphism)**
- Same method name, different parameters.
```java
class MathOperations {
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
}

public class OverloadingExample {
    public static void main(String[] args) {
        MathOperations obj = new MathOperations();
        System.out.println(obj.add(5, 10));    // Calls int method
        System.out.println(obj.add(5.5, 2.5)); // Calls double method
    }
}
```

### **Method Overriding (Runtime Polymorphism)**
Occurs when a child class **redefines** a method from its parent class.

```java
class Parent {
    void show() {
        System.out.println("Parent Show");
    }
}

class Child extends Parent {
    void show() {
        System.out.println("Child Show");
    }
}

public class OverridingExample {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.show();  // Calls child's version
    }
}
```

---

## **5. Abstract Classes & Interfaces**
### **Abstract Class**
- **Cannot be instantiated**.  
- May have **both abstract and concrete methods**.  
- Used for **partial implementation**.

```java
abstract class Animal {
    abstract void makeSound();  // Abstract method
    void sleep() {
        System.out.println("Sleeping...");
    }
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark");
    }
}

public class AbstractExample {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound();
        myDog.sleep();
    }
}
```

---

### **Interfaces (Pure Abstraction)**
- **100% abstraction** (before Java 8).  
- All methods are **abstract by default**.  
- **No constructors** in interfaces.

```java
interface Animal {
    void makeSound();  // By default, abstract
}

class Dog implements Animal {
    public void makeSound() {
        System.out.println("Bark");
    }
}

public class InterfaceExample {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound();
    }
}
```

---

## **6. Composition and Aggregation**
Both are ways to **model relationships** between objects.

### **Composition (Strong Association)**
- **"Has-a" relationship**  
- **Dependent relationship** (If the parent is destroyed, the child also gets destroyed).

```java
class Engine {
    void start() {
        System.out.println("Engine Started");
    }
}

class Car {
    private Engine engine = new Engine();  // Composition

    void start() {
        engine.start();
        System.out.println("Car Started");
    }
}

public class CompositionExample {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start();
    }
}
```
**Output:**
```
Engine Started
Car Started
```

---

### **Aggregation (Weak Association)**
- Objects can exist **independently**.

```java
class Address {
    String city;

    Address(String city) {
        this.city = city;
    }
}

class Employee {
    String name;
    Address address;  // Aggregation

    Employee(String name, Address address) {
        this.name = name;
        this.address = address;
    }
}

public class AggregationExample {
    public static void main(String[] args) {
        Address addr = new Address("New York");
        Employee emp = new Employee("John", addr);
        System.out.println(emp.name + " lives in " + emp.address.city);
    }
}
```
---
### **Final Thoughts**
- **Inheritance** → Code reuse.  
- **Polymorphism** → Flexibility & method overriding.  
- **Abstract Classes & Interfaces** → Abstraction & blueprint for classes.  
- **Composition & Aggregation** → Object relationships.
