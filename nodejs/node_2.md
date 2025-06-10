# Node.js, Express, and JavaScript Concepts

## Table of Contents

- [Node.js, Express, and JavaScript Concepts](#nodejs-express-and-javascript-concepts)
  - [Table of Contents](#table-of-contents)
  - [Preparation](#preparation)
  - [NPM and Package Managers](#npm-and-package-managers)
  - [HTTP Cookies](#http-cookies)
  - [Useful References](#useful-references)
  - [PNPM](#pnpm)
  - [Storage Differences](#storage-differences)
  - [JavaScript MutationObserver](#javascript-mutationobserver)
  - [MongoDB vs MySQL](#mongodb-vs-mysql)
  - [JavaScript Coding Interview Questions](#javascript-coding-interview-questions)
  - [JavaScript String Methods](#javascript-string-methods)
  - [Global Error Handling](#global-error-handling)
  - [Shallow Copy vs Deep Copy in JavaScript](#shallow-copy-vs-deep-copy-in-javascript)
  - [Array Methods: filter, map, reduce](#array-methods-filter-map-reduce)
  - [JavaScript Concepts](#javascript-concepts)
  - [ES6 Features](#es6-features)
  - [Call, Apply, and Bind](#call-apply-and-bind)
  - [Closures and Currying](#closures-and-currying)
  - [Middleware in Node.js](#middleware-in-nodejs)
  - [What is Middleware?](#what-is-middleware)
  - [Why Use Express.js on Top of Node.js?](#why-use-expressjs-on-top-of-nodejs)
  - [Node.js Architecture](#nodejs-architecture)
  - [Node.js vs Browser Runtime](#nodejs-vs-browser-runtime)
  - [Buffer in Node.js](#buffer-in-nodejs)
  - [Node.js REPL](#nodejs-repl)
  - [res.write vs res.end vs res.send](#reswrite-vs-resend-vs-ressend)
  - [Streams in Node.js](#streams-in-nodejs)
  - [Choosing node\_modules](#choosing-node_modules)
  - [Proxy Server](#proxy-server)
  - [Blocking vs Non-Blocking in Node.js](#blocking-vs-non-blocking-in-nodejs)
  - [EventEmitter in Node.js](#eventemitter-in-nodejs)
  - [Synchronous vs Asynchronous JavaScript](#synchronous-vs-asynchronous-javascript)
  - [Callback, Callback Hell, Inversion of Control](#callback-callback-hell-inversion-of-control)
  - [Promises and Async/Await](#promises-and-asyncawait)
  - [Semantic Versioning](#semantic-versioning)
  - [Express.js Middleware](#expressjs-middleware)
  - [express-slow-down](#express-slow-down)
  - [express-rate-limit](#express-rate-limit)
  - [REST API vs SOAP API](#rest-api-vs-soap-api)
  - [HTTP Methods](#http-methods)
  - [Web Application Architecture](#web-application-architecture)
  - [HTTP Protocol](#http-protocol)
  - [Web Server vs Application Server](#web-server-vs-application-server)
  - [REST API Introduction](#rest-api-introduction)
  - [📦 Node.js Buffer vs Stream – Explained with Simple Code](#-nodejs-buffer-vs-stream--explained-with-simple-code)
  - [🔹 What is a Buffer?](#-what-is-a-buffer)
  - [🔹 What is a Stream?](#-what-is-a-stream)
  - [✅ Real-World Analogy](#-real-world-analogy)
  - [💻 Code Example](#-code-example)
    - [📁 Using Buffer (Read whole file into memory)](#-using-buffer-read-whole-file-into-memory)


## Preparation

- Create a Node server?
- ES6 
- What is middleware?
- Why do we use Express.js on top of Node.js?
- Error handling in Node.js
- Coding related to `setTimeout`
- How does Node work behind the scenes?
- Call, apply, and bind
- Difference between REST API and SOAP API
- Different HTTP methods and their usages

---

## NPM and Package Managers

- What is NPM?
- What is a callback function? How does it work in Node.js?
- Does Node.js support multi-threaded request/response?
- Explain Node.js architecture. How does it work?
- Explain asynchronous and non-blocking API?
- Create a localhost server
- Create a localhost server with port 3000, handle 10 requests one by one. Show how response fetch works. Explain how it works.
- What are the core modules of Node.js?
- Explain event emitter. Write a sample.
- What is `package.json`? How does it help in configuring and running Node.js?
- `console.log(60 + "20" + 20*20)`
- `console.log(undefined == undefined);`
- `console.log(undefined === undefined);`

---

## HTTP Cookies

- [GeeksforGeeks: HTTP Cookies](https://www.geeksforgeeks.org/http-cookies/)
- [Express.js: res.cookie](https://expressjs.com/en/4x/api.html#res.cookie)
- [Node Express Postgres Auth Example](https://github.com/sjMalik/node-express-postgres-auth/blob/main/README.md#authentication)

---

## Useful References

- [NPM and Package.json - FreeCodeCamp](https://www.freecodecamp.org/news/what-is-npm-a-node-package-manager-tutorial-for-beginners/)
- [Node.js Core Modules - Flavio Copes](https://flaviocopes.com/node-core-modules/)
- [JavaScript, Node.js, Express, HTML, CSS Handbook](https://flaviocopes.com/access/)

---

## PNPM

**Why is pnpm so much faster than NPM?**

- Shared dependency model: Stores packages in a global store and connects to them from each project, saving disk space and installation time.
- Parallel installation: Uses multiple threads to install packages concurrently.
- Symlink-based linking: Creates symlinks instead of duplicating packages.
- Small package cache: Smaller cache due to shared dependency architecture.
- Downloads packages and dependencies once, reducing network use.
- Supports several registries and has automatic garbage collection for unused packages.

[Reference](https://www.linkedin.com/posts/thealiraza_javascript-npm-yarn-activity-7060554724860661760-D27H/?utm_source=share&utm_medium=member_android)

---

## Storage Differences

- Difference Between Local Storage, Session Storage, and Cookies

---

## JavaScript MutationObserver

---

## MongoDB vs MySQL

- [When to use MongoDB rather than MySQL](https://medium.com/@rsk.saikrishna/when-to-use-mongodb-rather-than-mysql-d03ceff2e922)
- [MongoDB vs MySQL - Educative](https://www.educative.io/blog/mongodb-vs-mysql)

**MySQL is a good choice if:**
- Your database won’t scale much.
- Your data structure is fixed.
- You have a high transaction rate.
- Data security is a top priority.
- You need better support or are working with legacy applications.

**MongoDB is a good choice if:**
- You want high data availability and instant recovery.
- You have an unstable schema or want to lower migration costs.
- Your services are cloud-based.
- You want to speed up development.
- Ideal for real-time analytics, mobile apps, IoT, etc.

---

## JavaScript Coding Interview Questions

- [Reference](https://www.fullstacktutorials.com/interviews/javascript-coding-questions-answers-6.html)

---

## JavaScript String Methods

- All string methods return a new string (strings are immutable).

---

## Global Error Handling

- [Node.js Process - Tutorialspoint](https://www.tutorialspoint.com/nodejs/nodejs_process.htm)
- [Node.js Process Object - FreeCodeCamp](https://www.freecodecamp.org/news/node-process-object-explained/)

```js
process.on('uncaughtException', (err) => { 
    console.log('whoops! there was an error'); 
});
```

---

## Shallow Copy vs Deep Copy in JavaScript

- [GeeksforGeeks: Shallow Copy in JavaScript](https://www.geeksforgeeks.org/what-is-shallow-copy-in-javascript/?ref=rp)

**Deep Copy Example with Lodash:**
```js
var employee = {
    eid: "E102",
    ename: "Jack",
    eaddress: "New York",
    salary: 50000,
    details: function () {
        return "Employee Name: " + this.ename + "-->Salary: " + this.salary;
    }
}
var deepCopy = lodash.cloneDeep(employee);
```

---

## Array Methods: filter, map, reduce

- `map()`: Iterates and transforms each element, returns a new array.
- `filter()`: Filters elements based on a condition, returns a new array.
- `reduce()`: Reduces array to a single value by applying a function.

---

## JavaScript Concepts

- Prototype in JavaScript
- Primitive and Non-primitive data-types
- Var, Let, and Const – What's the Difference?
- Null vs Undefined

---

## ES6 Features

- `const` and `let` for variable declarations
- Arrow functions
- Template literals
- Object and array destructuring
- Default parameters
- Classes
- Rest and spread operators

---

## Call, Apply, and Bind

- [FreeCodeCamp: Apply, Call, and Bind](https://www.freecodecamp.org/news/how-to-use-the-apply-call-and-bind-methods-in-javascript-80a8e6096a90/)

```js
const employee1 = {name: 'Surajit'};
const invite = function (greetings1, greetings2) {
    console.log(greetings1+ ' '+ this.name+ ', '+greetings2);
}
// bind
const inviteEmp1 = invite.bind(employee1);
inviteEmp1('Hello', 'How are you?');
// call
invite.call(employee1, 'Hello',  'How are you?');
// apply
invite.apply(employee1, ['Hello',  'How are you?']);
```

---

## Closures and Currying

- [FreeCodeCamp: JavaScript Closures](https://www.freecodecamp.org/news/lets-learn-javascript-closures-66feb44f6a44/)
- [Closure Coding Examples](https://coderbyte.com/algorithm/3-common-javascript-closure-questions)

**Closure Example:**
```js
function foo() {
    var b = 1;
    function inner() {
        return b;
    }
    return inner;
}
var get_func_inner = foo();
```

**Currying Example:**
```js
function calculateVolume(l) {
    return function(w) {
        return function(h) {
            return l * w * h;
        }
    }
}
```

---

## Middleware in Node.js

- CORS Middleware
    ```js
    const cors = require("cors");
    app.use(cors());
    ```
- JSON Middleware
    ```js
    app.use(express.json());
    ```
- URL-encoded Middleware
    ```js
    app.use(express.urlencoded({extended: false}));
    ```
- Static Middleware
    ```js
    app.use(express.static(path.join(__dirname, 'public')));
    ```
- Error-Handling Middleware
    ```js
    app.use(function(err, req, res, next) {
        res.locals.message = err.message;
        res.locals.error = req.app.get('env') === 'development' ? err : {};
        res.status(err.status || 500);
        res.render('error');
    });
    ```
- Method-Override Middleware
    ```js
    var methodOverride = require('method-override');
    app.use(methodOverride('_method'));
    ```
- Morgan, Express-slow-down, Express-rate-limit

---

## What is Middleware?

Middleware is a function that has access to request, response, and the next middleware function. It exists between the request and response cycles of Node.js execution.

**Types of Middleware:**
- Application-level
- Router-level
- Built-in

**Advantages:**
- Simplifies software development
- Controls connections between components
- Cost-effective for managing resources
- Supports authentication, load balancing, and more

---

## Why Use Express.js on Top of Node.js?

Express.js is a fast, flexible, and minimalist web framework built on top of Node.js. It simplifies building web applications and RESTful APIs by providing routing, middleware, templating, and database integration.

**ExpressJS vs NodeJS Table:**

| Feature         | ExpressJS                | NodeJS                        |
|-----------------|-------------------------|-------------------------------|
| Purpose         | Web framework           | JavaScript runtime            |
| Built on        | NodeJS                  | Chrome’s V8 JavaScript engine |
| Focus           | Server-side development | General-purpose JS programming|
| Key features    | Routing, middleware     | Non-blocking I/O, event-driven|
| Use Cases       | Web apps, REST APIs     | Scripting, CLI tools          |

---

## Node.js Architecture

- Built on Chrome V8 engine and Libuv (C/C++)
- Single-threaded, event-driven, non-blocking I/O
- Uses event loop and thread pool for heavy tasks

**Event Loop Phases:**
1. Expired timeout callbacks (e.g., `setTimeout`)
2. I/O polling callbacks
3. `setImmediate` callbacks
4. Close callbacks

**Example:**
```js
console.log("This is the first statement");
setTimeout(function(){
    console.log("This is the second statement");
}, 1000);
console.log("This is the third statement");
```

---

## Node.js vs Browser Runtime

- Node.js: No DOM, access to system resources, uses `global`
- Browser: Has DOM, uses `window`

---

## Buffer in Node.js

- Used to store binary data
- Example:
    ```js
    var b = new Buffer(10000);
    var str = " ";
    b.write(str);
    console.log(str.length);
    console.log(b.length);
    ```

---

## Node.js REPL

- REPL: Read, Eval, Print, Loop
- Start with `node` in terminal

---

## res.write vs res.end vs res.send

- `res.send`: Express.js only, combines `res.write` + `res.end`
- `res.write`: Can be called multiple times
- `res.end`: Ends the response

---

## Streams in Node.js

- Streams handle reading/writing data efficiently (in chunks)
- Types: Writable, Readable, Duplex, Transform

---

## Choosing node_modules

**Factors:**
- Number of downloads
- Recent updates
- Contributors
- Documentation
- Test coverage
- GitHub activity

---

## Proxy Server

- Acts as intermediary between client and server
- Used for hiding API keys, rate limiting, caching

---

## Blocking vs Non-Blocking in Node.js

**Blocking Example:**
```js
const data = fs.readFileSync(filepath, {encoding: 'utf8'});
```

**Non-Blocking Example:**
```js
fs.readFile(filepath, {encoding: 'utf8'}, (err, data) => {
    console.log("data");
});
```

---

## EventEmitter in Node.js

```js
const EventEmitter = require('events');
const eventEmitter = new EventEmitter();

eventEmitter.on('start', () => {
    console.log('started');
});
eventEmitter.emit('start');
```

---

## Synchronous vs Asynchronous JavaScript

- Synchronous: Executes line by line
- Asynchronous: Executes without blocking, uses callbacks/promises

---

## Callback, Callback Hell, Inversion of Control

- Callback: Function passed as argument to another function
- Callback Hell: Nested callbacks, hard to read/maintain
- Inversion of Control: Loss of control when passing callbacks

---

## Promises and Async/Await

- Promises: Handle async operations, avoid callback hell
- Async/Await: Syntactic sugar over promises, makes async code look synchronous

**Example:**
```js
async function getData() {
    var data = "Hello World";
    return data;
}
getData().then(data => console.log(data));
```

---

## Semantic Versioning

- Format: `major.minor.patch`
- `^` (caret): Allow minor and patch updates
- `~` (tilde): Allow patch updates only

---

## Express.js Middleware

- Handles requests between server and controller
- Can process requests, add logging/authentication, set headers, optimize performance

**Example:**
```js
app.use(express.json());
app.use((error, req, res, next) => {
    res.status(error.status || 500).json({
        message: error.message,
        stack: process.env.NODE_ENV === 'production' ? '' : error.stack
    });
});
```

---

## express-slow-down

- Slows down responses after a threshold

```js
const slowDown = require("express-slow-down");
const speedLimiter = slowDown({
    windowMs: 15 * 60 * 1000,
    delayAfter: 100,
    delayMs: 500
});
app.use(speedLimiter);
```

---

## express-rate-limit

- Limits number of requests per window

```js
import rateLimit from 'express-rate-limit'
const limiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 100,
    standardHeaders: true,
    legacyHeaders: false,
});
app.use(limiter);
```

---

## REST API vs SOAP API

| Feature         | REST API                         | SOAP API                        |
|-----------------|----------------------------------|---------------------------------|
| Type            | Architectural style              | Protocol                        |
| Data Format     | JSON, XML, Plain-text, etc.      | XML only                        |
| Bandwidth       | Less                             | More                            |
| Security        | SSL, HTTPS                       | SSL, WS-Security                |
| Flexibility     | High                             | Low                             |
| ACID Compliance | No                               | Yes                             |

---

## HTTP Methods

- **GET**: Retrieve resource
- **POST**: Create resource
- **PUT**: Update or create resource
- **PATCH**: Modify resource
- **DELETE**: Delete resource

---

## Web Application Architecture

- **Presentation Layer**: Client/browser
- **Business Layer**: Handles logic/routing
- **Persistence Layer**: Data storage

**Types:**
- Single Page Applications (SPA)
- Microservices
- Serverless Architectures

---

## HTTP Protocol

- Media independent, connectionless, stateless
- Request includes: Request-line, headers, method, URI, etc.

---

## Web Server vs Application Server

- **Web Server**: Handles HTTP requests, serves static content
- **Application Server**: Handles business logic, state, security, persistence

---

## REST API Introduction

- REST: Representational State Transfer
- Uses HTTP methods for CRUD operations
- Idempotence: Multiple identical requests have the same effect

---


## 📦 Node.js Buffer vs Stream – Explained with Simple Code

## 🔹 What is a Buffer?

A **Buffer** is a temporary storage for raw binary data. It loads the **entire** file or data into memory before processing.

🧠 **Think of it like**:  
> “Hold all data in hand, then process.”

---

## 🔹 What is a Stream?

A **Stream** handles data **chunk by chunk** — it processes data **as it arrives**, without loading the whole thing into memory.

🧠 **Think of it like**:  
> “Process data while receiving it.”

---

## ✅ Real-World Analogy

- **Buffer**: You wait for the full movie to download before watching.
- **Stream**: You start watching while it’s still downloading.

---

## 💻 Code Example

Assume you have a large file: `large.txt`.

### 📁 Using Buffer (Read whole file into memory)

```js
const fs = require('fs');

fs.readFile('large.txt', (err, data) => {
  if (err) throw err;
  console.log('File size:', data.length); // data is a Buffer
  // Process the whole file at once
});


