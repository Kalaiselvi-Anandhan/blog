---
title: Promises On Async / Await
author: Kalaiselvi Anandhan
date: 2020-08-24
hero: ./images/async-await-javascript.jpg
slug: promises-on-async-await
excerpt: Explore more about Promises on Async / Await 
---

# THE BASICS OF ASYNC / AWAIT

Async / Await hailed as an easiest way to use [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). It act as a syntactic sugar on top of promises, making asynchronous code easier to write and to read.

## THE ASYNC KEYWORD

The async keyword before the function declaration tells the JavaScript engine that the function is [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function). An async function is a function that knows how to expect the possibility of the await keyword being used to invoke asynchronous code.

Lets look at the below example,

``` Javascript
let hello = function(){
    return "Hello"
}

let asyncHello = async function(){
    return "Hello"
}

console.log(hello(),asyncHello()) // Hello Promise { 'Hello' }
```

The hello function returns the string but the asyncHello function itself returns a promise because the async keyword is added to functions to tell them to return a promise rather than directly returning the value. This exhibits that async functions return the values that are guaranteed to be converted to promises.

## THE AWAIT KEYWORD

The await keyword is used in front of any async promise-based function to pause your code on that line until the promise to get resolved or rejected and then it returns the value or throws the error of that Promise.

Lets consider the below example,

``` JavaScript
let asyncHello = async function()
{
    let result = await Promise.resolve("Hello")
    console.log(result) // Hello
}
asyncHello()
```

It illustrates that the await expression will return the resolved value of the Promise and we store the value into a variable.

**Note :  The await keyword is only valid inside async functions. If you use it outside of an async function's body, you will get a Syntax Error.**

# PROMISES WORK WITH ASYNC / AWAIT 

Async / Await is built on top of promises, so it's compatible with all the features offered by promises. Promises work with Async / Await in two different ways,

1. Sequential
2. Parallel

Lets consider the function that returns Promise,

``` JavaScript
function resolveAfter1Second(x) {
    return new Promise((resolve,reject) => {
        setTimeout(() => {
           resolve(x)
        }, 1000)
    })
}
```

:point_right: **Sequential Execution**

In the following example, we successively achieve Sequential Execution by awaiting the Promise. Inside the Async function the first await would look for the Promise that has either been fulfilled or rejected and then the await expression return value or throw an error. After completion of first await, the next await proceed the same process.

```JavaScript
(async function() { 
    try{
        console.time("sequential execution")
        let a = await resolveAfter1Second(2)
        let b = await resolveAfter1Second(3)
        let sum = a + b
        console.log(sum) // 5
        console.timeEnd("sequential execution") //sequential execution: 2s
    }
    catch(error){
        console.log(error)
    }
})();
```

For summing up of two values it takes two seconds because the execution suspends 1 second for the first await, and then another 1 second for the second await. The second timer is not created until the first has already fired, so the code finishes after 2 seconds.

:point_right: **Parallel Execution**

To safely perform two or more tasks in parallel, you must await a call to [Promise.all()]() method. Promise.all will take an array of promises, and compose them all into a single promise, which resolves only when every input promise in the array has resolved itself. 

Consider the below example, 

```JavaScript
(async function() { 
    try{
        console.time("parallel execution")
        let [a,b] = await Promise.all([resolveAfter1Second(2),resolveAfter1Second(3)])
        let sum =a+b;
        console.log(sum); //5
        console.timeEnd("parallel execution") //parallel execution: 1s
    }
    catch(error){
        console.log(error)
    }
})()
```

By using a single await we are able to get all the resolved values of the Promises. For summing up of two values it takes only 1 second because the Promises gets executed in parallel.

Here is another way to do things in parallel with async/await though it is not recommended, 

```JavaScript
(async function() { 
    try{
        console.time("sequential execution")
        let a = resolveAfter1Second(2)
        let b = resolveAfter1Second(3)
        let sum = await a + await b;
        console.log(sum) // 5
        console.timeEnd("sequential execution") //sequential execution: 1s
    }
    catch(error){
        console.log(error)
    }
})();
```

In the above example we have dispatched both Promises (the timer gets started...) before we await anything so they run concurrently, which means the code runs in 1 second. At the time we begin awaiting, it's too late to delay either of them and they just return the resolved values of the respective promises stored in the variables.

# WHY PROMISES ON ASYNC / AWAIT 

:pushpin: **Concise and Clean**

We don't want to use .then and the anonymous function that handles response or data. Here where the await plays a vital role to handle the fulfillment and rejection of Promise with a single keyword.

```JavaScript
const add = (a,b) => new Promise((resolve,reject)=>{
    (a<0 || b<0) ? reject("error") : resolve(a + b)
})

add(1,2)
.then((data)=>{
    return add(data,2)
})
.then((data)=>{
    console.log(data) // 5
})
.catch((error)=>{
    console.log("error")
});

async function sums(){
    try{
        let data = await add(1,2)
        let result = await add(data,2)
        console.log(result) // 5
    }
    catch(err){
        console.log(err)
    }
}
sums();
```

:pushpin: **Error Handling**

Error handling is simpler and it relies on try / catch just like any other synchronous code.

```JavaScript 
const add = (a,b) => new Promise((resolve,reject)=>{
    (a<0 || b<0) ? reject("error") : resolve(a + b)
})

async function sums(){
    try{
        let data = await add(1,2)
        let result = await add(data, -2)
        console.log(result)
    }
    catch(err){
        console.log(err) // error
    }
}
sums();
```

The await will throw an error only the promise gets rejected and the catch block will handle the thrown error.

:pushpin: **Flatten the Promise nesting**

By utilizing the await expression we can flatten the Promises nesting from a bit.

## REFERENCE

[MDN Async Await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)

[Async Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
