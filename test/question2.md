Extended Problem (Currying Example):


**Problem Description**

Create a new function `curry` that takes any function `fn` with two arguments and returns a curried version of that function. The curried version should allow calling the function `fn` with one argument at a time.

### Problem Description:

- Implement a function `curry` that takes a function `fn` as input.
- `fn` will have two parameters, and `curry` should return a new function that can be called with one argument at a time.

### Example:

```js
const add = (a, b) => a + b;
const curriedAdd = curry(add);

console.log(curriedAdd(2)(3)); // Output: 5
```

### Code Stub (For Students):

```js
function curry(fn) {
    // Return a curried version of the function `fn`
}
```

### Complete Solution:

```js
function curry(fn) {
    return function(a) {
        return function(b) {
            return fn(a, b);
        };
    };
}

// Example usage
const add = (a, b) => a + b;
const curriedAdd = curry(add);
console.log(curriedAdd(2)(3)); // Output: 5
console.log(curriedAdd(10)(20)); // Output: 30
```

### Test Cases:

```js
// Test Case 1: Adding using curried function
const add = (a, b) => a + b;
const curriedAdd = curry(add);
console.log(curriedAdd(3)(4));  // Expected Output: 7

// Test Case 2: Multiplying using curried function
const multiply = (a, b) => a * b;
const curriedMultiply = curry(multiply);
console.log(curriedMultiply(5)(6));  // Expected Output: 30
```