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

---
