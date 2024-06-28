# SQL Cheat Sheet

This repository provides a comprehensive cheat sheet for SQL queries. It includes examples of basic and advanced SQL queries to help you quickly reference and use SQL in your projects.

## Contents

- [Basic Queries](#basic-queries)
  - [Create Tables](#create-tables)
  - [Insert Data](#insert-data)
  - [Update Data](#update-data)
  - [Delete Data](#delete-data)
  - [Select Queries](#select-queries)
  - [Join Queries](#join-queries)
- [Advanced Queries](#advanced-queries)
  - [Subqueries](#subqueries)
  - [Aggregate Functions](#aggregate-functions)
  - [Window Functions](#window-functions)
  - [Common Table Expressions](#common-table-expressions)
  - [Indexes](#indexes)

## Basic Queries

### Create Tables
```sql
-- Create a sample table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100) UNIQUE,
    HireDate DATE,
    Salary DECIMAL(10, 2)
);
```

### Insert Data
```sql
-- Insert data into Employees table
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, HireDate, Salary)
VALUES (1, 'John', 'Doe', 'john.doe@example.com', '2022-01-15', 60000);
```

### Update Data
```sql
-- Update an employee's salary
UPDATE Employees
SET Salary = 65000
WHERE EmployeeID = 1;
```

### Delete Data
```sql
-- Delete an employee record
DELETE FROM Employees
WHERE EmployeeID = 1;
```

### Select Queries
```sql
-- Select all employees
SELECT * FROM Employees;

-- Select specific columns
SELECT FirstName, LastName FROM Employees;

-- Select with WHERE clause
SELECT * FROM Employees WHERE Salary > 50000;

-- Order by Salary descending
SELECT * FROM Employees ORDER BY Salary DESC;
```

### Join Queries
```sql
-- Join Employees with Departments
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Left Join Employees with Departments
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Right Join Employees with Departments
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
RIGHT JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Full Outer Join Employees with Departments
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
FULL OUTER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Self Join: Find employees who have the same manager
SELECT e1.FirstName AS Employee, e2.FirstName AS Manager
FROM Employees e1
JOIN Employees e2 ON e1.ManagerID = e2.EmployeeID;

-- Cross Join Employees with Departments
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
CROSS JOIN Departments d;

-- Join with multiple tables: Employees, Departments, and Projects
SELECT e.FirstName, e.LastName, d.DepartmentName, p.ProjectName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
JOIN Projects p ON e.ProjectID = p.ProjectID;
```

## Advanced Queries

### Subqueries
```sql
-- Subquery example
SELECT FirstName, LastName
FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```

### Aggregate Functions
```sql
-- Using aggregate functions
SELECT DepartmentID, AVG(Salary) AS AvgSalary
FROM Employees
GROUP BY DepartmentID
HAVING AvgSalary > 10000;
```

### Window Functions
```sql
-- Window function example
SELECT FirstName, LastName, Salary,
       RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```

### Common Table Expressions
```sql
-- Common Table Expression (CTE) example
WITH EmployeeCTE AS (
    SELECT EmployeeID, FirstName, LastName
    FROM Employees
)
SELECT * FROM EmployeeCTE;
```

### Indexes
```sql
-- Create an index
CREATE INDEX idx_email ON Employees(Email);
```
