# SQL Commands

SQL commands are instructions used to communicate with a database. They are used to create, retrieve, update, delete, and manage data.

---

# SQL Command Categories

| Category | Purpose |
|----------|---------|
| DDL | Defines the database structure |
| DML | Manipulates the data inside tables |
| DQL | Retrieves data from tables |
| DCL | Controls user permissions |
| TCL | Manages database transactions |

---

# DDL (Data Definition Language)

DDL commands define or modify the database structure.

---

## CREATE

The **CREATE** command is used to create a new database, table, view, or index.

### Syntax

```sql
CREATE DATABASE College;
```

```sql
CREATE TABLE Student(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT,
    Course VARCHAR(30)
);
```

---

## ALTER

The **ALTER** command is used to modify the structure of an existing table.

### Add a Column

```sql
ALTER TABLE Student
ADD Email VARCHAR(50);
```

### Modify a Column

```sql
ALTER TABLE Student
MODIFY Age INT;
```

### Rename a Column

```sql
ALTER TABLE Student
RENAME COLUMN Name TO StudentName;
```

### Drop a Column

```sql
ALTER TABLE Student
DROP COLUMN Email;
```

---

## RENAME

The **RENAME** command changes the name of a table.

```sql
RENAME TABLE Student TO Students;
```

---

## TRUNCATE

The **TRUNCATE** command removes all records from a table without deleting the table.

```sql
TRUNCATE TABLE Student;
```

---

## DROP

The **DROP** command permanently deletes a database or table.

```sql
DROP TABLE Student;
```

```sql
DROP DATABASE College;
```

---

# DML (Data Manipulation Language)

DML commands manipulate the data stored in tables.

---

## INSERT INTO

The **INSERT INTO** command adds new records to a table.

```sql
INSERT INTO Student
VALUES(101,'Rahul',20,'BCA');
```

Multiple records

```sql
INSERT INTO Student
VALUES
(102,'Aman',21,'BCA'),
(103,'Priya',19,'BBA');
```

---

## UPDATE

The **UPDATE** command modifies existing records.

```sql
UPDATE Student
SET Course='MCA'
WHERE StudentID=101;
```

---

## DELETE

The **DELETE** command removes one or more records from a table.

```sql
DELETE FROM Student
WHERE StudentID=101;
```

Delete all rows

```sql
DELETE FROM Student;
```

---

# DQL (Data Query Language)

DQL commands retrieve information from the database.

---

## SELECT

The **SELECT** command retrieves data from one or more tables.

```sql
SELECT * FROM Student;
```

Specific columns

```sql
SELECT Name,Course
FROM Student;
```

---

## DISTINCT

Returns only unique values.

```sql
SELECT DISTINCT Course
FROM Student;
```

---

## WHERE

Filters rows based on a condition.

```sql
SELECT *
FROM Student
WHERE Age>20;
```

---

## ORDER BY

Sorts records in ascending or descending order.

Ascending

```sql
SELECT *
FROM Student
ORDER BY Name ASC;
```

Descending

```sql
SELECT *
FROM Student
ORDER BY Age DESC;
```

---

## LIMIT

### Definition

Returns only a specified number of records.

```sql
SELECT *
FROM Student
LIMIT 5;
```

---

## AS (Alias)

Provides a temporary name to a column or table.

```sql
SELECT Name AS Student_Name
FROM Student;
```

---

# SQL Operators

## AND

Returns records when both conditions are true.

```sql
SELECT *
FROM Student
WHERE Age>18 AND Course='BCA';
```

---

## OR

Returns records if either condition is true.

```sql
SELECT *
FROM Student
WHERE Course='BCA'
OR Course='BBA';
```

---

## NOT

Returns records that do not satisfy a condition.

```sql
SELECT *
FROM Student
WHERE NOT Course='BCA';
```

---

## BETWEEN

Returns values within a range.

```sql
SELECT *
FROM Student
WHERE Age BETWEEN 18 AND 22;
```

---

## IN

Checks whether a value exists in a list.

```sql
SELECT *
FROM Student
WHERE Course IN('BCA','BBA');
```

---

## LIKE

Searches for a pattern.

Starts with A

```sql
SELECT *
FROM Student
WHERE Name LIKE 'A%';
```

Ends with a

```sql
SELECT *
FROM Student
WHERE Name LIKE '%a';
```

Contains "ri"

```sql
SELECT *
FROM Student
WHERE Name LIKE '%ri%';
```

---

## IS NULL

Finds NULL values.

```sql
SELECT *
FROM Student
WHERE Email IS NULL;
```

---

## IS NOT NULL

Finds non-NULL values.

```sql
SELECT *
FROM Student
WHERE Email IS NOT NULL;
```

---

# Aggregate Functions

Aggregate functions perform calculations on multiple rows.

---

## COUNT()

Returns the total number of rows.

```sql
SELECT COUNT(*)
FROM Student;
```

---

## SUM()

Returns the total sum.

```sql
SELECT SUM(Age)
FROM Student;
```

---

## AVG()

Returns the average value.

```sql
SELECT AVG(Age)
FROM Student;
```

---

## MAX()

Returns the highest value.

```sql
SELECT MAX(Age)
FROM Student;
```

---

## MIN()

Returns the lowest value.

```sql
SELECT MIN(Age)
FROM Student;
```

---

# GROUP BY

Groups rows having the same values.

```sql
SELECT Course,
COUNT(*)
FROM Student
GROUP BY Course;
```

---

# HAVING

Filters grouped records.

```sql
SELECT Course,
COUNT(*)
FROM Student
GROUP BY Course
HAVING COUNT(*)>2;
```

---

# SQL Joins

## INNER JOIN

Returns matching records from both tables.

```sql
SELECT *
FROM Student
INNER JOIN Orders
ON Student.StudentID=Orders.StudentID;
```

---

## LEFT JOIN

Returns all records from the left table and matching records from the right table.

```sql
SELECT *
FROM Student
LEFT JOIN Orders
ON Student.StudentID=Orders.StudentID;
```

---

## RIGHT JOIN

Returns all records from the right table and matching records from the left table.

```sql
SELECT *
FROM Student
RIGHT JOIN Orders
ON Student.StudentID=Orders.StudentID;
```

---

## FULL OUTER JOIN

Returns all matching and non-matching records from both tables.

```sql
SELECT *
FROM Student
FULL OUTER JOIN Orders
ON Student.StudentID=Orders.StudentID;
```

---

# UNION

Combines the results of two SELECT queries and removes duplicate rows.

```sql
SELECT Name FROM Student
UNION
SELECT Name FROM Teacher;
```

---

# UNION ALL

Combines the results of two SELECT queries including duplicates.

```sql
SELECT Name FROM Student
UNION ALL
SELECT Name FROM Teacher;
```

---

# EXISTS

Checks whether a subquery returns any records.

```sql
SELECT Name
FROM Student
WHERE EXISTS
(
SELECT *
FROM Orders
WHERE Orders.StudentID=Student.StudentID
);
```

---

# ANY

Returns TRUE if any value satisfies the condition.

```sql
SELECT *
FROM Student
WHERE Age > ANY
(
SELECT Age
FROM Student
WHERE Course='BCA'
);
```

---

# ALL

Returns TRUE only if all values satisfy the condition.

```sql
SELECT *
FROM Student
WHERE Age > ALL
(
SELECT Age
FROM Student
WHERE Course='BCA'
);
```

---

# SQL Constraints

- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- NOT NULL
- DEFAULT
- CHECK
- AUTO_INCREMENT

---

# Views

A View is a virtual table created from one or more tables.

```sql
CREATE VIEW StudentView AS
SELECT Name,Course
FROM Student;
```

---

# Index

An Index improves the speed of searching data.

```sql
CREATE INDEX idx_name
ON Student(Name);
```
---