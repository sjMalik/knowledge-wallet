# Contents

- [Contents](#contents)
  - [JavaScript (the language) itself is synchronous, but it supports asynchronous programming](#javascript-the-language-itself-is-synchronous-but-it-supports-asynchronous-programming)
  - [Node.js (JavaScript runtime) is asynchronous by nature, even though you write it in JavaScript](#nodejs-javascript-runtime-is-asynchronous-by-nature-even-though-you-write-it-in-javascript)
  - [Synchronous Built-in APIs (e.g., for file operations)](#synchronous-built-in-apis-eg-for-file-operations)
  - [Using async/await to make asynchronous code look synchronous](#using-asyncawait-to-make-asynchronous-code-look-synchronous)
  - [let vs var Scope (Closure in Loops)](#let-vs-var-scope-closure-in-loops)
  - [Why different behavior for var and let](#why-different-behavior-for-var-and-let)
  - [Arrow Function this Binding](#arrow-function-this-binding)
  - [Destructuring with Default Values](#destructuring-with-default-values)
  - [Promise Basics](#promise-basics)
  - [Missed Return](#missed-return)
  - [What is middleware in Node.js (Express)?](#what-is-middleware-in-nodejs-express)
  - [How would you create middleware that catches errors in Express?](#how-would-you-create-middleware-that-catches-errors-in-express)
  - [Why does Promise run before setTimeout even with 0 ms delay?](#why-does-promise-run-before-settimeout-even-with-0-ms-delay)
  - [Advantages of Promises over callbacks?](#advantages-of-promises-over-callbacks)

---

## JavaScript (the language) itself is synchronous, but it supports asynchronous programming

**Nature:** JavaScript is single-threaded and synchronous by default.

**Synchronous by Default:** Code is executed line by line, and the next line waits until the current line finishes.

**Asynchronous Capabilities:** JavaScript can handle asynchronous operations using:

- `setTimeout()`, `setInterval()`
- Promises
- async/await
- Event loops (in the browser or Node.js)

> 📌 So, JavaScript itself is synchronous, but it supports asynchronous programming through language features and APIs.

---

## Node.js (JavaScript runtime) is asynchronous by nature, even though you write it in JavaScript 

**Nature:** Node.js is event-driven, non-blocking, and designed for asynchronous programming.

**Asynchronous by Design:** Node.js uses:

- Event loop
- Callbacks, Promises, async/await
- Non-blocking I/O APIs

**Built for Concurrency:** This is especially useful for handling multiple network requests, file I/O, etc., without blocking the main thread.

> 📌 So, Node.js is asynchronous by nature, even though you write it in JavaScript (which is synchronous by default).

---

## Synchronous Built-in APIs (e.g., for file operations)

Node.js provides synchronous versions of some functions, especially in the `fs` module.

🔹 **Example: Read file synchronously**

```js
const fs = require('fs');

// Synchronous version
const data = fs.readFileSync('example.txt', 'utf8');
console.log('File contents:', data);

console.log('This line waits until file reading is done.');
```

`fs.readFileSync` blocks the event loop until the file is fully read.

---

## Using async/await to make asynchronous code look synchronous

This doesn't block the event loop but allows sequential-looking code.

```js
const fs = require('fs/promises');

async function readFile() {
    const data = await fs.readFile('example.txt', 'utf8');
    console.log('File contents:', data);
}

readFile();
```

This is still asynchronous under the hood, but appears sequential.

---

## let vs var Scope (Closure in Loops)

```js
function test() {
    for (var i = 0; i < 3; i++) {
        setTimeout(() => console.log(i), 100);
    }

    for (let j = 0; j < 3; j++) {
        setTimeout(() => console.log(j), 100);
    }
}

test();
```

**Output:**
```
3
3
3
0
1
2
```

**Explanation:**

- `var` is function-scoped, so all timeouts share the same `i`, which becomes 3 after the loop finishes.
- `let` is block-scoped, so each `j` in the loop gets a new binding (closure), preserving its value.

---

## Why different behavior for var and let

**A:**

- `var` is hoisted and initialized with `undefined`.
- `let` is hoisted but stays uninitialized until declaration (Temporal Dead Zone).

**Q: What is Temporal Dead Zone?**  
**A:** The time between entering scope and variable declaration where accessing the variable throws a ReferenceError.

```js
console.log(a);
var a = 10;

function test() {
    console.log(b);
    let b = 20;
}
test();
```

**Output:**
```
console.log(a)
undefined (var hoisted)

console.log(b);
                            ^
ReferenceError: Cannot access 'b' before initialization
```

---

## Arrow Function this Binding

Arrow functions don’t have their own `this`. They use `this` from the surrounding lexical scope, which here is the global object (no value property).  
Arrow: lexical binding; Regular: dynamic based on call site.

```js
const obj = {
    count: 10,
    a: function () {
        console.log(this.count);
    },
    b: () => {
        console.log(this.count);
    }
};

obj.a(); // ?
obj.b();   // ?
```

**Output:**
```
10
undefined
```

**Explanation:**

- In regular function `a()`, `this` refers to `obj`, so `this.count = 10`.
- Arrow functions do not have their own `this`, they inherit it from the lexical context (likely global or undefined).

---

## Destructuring with Default Values

```js
const { name = 'Anonymous', age } = { age: 30 };
console.log(name, age);
```

**Output:**
```
Anonymous 30
```

**Explanation:**  
Destructuring `{ age: 30 }` does not include a `name` key.  
So `name` falls back to its default value: `'Anonymous'`.

---

## Promise Basics

```js
console.log("1");

Promise.resolve().then(() => {
    console.log("2");
});

console.log("3");
```

**Expected Output:**
```
1
3
2
```

Because Promises (`then`) run in the microtask queue, after the current call stack is empty.

---

## Missed Return

```js
Promise.resolve(1)
    .then(x => {
        x + 1;
    })
    .then(console.log);
```

**Expected Output:**
```
undefined
```

🔍 Because `x + 1` is not returned, the value passed to the next `.then()` is `undefined`.

---

## What is middleware in Node.js (Express)?

Middleware is a function that has access to the request (`req`), response (`res`), and the next middleware function in the application’s request-response cycle.

Consider the following Express.js route with two middleware functions:

```js
function first(req, res, next) {
    console.log('First middleware');
}

function second(req, res, next) {
    console.log('Second middleware');
    res.send('Done');
}

app.get('/', first, second);
```

What will happen when a client makes a GET request to `'/'`? Will both middleware functions run? Why or why not?

Only `'First middleware'` is logged, and the request hangs without a response.

`'Second middleware'` never runs because `next()` is not invoked in the first middleware.

Middleware must either call `next()`, end the response (`res.send`, `res.end`), or pass control via error handling (`next(err)`).

---

## How would you create middleware that catches errors in Express?

By defining middleware with four parameters: `(err, req, res, next)`

```js
function errorHandler(err, req, res, next) {
    console.error(err.stack);
    res.status(500).send('Something broke!');
}
```

---

## Why does Promise run before setTimeout even with 0 ms delay?

**A:** Promises go to the microtask queue, which has higher priority and runs immediately after the current stack completes. `setTimeout` goes to the macrotask queue, which runs after all microtasks finish.

**Extra:** Microtasks include Promises and `process.nextTick`. Macrotasks include timers, I/O, and UI rendering.

```js
console.log('Start');

setTimeout(() => {
    console.log('Timeout 1');
}, 0);

Promise.resolve().then(() => {
    console.log('Promise 1');
});

console.log('End');
```

**Output:**
```
Start
End
Promise 1
Timeout 1
```

---

##  Advantages of Promises over callbacks?

- Avoids callback hell (nested callbacks).
- Easier chaining (`.then()`).
- Cleaner error handling (`.catch()`).
- Can combine multiple async results with `Promise.all`.

**Callback Hell**

```js
getUser(1, function(user) {
    getPosts(user.id, function(posts) {
        getComments(posts[0].id, function(comments) {
            console.log(comments);
        });
    });
});
```

**Promise Version**

```js
getUser(1)
    .then(user => getPosts(user.id))
    .then(posts => getComments(posts[0].id))
    .then(comments => console.log(comments))
    .catch(err => console.error(err));
```