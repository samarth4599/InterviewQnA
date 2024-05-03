# Javascript Interview Questions

## What are Promises in JS?

In JavaScript, promises are objects used for asynchronous programming. They represent the eventual completion (or failure) of an asynchronous operation and allow you to handle the result once it's available, whether it's a success or an error.

Promises have three states:

Pending: Initial state, neither fulfilled nor rejected.
Fulfilled: The operation completed successfully.
Rejected: The operation failed.

You create a promise using the new Promise() constructor, passing a function with two arguments: resolve and reject. Inside this function, you perform your asynchronous task. When the task completes successfully, you call resolve() with the result. If an error occurs, you call reject() with an error object.

Here's a simple example:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Perform some asynchronous operation, like fetching data
  setTimeout(() => {
    const data = "This is the result";
    // Simulate success
    resolve(data);
    // Simulate failure
    // reject(new Error('Something went wrong'));
  }, 2000);
});

// Consuming the promise using .then() and .catch()
myPromise
  .then((result) => {
    console.log("Success:", result);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

Promises provide a more structured way to handle asynchronous code compared to callbacks, making code easier to read and maintain. Additionally, they support chaining using the .then() method, allowing you to perform multiple asynchronous operations sequentially.

## What is Callback Hell?

Callback hell, also known as "Pyramid of Doom," is a situation that arises in asynchronous JavaScript programming when you have multiple nested callbacks within callbacks, making the code difficult to read, understand, and maintain. This typically occurs when dealing with asynchronous operations such as fetching data from a server, reading files, or handling user input.

Here's an example of callback hell:

```javascript
asyncFunction1(arg1, function (err, result1) {
  if (err) {
    handleError(err);
  } else {
    asyncFunction2(result1, function (err, result2) {
      if (err) {
        handleError(err);
      } else {
        asyncFunction3(result2, function (err, result3) {
          if (err) {
            handleError(err);
          } else {
            // Do something with result3
          }
        });
      }
    });
  }
});
```

Callback hell can lead to several issues:

Readability: Nested callbacks make the code difficult to read and understand, especially for developers who are not familiar with the codebase.
Error handling: Error handling becomes cumbersome, as you need to handle errors at each level of nesting, leading to repetitive code and potential for errors to be missed.
Debugging: Debugging becomes challenging, as it's harder to trace the flow of execution through nested callbacks.
Maintainability: Code that is difficult to read and understand is also harder to maintain and update, increasing the likelihood of introducing bugs.

To avoid callback hell, you can use techniques such as promises, async/await to organize asynchronous code in a more readable and maintainable way.

## What are Closures?

A closure is created when a function is defined within another function (the outer function) and has access to the outer function's variables. Even after the outer function has finished executing, the inner function maintains a reference to the variables of the outer function, keeping them "alive" within its scope. This enables the inner function to access and manipulate those variables, even though they are technically out of scope.

Here's a simple example:

```javascript
function outerFunction() {
  let outerVariable = "I am from the outer function";

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

const closure = outerFunction();
closure(); // Output: I am from the outer function
```

Closures are powerful because they allow for:

Encapsulation: The inner function can access variables from the outer function's scope, but those variables are not accessible from outside, providing a level of encapsulation and data privacy.
Data Persistence: Variables in the outer function's scope are "captured" by the inner function and remain available for use even after the outer function has completed execution.
Callbacks: Closures are commonly used to create callbacks and maintain state in event-driven programming, such as handling asynchronous operations or responding to user interactions.
