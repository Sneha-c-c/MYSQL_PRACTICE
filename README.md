# MYSQL 
## 📌 DBMS (Database Management System)

A **DBMS** is software that allows us to store, organize, and manage data in a structured way.  

**Example:** A phonebook where you can insert, search, update, and delete contacts.  

### 🔑 Key Features
- Provides data storage.
- Ensures data security.
- Handles multiple users.
- Supports queries.

---

## 📌 RDBMS (Relational Database Management System)

An **RDBMS** is a special type of DBMS that organizes data into **tables (rows & columns)** and allows **relationships between tables**.  
It is based on **E. F. Codd’s relational model**.

### 🔑 Key Features
- Stores data in **tables (relations)**.
- Each row = **record (tuple)**.  
- Each column = **attribute (field)**.  
- Supports **SQL (Structured Query Language)**.  
- Enforces **keys (Primary Key, Foreign Key)**.  
- Ensures **data integrity**.

---

## 📌 MySQL – Definition

**MySQL** is an open-source **Relational Database Management System (RDBMS)**.  
It uses **SQL** to store, manage, and retrieve data.  

### 💡 Why is MySQL used?
- To **store and manage structured data**.  
- To handle **transactions reliably** (ACID compliance with InnoDB).  
- To provide **fast query performance**.  
- To support **multiple users concurrently**.  

---

## 📌 ACID Properties in DBMS

ACID stands for:  
- **A → Atomicity**  
- **C → Consistency**  
- **I → Isolation**  
- **D → Durability**

### 1️⃣ Atomicity – *"All or Nothing"*
- A transaction is treated as one unit:  
  - Either all steps succeed, or none are applied.  
- If any step fails → everything is rolled back.  

**Example:**  
Transfer ₹1000 from Account A → B  
- Step 1: Deduct ₹1000 from A  
- Step 2: Add ₹1000 to B  
- If Step 2 fails, Step 1 is undone.  

👉 In MySQL: Handled using **ROLLBACK** on failure.  

---

### 2️⃣ Consistency – *"Valid State → Valid State"*
- Database must move from one **valid state** to another.  
- Constraints & rules must always be followed.  

**Example:**  
If `balance >= 0`, withdrawal cannot leave balance at -500.  

👉 In MySQL: Handled with **NOT NULL, CHECK, FOREIGN KEY** constraints.  

---

### 3️⃣ Isolation – *"No Interference"*
- Multiple transactions don’t affect each other.  

**Example:**  
Two people booking the **last movie ticket**:  
- Only one succeeds, the other fails gracefully.  

👉 In MySQL: Controlled using **Transaction Isolation Levels** (`READ COMMITTED`, `SERIALIZABLE`, etc.).  

---

### 4️⃣ Durability – *"Once Saved, Always Saved"*
- Once committed, changes are **permanent**.  
- Data remains even after crash or power failure.  

**Example:**  
If transfer is successful, money stays updated.  

👉 In MySQL: Handled by **logs & commit records (COMMIT)**.  

---

## 📌 Table – Definition

- A **table** is the basic unit of storage in an RDBMS.  
- Stores data in **rows (records)** and **columns (attributes)**.  

---

## 📌 Primary Key

- A **Primary Key** uniquely identifies each row in a table.  
- Rules:
  - Must be **unique**.  
  - Cannot be **NULL**.  

---

## 📌 Foreign Key

- A **Foreign Key** links one table to another.  
- It refers to the **Primary Key** in another table.  
- Ensures **referential integrity** (no invalid references).  

---

## 👥 MySQL User Management  

### ➤ Create a User  

```sql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost';
FLUSH PRIVILEGES;

-- Login
mysql -u username -p
```

---

# 🏗️ MySQL Basics – Database, Tables & Queries  

## 1️⃣ Create & Use a Database  

```sql
CREATE DATABASE academy;
USE academy;
```

---

## 2️⃣ Create Your First Table  

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);
```

- **student_id** → auto-incremented, unique ID.  
- **name** → required.  
- **age** → optional.  
- **email** → must be unique.  

---

## 3️⃣ Insert Data  

```sql
INSERT INTO students (name, age, email)
VALUES 
  ('Sneha', 23, 'sneha@example.com'),
  ('Rahul', 25, 'rahul@example.com'),
  ('Ananya', 22, 'ananya@example.com');
```

---

## 4️⃣ Query Data  

```sql
SELECT * FROM students;
```

---

## 5️⃣ Update & Delete  

Update Sneha’s age:  

```sql
UPDATE students
SET age = 24
WHERE name = 'Sneha';
```

Delete Rahul’s record:  

```sql
DELETE FROM students
WHERE name = 'Rahul';
```

---

## 🔢 Common MySQL Data Types  

### Numbers  
- **INT** → whole numbers (±2 billion).  
- **BIGINT** → very large numbers (e.g., IDs).  
- **DECIMAL(p,s)** → precise numbers (e.g., `DECIMAL(10,2)`).  

### Strings  
- **CHAR(n)** → fixed length (e.g., country code `'IN'`).  
- **VARCHAR(n)** → variable length (best for names, emails).  
- **TEXT** → long text.  

### Dates & Times  
- **DATE** → `2025-09-04`.  
- **DATETIME** → `2025-09-04 11:30:00`.  
- **TIMESTAMP** → timezone-aware, smaller range.  

### Booleans  
- **BOOLEAN** → stored as `TINYINT(1)` (`0 = false`, `1 = true`).  

## 🔹 1. Numeric Data Types

| Type         | Storage    | Range (Signed)                          | Example Usage             |
|--------------|------------|------------------------------------------|---------------------------|
| `TINYINT`    | 1 byte     | -128 to 127                             | Flags, Boolean values     |
| `SMALLINT`   | 2 bytes    | -32,768 to 32,767                       | Small counters            |
| `MEDIUMINT`  | 3 bytes    | -8,388,608 to 8,388,607                 | Medium-sized counters     |
| `INT`        | 4 bytes    | -2,147,483,648 to 2,147,483,647         | IDs, age, counts          |
| `BIGINT`     | 8 bytes    | ~±9.22e18                               | Large IDs, financial data |
| `DECIMAL(M,D)` | Varies   | Exact fixed-point numbers               | Money, accounting         |
| `FLOAT`      | 4 bytes    | Approximate floating point              | Sensor data, scientific   |
| `DOUBLE`     | 8 bytes    | Higher precision floating point         | Scientific data           |

💡 **Tip:** Use `DECIMAL` for financial calculations to avoid rounding errors.

---

## 🔹 2. String Data Types

| Type       | Description                         | Example Usage            |
|------------|-------------------------------------|--------------------------|
| `CHAR(n)`  | Fixed-length string (0–255 chars)   | Country codes (`US`, `IN`) |
| `VARCHAR(n)` | Variable-length string (0–65535) | Names, emails            |
| `TEXT`     | Large text (up to 65,535 chars)     | Blog posts, descriptions |
| `BLOB`     | Binary data (up to 65,535 bytes)    | Images, files            |

### Variants
- `TINYTEXT`, `TEXT`, `MEDIUMTEXT`, `LONGTEXT` (increasing storage size).
- `TINYBLOB`, `BLOB`, `MEDIUMBLOB`, `LONGBLOB`.

---

## 🔹 3. Date and Time Data Types

| Type        | Format              | Example              | Usage                  |
|-------------|---------------------|----------------------|------------------------|
| `DATE`      | `YYYY-MM-DD`        | `2025-09-08`         | Birthdays              |
| `DATETIME`  | `YYYY-MM-DD HH:MM:SS` | `2025-09-08 12:30:45` | Orders, events         |
| `TIMESTAMP` | UTC `YYYY-MM-DD HH:MM:SS` | Auto-updates | Audit trails           |
| `TIME`      | `HH:MM:SS`          | `14:35:00`           | Duration, shifts       |
| `YEAR`      | `YYYY`              | `2025`               | Year-only fields       |

💡 **Tip:** Use `TIMESTAMP` for “last modified” fields (auto-update feature).

---

## 🔹 4. Boolean Data Type

- `BOOLEAN` / `BOOL` is stored as `TINYINT(1)` internally.
- `0 = FALSE`, `1 = TRUE`.

```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  is_active BOOLEAN
);

---

## 🔹 ENUM

- **Definition:** Stores a single value from a predefined list.  
- **Use case:** When a column should only accept **one value** from a fixed set.  

**Example:**

```sql
status ENUM('active', 'inactive', 'banned')

---

# 📘 MySQL SET Data Type

The **SET** data type in MySQL allows a column to store **multiple values** from a predefined list.  

---

## 🔹 Definition
- Stores **zero or more values** chosen from a fixed set of options.
- Useful for features, tags, or multiple attributes that a single row can have.

---

## 🔹 Example

```sql
CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    features SET('Eco-Friendly', 'Durable', 'Waterproof')
);


# 📘 SQL Categories & CRUD in MySQL

This document explains the four major **SQL categories**—DDL, DML, DCL, TCL—and the CRUD operations (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) with MySQL-focused examples, tips, and interview insights.

---

## 🔹 SQL Categories Overview

| Category | Full Form                  | Purpose                                   | Examples                          |
|----------|----------------------------|-------------------------------------------|-----------------------------------|
| DDL      | Data Definition Language   | Defines database structure                | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| DML      | Data Manipulation Language | Works with data inside tables             | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| DCL      | Data Control Language      | Manages user access and permissions       | `GRANT`, `REVOKE`, `CREATE USER`       |
| TCL      | Transaction Control Language | Controls transactions & consistency    | `COMMIT`, `ROLLBACK`, `SAVEPOINT`      |

---

## 1) DDL — Data Definition Language
Defines and changes **database structure**.

### Common Commands
- `CREATE` — Make new databases, tables, indexes
- `ALTER` — Modify schema
- `DROP` — Remove databases or tables
- `TRUNCATE` — Empty a table (keeps structure)

### Example
```sql
CREATE DATABASE library;
USE library;

CREATE TABLE authors (
  author_id BIGINT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(200) NOT NULL,
  country VARCHAR(80)
) ENGINE=InnoDB;

ALTER TABLE authors ADD INDEX idx_country (country);
TRUNCATE TABLE authors;
DROP TABLE authors;

