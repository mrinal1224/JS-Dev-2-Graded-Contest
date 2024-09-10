### Problem Statement

Write a function `invokeNTimes` that takes **three parameters**:

1. A function (`fn`),
2. An integer (`n`),
3. An array of arguments (`args`).

The function should return a **new function** that, when called, invokes the provided function `fn` exactly `n` times, using the arguments from the `args` array for each invocation. Each call to `fn` should pass the elements from the `args` array in order, starting from the first element again if the array runs out of values.

If `args` is an empty array, invoke the function `fn` without any arguments. The returned function should return an array containing the results of each invocation of `fn`.

### Problem Description

- You need to implement a function `invokeNTimes(fn, n, args)` that returns a new function.
- When the returned function is invoked, it should call the `fn` function **exactly** `n` times.
- The arguments for each call to `fn` should be taken from the `args` array. If the number of calls exceeds the length of the `args` array, wrap around and use the array elements again.
- If the `args` array is empty, invoke `fn` without any arguments.

### Example

```javascript
const add = (x, y) => x + y;
const invoke = invokeNTimes(add, 5, [1, 2]); 

console.log(invoke()); // Output: [3, 3, 3, 3, 3]
```

In this example, `add` is invoked 5 times with the arguments from the `args` array. Since `args = [1, 2]`, each call to `add` uses these values.

```javascript
const multiply = (x, y) => x * y;
const invoke = invokeNTimes(multiply, 4, [2, 3]);

console.log(invoke()); // Output: [6, 6, 6, 6]
```

In this example, `multiply` is invoked 4 times, with each call using the values from the `args` array.

### Hints

1. Use a loop inside the returned function to call `fn` multiple times.
2. To wrap around the arguments array, you can use the modulus operator to cycle through the array indices.
3. Return an array with the results of each invocation.

### Solution Approach

1. The `invokeNTimes` function takes the function `fn`, an integer `n`, and an array of arguments `args`.
2. Inside the returned function, we create a loop to call `fn` `n` times.
3. For each call, we determine which elements of the `args` array to use by cycling through it using the modulus operator.
4. We collect the results of each invocation and return them as an array.

### Test Cases

```javascript
// Test Case 1: Basic functionality with wrapping args
const add = (x, y) => x + y;
const invoke = invokeNTimes(add, 5, [1, 2]); 
console.log(invoke()); // Expected Output: [3, 3, 3, 3, 3]

// Test Case 2: More complex function
const multiply = (x, y) => x * y;
const invoke2 = invokeNTimes(multiply, 4, [2, 3]);
console.log(invoke2()); // Expected Output: [6, 6, 6, 6]

// Test Case 3: Empty args array
const log = () => "called";
const invoke3 = invokeNTimes(log, 3, []);
console.log(invoke3()); // Expected Output: ["called", "called", "called"]

// Test Case 4: Single argument, multiple invocations
const square = (x) => x * x;
const invoke4 = invokeNTimes(square, 3, [4]);
console.log(invoke4()); // Expected Output: [16, 16, 16]
```

### Code Stub

```javascript
function invokeNTimes(fn, n, args) {
    return function() {
        // Students will implement the solution here
    }
}
```

### Complete Solution

```javascript
function invokeNTimes(fn, n, args) {
    return function() {
        const result = [];
        for (let i = 0; i < n; i++) {
            if (args.length > 0) {
                result.push(fn(...args.slice(i % args.length, (i % args.length) + fn.length)));
            } else {
                result.push(fn());
            }
        }
        return result;
    };
}
```

