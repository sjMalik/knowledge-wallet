# NodeJS Interview QnAs

## Table of Contents

<!-- Add table of contents -->
- [NodeJS Interview QnAs](#nodejs-interview-qnas)
  - [Table of Contents](#table-of-contents)
  - [LTIMindtree: Interview - NodeJS Developer](#ltimindtree-interview---nodejs-developer)
    - [1st Round](#1st-round)
      - [What is Node.js?](#what-is-nodejs)
      - [What is callback hell?](#what-is-callback-hell)
      - [What is Promise.all()?](#what-is-promiseall)
      - [Difference between array.forEach() and array.map](#difference-between-arrayforeach-and-arraymap)
      - [How do I choose node\_modules?](#how-do-i-choose-node_modules)
      - [How do you secure the API?](#how-do-you-secure-the-api)
        - [Express Slow Down \& Rate Limit](#express-slow-down--rate-limit)
        - [JWT Authorization](#jwt-authorization)
        - [Use HTTPS/TLS for REST APIs](#use-httpstls-for-rest-apis)
      - [What is the closure?](#what-is-the-closure)
    - [Coding Test](#coding-test)
    - [2nd Round](#2nd-round)
  - [II) ESKO: Interview - NodeJS Developer](#ii-esko-interview---nodejs-developer)
  - [III) Engineersmind.com - Interview (Full Stack Web Developer)](#iii-engineersmindcom---interview-full-stack-web-developer)
    - [1st Round](#1st-round-1)
    - [2nd Round](#2nd-round-1)
    - [Coding Test](#coding-test-1)
  - [IV) Capgemini - Interview VueJs Developer](#iv-capgemini---interview-vuejs-developer)
    - [1st Round](#1st-round-2)
    - [2nd Round](#2nd-round-2)
  - [V) Riktamtech](#v-riktamtech)
  - [VI) PWC](#vi-pwc)
    - [Preparation](#preparation)
    - [Additional Questions](#additional-questions)
  - [NodeJS Interview: Code Examples](#nodejs-interview-code-examples)
    - [Database Design](#database-design)
    - [Create a promise response true if resolved and false if rejected. Achieve the same with async and await](#create-a-promise-response-true-if-resolved-and-false-if-rejected-achieve-the-same-with-async-and-await)
    - [What do you use for the authentication purpose?](#what-do-you-use-for-the-authentication-purpose)
    - [Create a POST API](#create-a-post-api)
    - [What is middleware? Why we used](#what-is-middleware-why-we-used)
    - [Call, bind and apply](#call-bind-and-apply)
    - [What is closure](#what-is-closure)
    - [Function Currying](#function-currying)
    - [Rest Operator, Rest parameter, Spread Operator](#rest-operator-rest-parameter-spread-operator)
      - [Rest Parameter](#rest-parameter)
      - [Spread Operator](#spread-operator)
    - [Var, let and const](#var-let-and-const)
    - [The unit test case write](#the-unit-test-case-write)
    - [Arrow function and its advantages](#arrow-function-and-its-advantages)
    - [3) get / post/put / patch](#3-get--postput--patch)
    - [14) return third highest value and third lowest element in an array with out using array index](#14-return-third-highest-value-and-third-lowest-element-in-an-array-with-out-using-array-index)


---

## LTIMindtree: Interview - NodeJS Developer

### 1st Round  
**Date:** 23/03/23

#### What is Node.js?
Node.js is the JavaScript runtime environment that is based on Google’s V8 Engine i.e. with the help of Node.js we can run the JavaScript outside of the browser. Other things that you may or may not have read about Node.js is that it is single-threaded, based on event-driven architecture, and non-blocking based on the I/O model.

Node.js application runs only on a single thread and by that, It means whether that Node.js application is being used by 5 users or 5 million users, it will only run on a single thread which makes the Node.js application blockable (which means that a single line of code can block the whole app because an only single thread is being used). So, to keep the Node.js application running, asynchronous code must be used everywhere having callback functions because as we know that asynchronous code keeps on running in the background and the callback gets executed as soon as the promise gets resolved rather than synchronous code which blocks the whole application until it gets finished executing. But, we can still use synchronous code however at some place in our application and that place is before our application enters Event-loop. Event-loop is what allows Node.js applications to run non-blocking asynchronous I/O-based operations i.e, all the asynchronous code is managed and executed within the event-loop and before that, we can use our synchronous code which is in this case known as Top-Level code.

#### What is callback hell?
Callback Hell is essentially nested callbacks stacked below one another forming a pyramid structure. Every callback depends on/waits for the previous callback, thereby making a pyramid structure that affects the readability and maintainability of the code.

```js
setTimeout(()=> {
    console.log('Hello');
    setTimeout(()=> {
        console.log('World')
    }, 1000)
}, 1000)
```

#### What is Promise.all()?
The method returns a single Promise after receiving one or more promises as input. When all of the Promises in the input are satisfied, the returning promise is fulfilled. When any of the inputs, or promises are refused, it rejects a promise with this first rejection reason.

```js
Promise.all([promise_1 , promise_2,  ...]).then(
    // do something...
)
```

#### Difference between array.forEach() and array.map
- `Array.forEach()` method is used to iterate over an array.
- The `Array.map()` method is used to iterate over an array. In each iteration, it applies a callback function on the current array element and manipulates the value of elements. and finally returns a completely new array.

```js
const numbers = [1,2,3,4,5];
const mappedNums = numbers.map(num=> num*2); // [2,4,6,8,10]
```

#### How do I choose node_modules?
**Factors:**
- Number of downloads
- How recently updated
- History of updates (has it been updated often over a long period of time)
- Number of contributors
- Have well-known/trusted developers and maintainers started it? [a]
- Do other important packages depend on it? [b]
- Is the package well-documented and has its own website?
- Does the module have test coverage?
- Github factors: updated: As of npm 1.2.20 and forward, modules without repository fields will show missing repository fields warning. (Nice touch to put a little pressure on people to package up their modules correctly.)
- Number of forks
- Number of commits
- Are issues being closed on GitHub, or have the same issues been open for a long time?

#### How do you secure the API?
- **Use throttling and rate-limiting:**  
  Throttling involves setting a temporary state that allows the API to evaluate every request and is often used as an anti-spam measure or to prevent abuse or denial-of-service attacks. There are two primary considerations when implementing the throttling feature: how much data should be allowed per user, and when should the limit be enforced?  
  On the other hand, rate-limiting helps administer REST API security by avoiding DoS and Brute force attacks. In some APIs, developers set soft limits, which allow clients to exceed request limits for a brief duration. Setting timeouts is one of the most straightforward API security best practices, as it can handle both synchronous and asynchronous requests.

##### Express Slow Down & Rate Limit

```js
// Allow 100 requests in 15 mins. After that add 500 ms delay in each request
// 101 will be delayed by 500 ms
// 102 will be delayed by 1000 ms
const speedLimiter = {
    windowMs: 15* 60 * 1000,
    delayAfter: 100,
    delayMs: 500
};
app.use(speedLimiter);

// Limit each IP to 100 requests per 15 mins
const rateLimiter = {
    windowMs: 15 * 60 * 1000,
    max: 100
}
app.use(rateLimiter);
```

##### JWT Authorization

```js
const jwt = require('jsonwebtoken');

const payload = {
    id,
    f_name,
    email
}
const token = jwt.sign(payload, JWT_SECRET, {
    expiresIn: JWT_TTL
});

jwt.verify(payload, JWT_SECRET, (err, decoded)=> {
    if(!err){
        return decoded
    }
})
```

##### Use HTTPS/TLS for REST APIs
HTTPS and Transport Layer Security (TLS) offer a secured protocol to transfer encrypted data between web browsers and servers. Apart from other forms of information, HTTPS also helps to protect authentication credentials in transit. As one of the most critical practices, every API should implement HTTPS for integrity, confidentiality, and authenticity. In addition, security teams should consider using mutually authenticated client-side certificates that provide extra protection for sensitive data and services. When building a secure REST API, developers should avoid redirecting HTTP to HTTPS, which may break API client security. Adequate steps should also be taken to divert Cross-Origin Resource Sharing (CORS) and JSONP requests for their fundamental vulnerabilities for cross-domain calls.

#### What is the closure?

---

### Coding Test

**Q1. Find the nth max elements from an array.**

```js
const getNthMax = function(arr, n) {
    // Sort the array in descending order
    arr = arr.sort((a,b)=> b-a);
    // Remove the duplicates
    arr = [...new Set(arr)];
    return arr[n-1];
}

console.log(getNthMax([100, 200, 200, 300, 400], 4));   // 100
```

---

### 2nd Round  
**Date:** 11/04/23

1. What are you currently working on?
2. Difference between Postgres and MySQL
3. How do you build authentication apis?
4. How do you create jwt token?
5. What value did you set for ttl?
6. How do you optimize the database?
7. How to run unit testing

---

## II) ESKO: Interview - NodeJS Developer

**Date:** 30/03/23

- Explain async await and why we use it.
- Write a Promise
- How do you make deployment?
- Did you work on the typescript?

---

## III) Engineersmind.com - Interview (Full Stack Web Developer)

### 1st Round  
**Date:** 30/03/23

- Event handling in vuejs
- Between vue and react what you’ll choose and why?
- What is store procedure? Why do we use it?
- Why do we use callback?
- How to track any change in a file?
- Transaction statements and why we use them?
- What is the difference between left join and inner join?
- If jwt expires then without redirecting the user to login how can you regenerate?
- Pipe method in node?
- What is the difference between set timeout and set interval?

### 2nd Round  
**Date:** 04/04/2023

- Difference between api and endpoint
- What is blocking in odeNodeJS?
- NodeJS REPL?
- What is callback hell? How do we overcome this?
- What is an event loop in NodeJS?
- What is an event emitter?
- What is a stream? Types of the stream?
- What is a buffer?
- VueJS lifecycle hooks?
- Difference between v-if and v-show
- What is chaining in NodeJS?

---

### Coding Test

**Q1. Write code in logic form and convert number to 2 significant digits**  
```
0.00003456 = 0.000034  
0.003123 = 0.0031  
0.1232 = 0.12  
```

**Q2. What is the output of below code?**
```js
var X = { Foo : 1};
var Output = (function()
{
delete X.foo;
return X.foo;
}
)();
console.log(Output); // undefined
```

**Q3. What is the output of below code?**
```js
var y = 1;
if (function f() {}) {
    y += typeof f;
}
console.log(y);  // 1undefined
```

**Q4. What is the output of below code?**
```js
var output = (function(x) {
    delete x;
    return x;
})(0);

console.log(output); // 0
```

---

## IV) Capgemini - Interview VueJs Developer

### 1st Round

- What is event bubbling and event capturing
- Es6 concepts
- Right a Class in javascript
- Check palindrome
- What is event looping
- V-if and v-show and v-once
- What are lifecycle hooks
- Usage of vuex

### 2nd Round

- What is hoisting
- What will be the output of the below code?

```js
function test() {
    console.log(a);     // undefined
    console.log(foo()); // 2
   
    var a = 1;
    function foo() {
       return 2;
    }
 }
 
 test();
```

- Write a Promise
- How do you write unit testing in vue?
- How do you make a page responsive with CSS property?
- Bootstrap
- What is closure?
- Suppose you have a function that returns the sum of two numbers how you’ll write unit testing?
- How do you deploy projects in AWS?
- Learn about Vue3
- Vuex and all its methods
- Waterfall, Agile and Scrum
- What is CI (Continuous Integration)
- Lifecycle hooks
- Difference between angular, vuejs and react
- What is the use of iframe?

---

## V) Riktamtech

- The challenging task you do in your project
- How you manage the traffic of the user in the trading platform
- Algorithm to find the largest palindrome in a string
- Which ORM do you use?
- Difference between josn and jsonb
- You have two table order and product. Find the 

---

## VI) PWC

- What is "Decorators" in TypeScript?  
  [https://github.com/aershov24/typescript-interview-questions#q14-what-is-decorators-in-typescript-](https://github.com/aershov24/typescript-interview-questions#q14-what-is-decorators-in-typescript-)
- keyof typeof  
  [https://stackoverflow.com/questions/55377365/what-does-keyof-typeof-mean-in-typescript](https://stackoverflow.com/questions/55377365/what-does-keyof-typeof-mean-in-typescript)
- Which architecture do you work with? Monolithic or Microservices. Explain the communication between microservices. Suppose you have a notification service how you call it
- Kafka messaging service
- Database transactions 
- What is closure?
- How NodeJs works?
- `[‘kolkata’, ‘Kolkata’, ‘Delhi’]` find the occurrence of the city?  
  //output {kolkata: 2, Delhi: 1}
- Unit testing
- Write a program to explain class in typescript
- What is promise.all()?
- Difference between authorization and authentication

### Preparation

- Create a node server?
- ES6 
- What is middleware?
- Why do we use express.js on top of the nodejs?
- Error handling in NodeJS
- Coding test related to setTimeout
- How does Node work behind the scene?
- Call, apply and bind
- Difference between REST API and SOAP API
- Different HTTP methods and their usages

---

### Additional Questions

1. Child process
2. Put and patch 
3. Options Methos In REST
4. Use of OPTIONS
5. CORS
6. How to connect to DB
7. Connect Node to Postgresql which package?
8. Node js security
9. How to make things Fast Like api Call?
10. SQL question ( Sex  conversion )

---

## NodeJS Interview: Code Examples

### Database Design
- Have you ever database design schema for any project - Normalization etc?
- SQL and NoSQL
- Query optimizing tool

### Create a promise response true if resolved and false if rejected. Achieve the same with async and await

```js
const getPromise1 = (flag)=> {
    return new Promise((resolve, reject)=> {
        if(flag){
            resolve(true)
        }else{
            const error = new Error(false);
            reject(error)
        }
    })
}

getPromise1(false).then(data=> console.log(data)).catch(e=> console.log(e))

// Using async/await
const getPromise2 = async (flag)=> {
    if(flag){
        return true
    }else{
        throw new Error(false)
    }
}

(async ()=> {
    try{
        let data = await getPromise2(false);
        console.log(data)
    }catch(e){
        console.log(e)
    }
})();
```

---

### What do you use for the authentication purpose?

```js
const jwt = require('jsonwebtoken');

// For Creating the token
const payload = {
    id,
    f_name,
    l_name,
    email
}
const token = jwt.sign(payload, JWT_SECRET, {
    expiresIn: JWT_TTL
});

// For verification
jwt.verify(payload, JWT_SECRET, (err, decoded)=> {
    if(!err){
        console.log(decoded);
    }
})
```

---

### Create a POST API

```js
const express = require('express');
const app = express();

app.use(express.json());

app.post('/', (req, res)=> {
    console.log(req.body);
    res.send('Success')
});

app.listen(3001, ()=> {
    console.log('Server running at port 3001')
})
```

---

### What is middleware? Why we used

---

### Call, bind and apply

The following are the methods in the function prototype chain:
- `Function.prototype.apply()`
- `Function.prototype.bind()`
- `Function.prototype.call()`

- The `apply()` method is an important method of the function prototype and is used to call other functions with a provided this keyword value and arguments provided in the form of an array or an array-like object.
- The `call()` method is used to call a function with a given this and arguments provided to it individually. This is very similar to apply, the only difference being that apply takes arguments in the form of an array or array-like objects, and here the arguments are provided individually.
- The `bind()` method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called. The bind function is much like the call function, with the main difference being that bind returns a new function whereas call does not.

---

### What is closure

A function along with its lexical scope bundled together form a closure. The function defined in the closure remembers the environment in which its created.

```js
function getSecret(){
    const secret = 7;
    return ()=> {
        return secret;
    }
};

const secretGetter = getSecret();
console.log(secretGetter());
```

---

### Function Currying

```js
function createBase(base){
    return (numberInput)=> {
        return numberInput + base
    }
}

var addSix = createBase(6);
console.log(addSix(10)); // returns 16
console.log(addSix(21)); // returns 27
```

---

### Rest Operator, Rest parameter, Spread Operator

- The rest parameter syntax allows us to represent an indefinite number of arguments as an array. With the help of a rest parameter, a function can be called with any number of arguments.
- The rest operator is used to put the rest of some specific user-supplied values into a JavaScript array.
- The spread operator (`...`) helps you expand iterable into individual elements.

#### Rest Parameter

```js
function add(...nums) {
    let sum = 0;
    for (let num of nums){
        sum+= num
    };
    return sum;
}

console.log(add(1,2,3,4,5)) // 15
```

#### Spread Operator

```js
const person = {
    f_name: 'Surajit',
    l_name: 'Malik',
    age: 29
}

// Spread Operator
const another_person = {...person, f_name: 'Abir'};
console.log(another_person);

// Rest operator
const {f_name, ...rest} = person;
console.log(f_name);
console.log(rest);
```

---

### Var, let and const

- **Scope of Var:**  
  Before the advent of ES6, var declarations ruled. There are issues associated with variables declared with var. Scope essentially means where these variables are available for use. var declarations are globally scoped or function/locally scoped. The scope is global when a var variable is declared outside a function. This means that any variable that is declared with var outside a function block is available for use in the whole window.var is a function scoped when it is declared within a function. This means that it is available and can be accessed only within that function.
- var variables can be re-declared and updated
- Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. So var variables are hoisted to the top of their scope and initialized with a value of undefined.
- **Let and Const are block scoped:**  
  A block is a chunk of code bounded by `{}`. A block lives in curly braces. Anything within curly braces is a block. So a variable declared in a block with let  is only available for use within that block.
- let can be updated but not re-declared
- Just like var,  a variable declared with let can be updated within its scope. Unlike var, a let variable cannot be re-declared within its scope.
- **Hoisting of let and const:**  
  Just like var, let & const declarations are hoisted to the top. Unlike var which is initialized as undefined, the let and const keyword is not initialized. So if you try to use a let variable before the declaration, you'll get a Reference Error.
- const cannot be updated or re-declared  
  This means that the value of a variable declared with const remains the same within its scope. It cannot be updated or re-declared. So if we declare a variable with a const

---

### The unit test case write

- `describe()` and `it()`
- The `it()` call identifies each individual test but by itself, it does not tell Mocha anything about how your test suite is structured. How you use the `describe()` call is what gives structure to your test suite.

```js
const expect = require('chai').expect;

describe('Simple example', ()=> {
    before(()=> {
        console.log('Execute before all the tests\n')
    })

    beforeEach(()=> {
        console.log('execute before each test')
    })

    it('get 4 by adding 2 + 2', ()=> {
        expect(2+2).equal(4);
    });

    it('Check boolean', ()=> {
        expect(2 === 2).to.be.true;
    })

    it('Checking string length', ()=> {
        expect('Foo').lengthOf(3);
    })

    it('check object property', ()=> {
        const a = {
            b: 10
        }
        expect(a).to.have.property('b');
    })

    after(()=> {
        console.log('Execute after all the tests')
    })

    afterEach(()=> {
        console.log('execute after each test\n')
    })
})
```

---

### Arrow function and its advantages

It is a new feature introduced in ES6 that is a more concise syntax for writing function expressions. It allows you to create functions more cleanly compared to regular functions. There is no declaration approach here, we can write by using Function expressions only.

There are certain differences between Arrow and Regular function, i.e

- **Syntax**
- **No arguments (arguments are array-like objects)**

```js
function findMaxNum(){
    return Math.max(...arguments);
}

console.log(findMaxNum.prototype) // { constructor: f }

console.log(findMaxNum(1,2,3));

const findMaxNum2 = (...args)=> {
    console.log(Math.max(...arguments)); // NaN
    return Math.max(...args);
};
console.log(findMaxNum2.prototype) // undefined

console.log(findMaxNum2(1,2));
```

- No prototype object for the Arrow function
- Cannot be invoked with a new keyword (Not a constructor function)
- No own this (call, apply & bind won't work as expected)
- In a traditional function, its internal this value is dynamic, it depends on how the function is invoked
- If we access this in the arrow function it will return the this of the closest non-arrow parent function.

```js
const user =  {
    name: 'Surajit',
    getUsername: function() {
        return this.name
    }
}
console.log(user.getUsername()); // Surajit

const user2 =  {
    name: 'Surajit',
    getUsername: () => {
        return this.name
    }
}
console.log(user2.getUsername()); // undefined
```

- It cannot be used as a Generator function
- Duplicate-named parameters are not allowed

---

### 3) get / post/put / patch  
### 14) return third highest value and third lowest element in an array with out using array index

```js
function getThirdMaxMin(arr){
    let sortedArrDesc = arr.sort((a,b)=> b-a);
    sortedArrDesc = [...new Set(sortedArrDesc)];
    console.log(sortedArrDesc)
    const thirdHighest = sortedArrDesc.length > 3 ? sortedArrDesc[2] : null;
    const thirdLowest= sortedArrDesc.length > 3 ? sortedArrDesc[sortedArrDesc.length - 3] : null;
    return {
        thirdHighest,
        thirdLowest
    }
}
console.log(getThirdMaxMin([3,4,4,1,2,19,11, 50]));
```
