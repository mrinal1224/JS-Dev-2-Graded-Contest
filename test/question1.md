### Problem Statement

Write a function called `cloneObjectWithExclusion` that takes two parameters: an object and an array of keys to exclude. The function should return a deep copy of the object but exclude the properties whose keys are in the exclusion array. The deep clone should be created such that any changes made to the new object do not affect the original object.

- **Input:** 
  - An object `obj` (can have nested objects) 
  - An array `excludeKeys` which contains keys to be excluded from the cloned object.

- **Output:** 
  - A deep-cloned object with the specified keys excluded.

**Note:**
- The function should iterate through all properties of the object, including nested objects.
- Any key in `excludeKeys` should not appear in the cloned object.

### Hints
1. Use recursion to iterate through nested objects.
2. Handle arrays and objects separately since both may require cloning.
3. Check if a key exists in the `excludeKeys` array before copying it to the new object.
4. Use `typeof` to differentiate between primitive values and objects.

### Solution Approach

1. Create a helper function that recursively iterates through each property of the object.
2. If a property is an object, recursively call the function on that object.
3. If a property is in the `excludeKeys` array, skip it during the cloning process.
4. Ensure that arrays are also handled correctly by iterating through their elements.
5. Return the deep-cloned object.

### Examples

#### Example 1:
```js
Input:
const obj = { a: 1, b: { c: 2, d: 3 }, e: 4 };
const excludeKeys = ['b', 'e'];

Output:
{ a: 1 }

Explanation:
The properties `b` and `e` are excluded, and only `a` remains in the deep clone.
```

#### Example 2:
```js
Input:
const obj = { x: 10, y: { z: 20, w: 30 }, m: { n: 40 } };
const excludeKeys = ['y'];

Output:
{ x: 10, m: { n: 40 } }

Explanation:
The property `y` is excluded, and the rest of the object is deep-cloned.
```

### Code Stub

```js
function cloneObjectWithExclusion(obj, excludeKeys) {
    // Your code here
}
```

### Complete Solution

```js
function cloneObjectWithExclusion(obj, excludeKeys) {
    if (obj === null || typeof obj !== 'object') {
        return obj; // return if obj is a primitive
    }
  
    // Handle arrays separately
    if (Array.isArray(obj)) {
        return obj.map(item => cloneObjectWithExclusion(item, excludeKeys));
    }
  
    const newObj = {};
  
    for (const key in obj) {
        if (obj.hasOwnProperty(key) && !excludeKeys.includes(key)) {
            // Recursively clone if the property is an object
            newObj[key] = cloneObjectWithExclusion(obj[key], excludeKeys);
        }
    }
  
    return newObj;
}
```

### Test Cases

```js
// Test case 1
const obj1 = { a: 1, b: { c: 2, d: 3 }, e: 4 };
const exclude1 = ['b', 'e'];
console.log(cloneObjectWithExclusion(obj1, exclude1)); 
// Expected output: { a: 1 }

// Test case 2
const obj2 = { x: 10, y: { z: 20, w: 30 }, m: { n: 40 } };
const exclude2 = ['y'];
console.log(cloneObjectWithExclusion(obj2, exclude2)); 
// Expected output: { x: 10, m: { n: 40 } }

// Test case 3: Empty object
console.log(cloneObjectWithExclusion({}, [])); 
// Expected output: {}

// Test case 4: No exclusions
const obj3 = { a: 1, b: { c: 2 }, d: 4 };
console.log(cloneObjectWithExclusion(obj3, [])); 
// Expected output: { a: 1, b: { c: 2 }, d: 4 }
```

This version of the problem tests deep cloning while introducing the complexity of handling key exclusions, offering a twist on the original concept.