# **MySQL Basics - README**

## **1. Introduction to MySQL**
MySQL is a **Relational Database Management System (RDBMS)** used to store and manage structured data. It follows the SQL (Structured Query Language) standard and is widely used for web applications, data management, and enterprise solutions.

### **DBMS vs. RDBMS**
- **DBMS (Database Management System)**: A software system that manages databases but does not enforce relationships between tables.
- **RDBMS (Relational Database Management System)**: A database system that supports relationships between tables using constraints like **Primary Key** and **Foreign Key**.

---

## **2. Managing Tables**
### **Create Table**
#### Definition:
The `CREATE TABLE` statement is used to define a new table in MySQL, specifying its columns, data types, and constraints.
#### Query:
```sql
CREATE TABLE Employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    salary DECIMAL(10,2) DEFAULT 50000.00
);
```

### **Auto Increment**
#### Definition:
The `AUTO_INCREMENT` attribute automatically generates unique numeric values for a column.
#### Example:
```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(100)
);
```

### **Rename Table**
#### Definition:
The `RENAME TABLE` statement renames an existing table.
#### Query:
```sql
RENAME TABLE Employees TO Staff;
```

### **Add Column**
#### Definition:
The `ALTER TABLE` statement is used to add a new column to an existing table.
#### Query:
```sql
ALTER TABLE Employees ADD COLUMN department VARCHAR(50);
```

### **Drop Column**
#### Definition:
The `ALTER TABLE DROP COLUMN` statement removes a column from an existing table.
#### Query:
```sql
ALTER TABLE Employees DROP COLUMN department;
```

### **Drop Table**
#### Definition:
The `DROP TABLE` statement permanently deletes a table and all its data.
#### Query:
```sql
DROP TABLE Employees;
```

### **Temporary Tables**
#### Definition:
Temporary tables exist only for the duration of a session or transaction.
#### Query:
```sql
CREATE TEMPORARY TABLE TempEmployees (
    id INT, name VARCHAR(100)
);
```

### **Generated Columns**
#### Definition:
Generated columns automatically compute values based on other columns.
#### Query:
```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    price DECIMAL(10,2),
    tax DECIMAL(10,2) GENERATED ALWAYS AS (price * 0.1) STORED
);
```

---

## **3. MySQL Constraints**
### **Primary Key**
#### Definition:
A `PRIMARY KEY` uniquely identifies each record in a table.
#### Query:
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

### **Foreign Key**
#### Definition:
A `FOREIGN KEY` enforces a link between two tables to maintain referential integrity.
#### Query:
```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

### **Disable Foreign Key Checks**
#### Definition:
Disables foreign key constraints temporarily.
#### Query:
```sql
SET FOREIGN_KEY_CHECKS = 0;
```

### **Unique Constraint**
#### Definition:
Ensures all values in a column are unique.
#### Query:
```sql
ALTER TABLE Users ADD CONSTRAINT UNIQUE (name);
```

### **Not Null Constraint**
#### Definition:
Ensures a column cannot have NULL values.
#### Query:
```sql
ALTER TABLE Users MODIFY name VARCHAR(100) NOT NULL;
```

### **Default Constraint**
#### Definition:
Assigns a default value to a column when no value is specified.
#### Query:
```sql
ALTER TABLE Employees ALTER salary SET DEFAULT 60000.00;
```

### **Check Constraint**
#### Definition:
Restricts values in a column based on a condition.
#### Query:
```sql
CREATE TABLE Employees (
    id INT PRIMARY KEY,
    age INT CHECK (age >= 18)
);
```

---

## **4. Insert Data**
### **Insert Single Row**
#### Definition:
Adds a single row into a table.
#### Query:
```sql
INSERT INTO Employees (name, age, salary) VALUES ('John Doe', 30, 55000.00);
```

### **Insert Multiple Rows**
#### Definition:
Inserts multiple records at once.
#### Query:
```sql
INSERT INTO Employees (name, age, salary) VALUES
('Alice', 25, 50000.00),
('Bob', 35, 60000.00);
```

### **Insert Using Another Table (INSERT INTO SELECT)**
#### Definition:
Copies data from one table into another.
#### Query:
```sql
INSERT INTO Employees (name, age, salary)
SELECT name, age, salary FROM TempEmployees;
```

---

## **5. Update Data**
### **Basic Update**
#### Definition:
Modifies existing records in a table.
#### Query:
```sql
UPDATE Employees SET salary = 65000 WHERE id = 1;
```

### **Update with JOIN**
#### Definition:
Updates data in a table using values from another table.
#### Query:
```sql
UPDATE Employees
JOIN Departments ON Employees.department_id = Departments.id
SET Employees.salary = Employees.salary * 1.1
WHERE Departments.name = 'HR';
```

---

## **6. Delete Data**
### **Delete with Join**
#### Definition:
Deletes records by referencing another table.
#### Query:
```sql
DELETE Employees FROM Employees
JOIN Departments ON Employees.department_id = Departments.id
WHERE Departments.name = 'HR';
```

---

## **7. Transactions & Table Locking**
### **Transactions**
#### Definition:
Ensures atomicity, consistency, isolation, and durability (ACID) for database operations.
#### Query:
```sql
START TRANSACTION;
UPDATE Employees SET salary = salary + 5000 WHERE id = 1;
COMMIT;
```

### **Table Locking**
#### Definition:
Prevents concurrent modifications by locking a table during operations.
#### Query:
```sql
LOCK TABLES Employees WRITE;
UPDATE Employees SET salary = 75000 WHERE id = 1;
UNLOCK TABLES;
```



