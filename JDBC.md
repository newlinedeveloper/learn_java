# **Database Connectivity (JDBC) in Java**  

JDBC (**Java Database Connectivity**) is an API that allows Java applications to interact with relational databases like **MySQL, PostgreSQL, Oracle, and SQL Server**. It provides methods for connecting to a database, executing SQL queries, and handling results.

---

# **1. Steps to Connect Java with MySQL/PostgreSQL**  
### ✅ Steps for Database Connectivity:  
1. Load the **JDBC Driver**.  
2. Establish a **connection** to the database.  
3. Create a **statement** (SQL query).  
4. Execute the **query** and process the results.  
5. Close the **resources**.

---

## **2. Connecting Java with MySQL**
👉 **First, add the MySQL JDBC driver to your project.**  
- **Maven Dependency for MySQL Driver**
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

- **JDBC URL for MySQL**
```java
String url = "jdbc:mysql://localhost:3306/mydatabase";
String user = "root";
String password = "password";
```

### **Example: Connecting to MySQL**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class MySQLConnection {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("Connected to MySQL successfully!");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Uses `DriverManager.getConnection(url, user, password)` to establish the connection.**  
✅ **Automatically closes the connection with `try-with-resources`.**

---

## **3. Connecting Java with PostgreSQL**
👉 **First, add the PostgreSQL JDBC driver to your project.**  
- **Maven Dependency for PostgreSQL Driver**
```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.5.0</version>
</dependency>
```

- **JDBC URL for PostgreSQL**
```java
String url = "jdbc:postgresql://localhost:5432/mydatabase";
String user = "postgres";
String password = "password";
```

### **Example: Connecting to PostgreSQL**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class PostgreSQLConnection {
    public static void main(String[] args) {
        String url = "jdbc:postgresql://localhost:5432/mydatabase";
        String user = "postgres";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("Connected to PostgreSQL successfully!");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Works the same way as MySQL, just with a different JDBC URL.**

---

# **4. Executing SQL Queries Using JDBC**  

## **4.1 Executing `SELECT` Queries**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class SelectQueryExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT id, name FROM users")) {

            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                System.out.println("ID: " + id + ", Name: " + name);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Uses `executeQuery()` to fetch results from the database.**  
✅ **Iterates through the `ResultSet` to process data.**  

---

## **4.2 Executing `INSERT`, `UPDATE`, and `DELETE` Queries**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateQueryExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {

            // Insert a new user
            String sqlInsert = "INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com')";
            stmt.executeUpdate(sqlInsert);
            System.out.println("User inserted successfully!");

            // Update user
            String sqlUpdate = "UPDATE users SET email='john.doe@example.com' WHERE name='John Doe'";
            stmt.executeUpdate(sqlUpdate);
            System.out.println("User updated successfully!");

            // Delete user
            String sqlDelete = "DELETE FROM users WHERE name='John Doe'";
            stmt.executeUpdate(sqlDelete);
            System.out.println("User deleted successfully!");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
✅ **Uses `executeUpdate()` to modify the database (INSERT, UPDATE, DELETE).**  
✅ **Returns the number of rows affected.**

---

# **5. Using ORM Frameworks (Hibernate)**
JDBC is great but requires **manual SQL handling**. **Hibernate** (an **ORM - Object-Relational Mapping** framework) helps manage database interactions more efficiently.

✅ **Advantages of Hibernate over JDBC**  
✔ Eliminates the need for writing SQL queries.  
✔ Maps Java objects directly to database tables.  
✔ Provides **Automatic Table Creation** (`@Entity`).  
✔ Supports **Caching** and **Lazy Loading**.  

---

## **5.1 Setting Up Hibernate with MySQL**
### **Step 1: Add Hibernate Dependencies (Maven)**
```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>6.2.0.Final</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

### **Step 2: Hibernate Configuration (`hibernate.cfg.xml`)**
```xml
<hibernate-configuration>
    <session-factory>
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/mydatabase</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password">password</property>
        <property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
        <property name="hibernate.hbm2ddl.auto">update</property>
        <property name="show_sql">true</property>
    </session-factory>
</hibernate-configuration>
```

---

### **Step 3: Define Entity Class**
```java
import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;
    
    @Column(name = "name")
    private String name;
    
    @Column(name = "email")
    private String email;

    // Constructors, Getters & Setters
}
```

---

### **Step 4: Perform Database Operations Using Hibernate**
```java
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class HibernateExample {
    public static void main(String[] args) {
        SessionFactory factory = new Configuration().configure().buildSessionFactory();
        Session session = factory.openSession();
        Transaction tx = session.beginTransaction();

        User user = new User();
        user.setName("Alice");
        user.setEmail("alice@example.com");

        session.save(user);
        tx.commit();
        session.close();

        System.out.println("User saved successfully!");
    }
}
```
✅ **No need to write SQL queries!**  
✅ **Manages database connection automatically.**  

---
