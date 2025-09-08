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

## 📌 MySQL User Management

### ➤ Create a User
```sql
-CREATE USER 'username'@'host' IDENTIFIED BY 'password'; // Create a user with password where host is where database is accesses from  usually localhost / % - accesses from anywhere
-GRANT ALL PRIVILAGES ON '.' TO 'username'@'localhost'
-FLUSH PRIVILAGES;// Refresh the page
-mysql -u username -p

# 📚 MySQL Basics – Database, Tables, Queries & Data Types

This guide walks through creating a database, adding tables, inserting data, running queries, and understanding MySQL data types.

---

## 🛠 Step 1: Create & Use a Database
```sql
CREATE DATABASE academy;
USE academy;

-CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);

# 📘 MySQL Basics – Creating Database, Tables, and Using Data Types

## 🔹 Step 1: Create & Use a Database
```sql
CREATE DATABASE academy;
USE academy;

Create Your First Table

We’ll make a simple students table.

CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);

# MySQL Basics: First Schema, Table & Data

This guide walks you through creating a database, building a table, inserting data, querying it, and performing updates/deletes in MySQL.

---

## Step 1: Create & Use a Database

```sql
CREATE DATABASE academy;
USE academy;
```

## Step 2: Create Your First Table

We’ll make a simple `students` table.

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);
```

- **student_id** → unique ID, auto-incremented.  
- **name** → required (`NOT NULL`).  
- **email** → must be unique.  
- **age** → optional.  

---

## Step 3: Insert Some Data

```sql
INSERT INTO students (name, age, email)
VALUES 
  ('Sneha', 23, 'sneha@example.com'),
  ('Rahul', 25, 'rahul@example.com'),
  ('Ananya', 22, 'ananya@example.com');
```

---

## Step 4: Query the Data

```sql
SELECT * FROM students;
```

---

## Step 5: Update & Delete

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

Check remaining data:

```sql
SELECT * FROM students;
```

---

## Common MySQL Data Types

### Numbers
- **INT** – whole numbers (±2 billion).  
  *Example:* `age INT`  
- **BIGINT** – very large whole numbers (e.g., bank account IDs).  
- **DECIMAL(p,s)** – precise numbers (like money).  
  *Example:* `salary DECIMAL(10,2)` → max 99999999.99  

### Strings
- **CHAR(n)** – fixed length. Good for short, uniform data (e.g., `'IN'`).  
- **VARCHAR(n)** – variable length, max n. Best for names, emails, etc.  
- **TEXT** – long text (articles, descriptions).  

### Dates & Times
- **DATE** – just year-month-day (e.g., `2025-09-04`).  
- **DATETIME** – date + time (e.g., `2025-09-04 11:30:00`).  
- **TIMESTAMP** – like `DATETIME`, but timezone-aware and smaller range. Often used for created/updated times.  

### Booleans
- **BOOLEAN** → actually stored as `TINYINT(1)` (`0 = false`, `1 = true`).  

---

## Summary
This example demonstrates how to:
1. Create and use a database.  
2. Define a table with constraints.  
3. Insert, query, update, and delete records.  
4. Understand common MySQL data types.  

