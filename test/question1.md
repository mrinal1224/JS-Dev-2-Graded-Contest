### Problem Statement:

**Title: Deep Clone with Modified Keys**

Write a function called `deepCloneWithModifications` that iterates through all keys of an object passed as an argument and creates a deep copy of the object. In the deep copy, the function should modify all string values by appending the word "_cloned" at the end of each string value, while keeping other types of values intact. The function should return this deep clone of the object.

**Requirements:**
1. The copy should be deep, meaning that changes to nested objects in the new object should not affect the original object.
2. For any string value in the object, append "_cloned" to the end of the string.
3. Non-string values such as numbers, booleans, or other objects should remain the same.

**Constraints:**
- The input object may have nested objects and arrays.
- The function should handle arrays and modify string elements inside them as well.

### Solution Approach:
- Use recursion to handle nested objects and arrays.
- For each key, check if the value is a string; if so, append "_cloned" to it.
- For objects and arrays, make recursive calls to handle nested elements.
- Use a helper function to perform the recursive deep cloning.

### Hints:
1. Use recursion to iterate over nested objects and arrays.
2. To check if a value is a string, use `typeof`.
3. You can use the `Array.isArray()` method to differentiate between arrays and objects.

### Test Cases:
```js
// Test Case 1: Basic object with string and number values
const obj1 = { name: "Alice", age: 25, city: "Wonderland" };
deepCloneWithModifications(obj1); 
// Expected Output: { name: "Alice_cloned", age: 25, city: "Wonderland_cloned" }

// Test Case 2: Object with nested objects
const obj2 = { 
    user: { name: "Bob", details: { city: "CityName", id: 101 } },
    active: true 
};
deepCloneWithModifications(obj2);
// Expected Output: { 
//   user: { name: "Bob_cloned", details: { city: "CityName_cloned", id: 101 } }, 
//   active: true 
// }

// Test Case 3: Object with arrays
const obj3 = { 
    items: ["apple", "banana", "carrot"], 
    count: 3 
};
deepCloneWithModifications(obj3);
// Expected Output: { items: ["apple_cloned", "banana_cloned", "carrot_cloned"], count: 3 }
```

### Code Stub:
```js
function deepCloneWithModifications(obj) {
    // Students should complete this function
}

// Example test cases for students to test their solution
const obj1 = { name: "Alice", age: 25, city: "Wonderland" };
console.log(deepCloneWithModifications(obj1));

const obj2 = { 
    user: { name: "Bob", details: { city: "CityName", id: 101 } },
    active: true 
};
console.log(deepCloneWithModifications(obj2));

const obj3 = { 
    items: ["apple", "banana", "carrot"], 
    count: 3 
};
console.log(deepCloneWithModifications(obj3));
```

### Complete Solution:
```js
function deepCloneWithModifications(obj) {
    if (Array.isArray(obj)) {
        return obj.map(item => deepCloneWithModifications(item));
    } else if (typeof obj === 'object' && obj !== null) {
        const clone = {};
        for (const key in obj) {
            if (typeof obj[key] === 'string') {
                clone[key] = obj[key] + '_cloned';
            } else {
                clone[key] = deepCloneWithModifications(obj[key]);
            }
        }
        return clone;
    }
    return obj;
}

// Test cases
const obj1 = { name: "Alice", age: 25, city: "Wonderland" };
console.log(deepCloneWithModifications(obj1));

const obj2 = { 
    user: { name: "Bob", details: { city: "CityName", id: 101 } },
    active: true 
};
console.log(deepCloneWithModifications(obj2));

const obj3 = { 
    items: ["apple", "banana", "carrot"], 
    count: 3 
};
console.log(deepCloneWithModifications(obj3));
```

In this modified version of the problem, the added complexity of appending "_cloned" to string values extends the difficulty slightly beyond a simple deep clone.