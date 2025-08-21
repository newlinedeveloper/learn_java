# 🚀 Java 17 Key Features (with Examples)

### 1. **Sealed Classes (Java 15 → finalized in 17)**

* Restrict which classes can extend a class or implement an interface.
* Good for **controlled inheritance hierarchy**.

```java
sealed interface Vehicle permits Car, Bike {}

final class Car implements Vehicle {}
final class Bike implements Vehicle {}
// Any other class cannot implement Vehicle
```

👉 Interview Q: *Why sealed classes?*
✅ They help maintain **exhaustiveness** in `switch` and enforce **strong modeling** of domain types.

---

### 2. **Pattern Matching for `instanceof` (Java 16 → LTS in 17)**

* Eliminates explicit casting.

```java
Object obj = "Hello Java 17";
if (obj instanceof String s) {
    System.out.println(s.toUpperCase()); // No need for cast
}
```

👉 Interview Q: *Why pattern matching?*
✅ Reduces boilerplate, improves readability.

---

### 3. **Switch Expressions (Java 12 → LTS in 17)**

* `switch` is now an **expression**, can return values, and uses `->`.

```java
String day = "MON";
int numLetters = switch (day) {
    case "MON", "FRI", "SUN" -> 3;
    case "TUE" -> 4;
    case "THU", "SAT" -> 6;
    case "WED" -> 9;
    default -> throw new IllegalArgumentException("Invalid day");
};
System.out.println(numLetters);
```

👉 Interview Q: *What’s new in switch?*
✅ Concise syntax, prevents fall-through, usable as an expression.

---

### 4. **Records (Java 16 → LTS in 17)**

* Immutable data carrier classes with auto-generated `equals`, `hashCode`, `toString`.

```java
record Employee(String name, int age) {}

public class Main {
    public static void main(String[] args) {
        Employee e = new Employee("Alice", 30);
        System.out.println(e.name()); // getter-like method
        System.out.println(e); // auto toString
    }
}
```

👉 Interview Q: *When to use records?*
✅ For **DTOs, configs, value objects** — no boilerplate.

---

### 5. **Text Blocks (Java 15 → LTS in 17)**

* Multi-line strings with `"""`.

```java
String json = """
    {
      "name": "Alice",
      "age": 30
    }
    """;
System.out.println(json);
```

👉 Interview Q: *Why text blocks?*
✅ Cleaner for JSON, SQL, XML in code.

---

### 6. **Helpful NullPointerExceptions (Java 14 → LTS in 17)**

* Shows **which variable** was null, not just “NPE”.

```java
String str = null;
System.out.println(str.length()); 
// Before: NullPointerException
// Now: Cannot invoke "String.length()" because "str" is null
```

---

### 7. **JEP 411: Deprecation of Security Manager**

* Security Manager is now **deprecated** (rarely used, but good to know).

---

### 8. **JEP 356: Enhanced Pseudo-Random Number Generators**

* More flexible RNG with **pluggable algorithms**.

```java
import java.util.random.RandomGenerator;

public class RandomDemo {
    public static void main(String[] args) {
        RandomGenerator rng = RandomGenerator.of("Xoshiro256PlusPlus");
        System.out.println(rng.nextInt(100));
    }
}
```

---

### 9. **Foreign Function & Memory API (Preview in Java 17)**

* Alternative to JNI for native code interop (not stable, but mentionable).

---

### 10. **Removed / Deprecated Stuff**

* **RMI Activation System** removed.
* **Applets API** deprecated (no one uses them).

---

# 🎯 Likely Java 17 Interview Questions

1. What are **sealed classes**? Give an example.
2. How do **records** differ from normal classes? Can they extend another class? (❌ No, but can implement interfaces).
3. How is **switch expression** different from old `switch`?
4. How does **pattern matching in instanceof** reduce boilerplate?
5. What are **text blocks** and why useful?
6. What is new about **NullPointerExceptions** in Java 17?
7. Which major **APIs got deprecated/removed** in Java 17?

---

⚡ Quick Tip: In interview, when asked *“What’s new in Java 17?”* → say:
👉 *Java 17 introduced sealed classes, pattern matching, records, switch expressions, text blocks, better NPEs, new RNGs, and deprecated legacy features like Security Manager & Applets.*

---

