# 📘 Database (DBMS) & SQL Notes

# Introduction

Before databases were introduced, data was stored using the **File System**. Although simple, it had many problems that led to the development of DBMS.

---

# File System

A **File System** is a method of storing data in separate files on a computer.

### Example
- Student.txt
- Employee.txt
- Salary.txt

Each file stores information independently.

---

# Disadvantages of File System

### 1. Data Redundancy
The same data is stored in multiple files, wasting storage.

**Example:** A student's address appears in different files.


### 2. Data Inconsistency
If data is updated in one file but not another, different files contain different values.


### 3. Difficult Data Access
Searching for information from multiple files is slow and difficult.


### 4. Poor Security
Anyone with file access can modify or delete data.


### 5. No Data Integrity
Incorrect or invalid data can easily be entered.


### 6. No Backup and Recovery
Recovering lost data after a crash is difficult.


### 7. Data Isolation
Data is stored in different files and formats, making relationships difficult.


### 8. Limited Multi-user Access
Multiple users cannot work efficiently on the same data simultaneously.

---

# Database

A **Database** is an organized collection of related data that is stored electronically and can be easily accessed, managed, updated, and retrieved.

### Examples
- Banking Database
- Hospital Database
- College Database
- Railway Reservation Database

### Features
- Organized data
- Fast searching
- Secure storage
- Easy updating
- Data sharing

---

# DBMS (Database Management System)

A **DBMS** is software that allows users to create, store, retrieve, update, and manage databases.

It acts as an interface between the user and the database.

### Examples
- MySQL
- Oracle
- SQL Server
- PostgreSQL
- SQLite
- MS Access

## Advantages of DBMS

- Reduces data redundancy
- Maintains consistency
- Better security
- Backup & recovery
- Data sharing
- Data integrity
- Easy maintenance

---

# RDBMS (Relational Database Management System)

An **RDBMS** stores data in the form of **tables** (rows and columns).

Tables are connected using **Primary Keys** and **Foreign Keys**.

### Examples
- MySQL
- PostgreSQL
- Oracle
- SQL Server

## Features of RDBMS

- Data stored in tables
- Supports relationships
- Uses SQL
- Reduces redundancy
- Ensures data integrity
- Supports transactions (ACID)

---

# Difference Between DBMS and RDBMS

| DBMS | RDBMS |
|------|--------|
| Stores data as files or tables | Stores data in related tables |
| Relationships are limited | Relationships supported |
| Less secure | More secure |
| Doesn't always support SQL | Uses SQL |
| Suitable for small applications | Suitable for large applications |

---

# What is SQL?

**SQL (Structured Query Language)** is a standard language used to communicate with relational databases.

SQL is used to:

- Create databases
- Create tables
- Insert data
- Update data
- Delete data
- Retrieve data
- Manage users
- Control permissions

---

# #NOTE:

A **Language** is a set of rules and commands used to communicate with a computer.

Examples:
- C
- Java
- Python
- SQL

A **Query** is a request given to a database to perform an operation.

Examples:

Retrieve data

```sql
SELECT * FROM Student;
```

Insert data

```sql
INSERT INTO Student VALUES(101,'Rahul');
```

Every SQL statement is called a **Query**.

---

# SQL vs NoSQL

| SQL | NoSQL |
|------|--------|
| Relational Database | Non-relational Database |
| Stores data in tables | Stores data as documents, key-value, graph, or column |
| Fixed schema | Flexible schema |
| Structured data | Structured & Unstructured data |
| Uses SQL language | Different query methods |
| ACID properties | BASE properties (mostly) |
| Better for complex queries | Better for large-scale applications |

---

## SQL Examples

- MySQL
- Oracle
- PostgreSQL
- SQL Server
- SQLite

---

## NoSQL Examples

- MongoDB
- Cassandra
- Redis
- CouchDB
- Firebase Firestore

---

# Structured Data

Structured Data is data organized in rows and columns with a predefined schema.

### Characteristics

- Fixed format
- Easy to search
- Stored in tables
- Uses SQL

### Example

| StudentID | Name | Course |
|-----------|------|--------|
| 101 | Rahul | BCA |
| 102 | Aman | BBA |

---

# Unstructured Data

Unstructured Data has no predefined format or schema.

### Examples

- Images
- Videos
- Audio
- Emails
- PDFs
- Social media posts
- Documents

---

## Characteristics

- Flexible format
- Difficult to analyze
- Very large volume
- Stored in NoSQL databases or cloud storage

---

# Structured vs Unstructured Data

| Structured Data | Unstructured Data |
|-----------------|-------------------|
| Stored in tables | Stored as files/documents |
| Fixed schema | No fixed schema |
| Easy to search | Hard to search |
| SQL databases | NoSQL databases |
| Examples: Student records | Examples: Images, Videos |

---

# Types of SQL Commands

| Category | Purpose |
|----------|----------|
| DDL | Define database structure |
| DML | Manipulate data |
| DQL | Retrieve data |
| DCL | Control permissions |
| TCL | Manage transactions |

---

# SQL Command Flow

```text
Database
      │
      ▼
   SQL Query
      │
      ▼
 Database Engine
      │
      ▼
 Result Returned
```

---

# Database Hierarchy

```text
Database
   │
   ├── Tables
   │      │
   │      ├── Rows (Records)
   │      └── Columns (Fields)
   │
   ├── Views
   ├── Indexes
   └── Stored Procedures
```

---

# Quick Revision

```text
File System
      │
      ▼
Problems
      │
      ▼
Database
      │
      ▼
DBMS
      │
      ▼
RDBMS
      │
      ▼
SQL
      │
      ▼
Queries
      │
      ▼
Retrieve & Manage Data
```