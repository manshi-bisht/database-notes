# Backend Development 
---

# What is Express.js?

Node.js can create a web server on its own, but it requires writing a lot of code manually.

**Express.js** is a framework built on top of Node.js that makes backend development easier and faster.

Instead of writing everything from scratch, Express provides useful functions for:

- Handling URLs
- Managing requests
- Sending responses
- Creating routes
- Using middleware

### Without Express

Node.js has to:

- Read the URL
- Check the HTTP method
- Parse incoming data
- Create the response manually

This requires more code.

### With Express

Express automatically handles these common tasks, allowing developers to focus only on the application's logic.

---

# What is a Framework?

A framework is a collection of tools and predefined code that helps developers build applications faster.

Instead of creating everything from zero, a framework already provides a structure.

### Examples

- Express.js
- Fastify
- Koa
- NestJS

Among these, Express is one of the most popular frameworks for learning backend development.

---

# Basic Route in Express

```javascript
app.get("/hello", (req, res) => {
    res.json({
        message: "Hello"
    });
});
```

### Explanation

- `app.get()` creates a GET route.
- `/hello` is the URL.
- `req` contains information sent by the client.
- `res` is used to send data back.

---

# 4. Understanding Request (req)

The **request object** contains everything the client sends to the server.

Some useful properties are:

## req.params

Used for dynamic values inside the URL.

Example

```
/users/5
```

Here,

```
req.params.id
```

returns

```
5
```

---

## req.query

Used for query parameters.

Example

```
/users?limit=10
```

```
req.query.limit
```

returns

```
10
```

---

## req.body

Contains data sent inside a POST or PUT request.

Example

```json
{
    "name": "John"
}
```

Important:

`req.body` only works after using:

```javascript
app.use(express.json());
```

---

## req.method

Returns the HTTP method.

Examples

```
GET
POST
PUT
DELETE
```

---

## req.url

Returns the requested URL.

Example

```
/documents
```

---

# Understanding Response (res)

The response object sends data back to the client.

Common methods:

```javascript
res.send()
```

Sends plain text or HTML.

---

```javascript
res.json()
```

Sends JSON data.

---

```javascript
res.status(404)
```

Sets the HTTP status code.

Example

```javascript
res.status(404).json({
    error: "Not Found"
});
```

---

# Routing

Routing decides which function should run when a specific URL is requested.

Example

```
GET /hello
```

↓

```
Route matches
```

↓

```
Controller runs
```

↓

```
Response is returned
```

---

# Routing Flow

```
Client

   │

   ▼

Route

   │

   ▼

Controller

   │

   ▼

Response
```

---

# Middleware

Middleware is a function that runs **before** the request reaches the controller.

It can:

- Check authentication
- Validate data
- Log requests
- Modify request data
- Stop invalid requests

---

## Middleware Structure

```javascript
function myMiddleware(req, res, next){

    // work here

    next();
}
```

`next()` passes control to the next middleware or controller.

If `next()` is not called, the request stops there.

---

# Middleware Flow

```
Client

   │

   ▼

express.json()

   │

   ▼

Logger Middleware

   │

   ▼

Controller

   │

   ▼

Response
```

---

# Why Middleware Order Matters

Correct Order

```javascript
app.use(express.json());

app.use(logger);

app.use(routes);
```

Wrong Order

```javascript
app.use(routes);

app.use(express.json());
```

Result:

```
req.body

↓

undefined
```

Always place `express.json()` before your routes.

---

# Logger Middleware

A logger prints information about every request.

Example

```javascript
function logger(req,res,next){

    console.log(req.method);

    console.log(req.url);

    next();
}
```

Example Output

```
GET

/api/documents
```

This helps during debugging.

---

# npm

npm stands for

**Node Package Manager**

It has two meanings:

1. The package registry
2. The command line tool

It is used to install and manage packages.

---

# package.json

Every Node project contains a file called

```
package.json
```

It stores

- Project name
- Version
- Scripts
- Dependencies
- Project information

Create it using

```bash
npm init -y
```

---

# Installing Packages

Install Express

```bash
npm install express
```

Install Nodemon

```bash
npm install --save-dev nodemon
```

Install Global Package

```bash
npm install -g nodemon
```

Remove Package

```bash
npm uninstall express
```

---

# Local vs Global Installation

## Local Installation

Package is available only inside the current project.

Example

```
npm install express
```

---

## Global Installation

Package becomes available across the entire computer.

Example

```
npm install -g nodemon
```

---

# Dependencies vs DevDependencies

## Dependencies

Required when the application runs in production.

Examples

- Express
- Mongoose

---

# Semantic Versioning (SemVer)

Every package version has three parts.

```
MAJOR.MINOR.PATCH
```

Example

```
4.22.2
```

Meaning

```
4

↓

Major Version

22

↓

Minor Version

2

↓

Patch Version
```

---

## Meaning of Each Part

### Major

Breaking changes.

Old code may stop working.

---

### Minor

New features are added.

Old code usually continues working.

---

### Patch

Bug fixes.

No major changes.

---

# Version Symbols

```
^4.18.0
```

Means

Any newer version inside Version 4.

Example

```
4.22.2
```

can be installed.

---

```
~4.18.0
```

Only patch updates.

---

```
4.18.0
```

Exactly this version.

No updates.

---

# package-lock.json

This file stores the exact package versions installed on your computer.

Benefits

- Same versions for everyone
- Fewer bugs
- Consistent project setup

Always commit this file to Git.

---

# Package Visibility

## Public Package

Anyone can install it.

---

## Private Package

Only authorized users can access it.

---

# Useful npm Commands

Create package.json

```bash
npm init -y
```

Install all dependencies

```bash
npm install
```

Install a package

```bash
npm install express
```

Install globally

```bash
npm install -g nodemon
```

Remove package

```bash
npm uninstall express
```

Check outdated packages

```bash
npm outdated
```

---
# Standard Backend Project Structure

```
project/

│

├── app.js

├── routes/

├── controllers/

├── models/

├── middleware/

├── package.json

├── package-lock.json

└── node_modules/
```

---

# app.js

The main entry point of the application.

Responsibilities

- Create Express app
- Register middleware
- Register routes
- Start the server

---

# routes/

Routes decide

**Which URL should call which controller.**

Example

```
GET /documents

↓

documentController
```

---

# controllers/

Controllers handle requests.

Responsibilities

- Receive req
- Call model
- Send response

Controllers know

- req
- res

Controllers should **not** directly read or write files.

---

# models/

Models manage data.

Responsibilities

- Read data
- Write data
- Update data
- Delete data

Models should never:

- Use req
- Use res
- Send responses

---

# middleware/

Runs before controllers.

Examples

- Logger
- Authentication
- Validation

---

# Backend Request Flow

```
Client

   │

   ▼

Route

   │

   ▼

Middleware

   │

   ▼

Controller

   │

   ▼

Model

   │

   ▼

Database

   │

   ▼

Controller

   │

   ▼

Response
```
---

# Models

Models are responsible only for data.

They should

- Read data
- Write data
- Find records
- Delete records

They should never

- Use req
- Use res
- Return HTTP status codes

---

# Controllers

Controllers connect routes with models.

Responsibilities

- Receive request
- Call model
- Check returned data
- Send response

Controllers know

- req
- res

Controllers should not directly access files or the database logic.

---

# Model vs Controller

| Model | Controller |
|--------|------------|
| Handles data | Handles request |
| Reads/Writes data | Sends response |
| Doesn't know req or res | Knows req and res |
| No status codes | Returns status codes |

---

# 15. Postman

Postman is used to test backend APIs.

With Postman, you can

- Send GET requests
- Send POST requests
- Send JSON data
- Check responses
- Save API collections

The browser address bar can only send **GET** requests.

To test **POST**, **PUT**, and **DELETE** requests, Postman is required.

---

# Important Points to Remember

- Express makes backend development much easier.
- `req` contains client data.
- `res` sends data back.
- Middleware runs before controllers.
- Middleware order is very important.
- Always call `next()` inside middleware.
- `express.json()` must be above your routes.
- `package.json` stores project information.
- `package-lock.json` stores exact installed versions.
- Controllers handle requests.
- Models handle data.
- Controllers and models should not do each other's work.
- Postman is essential for testing APIs.

---

# Quick Revision

```
Client

↓

Express

↓

Middleware

↓

Route

↓

Controller

↓

Model

↓

Database

↓

Controller

↓

Response
```