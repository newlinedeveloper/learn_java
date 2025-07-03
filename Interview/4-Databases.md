## 🔹 Databases (PostgreSQL & MongoDB)

---

### ✅ **SQL (PostgreSQL)**

### 1. **How do you optimize SQL queries?**

**Key optimization techniques:**

* Use **indexes** on columns used in `WHERE`, `JOIN`, or `ORDER BY`.
* Avoid `SELECT *`; fetch only required columns.
* Use **EXPLAIN ANALYZE** to inspect query execution plans.
* Avoid **N+1 queries** (fetch related data with joins).
* Use **LIMIT**, **OFFSET** wisely for pagination.
* Use **connection pooling** for high-concurrency systems.

**Example:**

```sql
EXPLAIN ANALYZE 
SELECT name FROM employees WHERE department_id = 10;
```

---

### 2. **Difference between `INNER JOIN`, `LEFT JOIN`, and `FULL JOIN`**

| Join Type | Description                                                             | Example Output (if no match)    |
| --------- | ----------------------------------------------------------------------- | ------------------------------- |
| `INNER`   | Returns only matching rows from both tables                             | Row excluded if no match        |
| `LEFT`    | All rows from the left + matched rows from the right (null if no match) | NULLs on right if no match      |
| `FULL`    | All rows from both sides, with NULLs where no match exists              | NULLs on both sides if no match |

**Example:**

```sql
-- INNER JOIN
SELECT e.name, d.name 
FROM employees e 
INNER JOIN departments d ON e.dept_id = d.id;

-- LEFT JOIN
SELECT e.name, d.name 
FROM employees e 
LEFT JOIN departments d ON e.dept_id = d.id;

-- FULL JOIN
SELECT e.name, d.name 
FROM employees e 
FULL JOIN departments d ON e.dept_id = d.id;
```

---

### 3. **What are indexes and when should you use them?**

**Answer:**

* Indexes improve query performance by allowing faster lookup of rows.
* PostgreSQL supports **B-tree, Hash, GIN, GiST** indexes.
* Use on columns used frequently in:

  * `WHERE`, `JOIN`, `ORDER BY`, `GROUP BY`.

**Example:**

```sql
CREATE INDEX idx_employee_email ON employees(email);
```

⚠️ Don’t overuse indexes — they slow down `INSERT`, `UPDATE` operations and increase storage.

---

## ✅ **NoSQL (MongoDB)**

### 4. **How does MongoDB store data?**

* MongoDB stores data in **BSON** format (Binary JSON).
* Each record is called a **document**.
* Documents are grouped into **collections**, which are similar to tables.

**Example document:**

```json
{
  "_id": ObjectId("..."),
  "name": "Alice",
  "role": "Engineer",
  "skills": ["Java", "Spring Boot"]
}
```

Stored in a `users` collection, this is analogous to a row in SQL.

---

### 5. **How do you model one-to-many relationships in MongoDB?**

You have **two main approaches**:

#### a) **Embedded Documents** (when data is tightly coupled & small)

```json
{
  "name": "John",
  "orders": [
    { "id": 1, "item": "Laptop" },
    { "id": 2, "item": "Mouse" }
  ]
}
```

#### b) **Referencing** (when data grows independently)

```json
// User Document
{
  "_id": ObjectId("user123"),
  "name": "John"
}

// Order Document
{
  "_id": ObjectId("order456"),
  "user_id": ObjectId("user123"),
  "item": "Laptop"
}
```

You'd join via `user_id` in your application logic (MongoDB doesn't support joins natively like SQL, but aggregation can help).

---

