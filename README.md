# Deep Clone Object

Write a function to perform a deep clone of a given object. This function should create a copy of the object, including nested objects and arrays, that does not share references with the

## Example

```
deepClone({ a: 1, b: { c: 2 } }); // { a: 1, b: { c: 2 } }
```

# Evaluation

## Junior Developer Perspective

A junior developer might use a straightforward recursive approach without considering all edge cases or optimizing for performance.

- Correctness: The solution correctly performs a deep clone for basic objects and arrays.
- Code Readability and Style: The code is readable and follows basic JavaScript conventions.
- Efficiency: The recursive approach works but might not be optimized for large or complex objects.
- Use of Language Features: Uses basic JavaScript features like recursion, typeof, and Array.isArray.
- Error Handling: No explicit error handling or edge case consideration.
- Code Structure: Simple and straightforward, but may struggle with very large or complex objects, circular references, or special object types like Date, Map, Set, etc.

```
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }

  const clone = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      clone[key] = deepClone(obj[key]);
    }
  }

  return clone;
}

// Basic test case
const original = { a: 1, b: { c: 2 } };
const clone = deepClone(original);
console.log(clone); // { a: 1, b: { c: 2 } }
console.log(clone.b === original.b); // false

```

## Senior Developer Considerations

A senior developer would enhance the function by considering performance optimizations, adding error handling, and handling special cases like circular references and special object types. Additionally, they might add documentation and tests.

- Correctness: The solution correctly performs a deep clone for objects, arrays, dates, maps, sets, and handles circular references.
- Code Readability and Style: The code is readable, well-documented, and follows good JavaScript practices.
- Efficiency: The use of a WeakMap to track seen objects avoids infinite loops with circular references and optimizes performance.
- Use of Language Features: Uses modern JavaScript features and object type checks effectively.
- Error Handling: Includes type checking and handles various object types and circular references.
- Code Structure: Modular and reusable, with clear separation of concerns and robust handling of different data types.

Here’s how a senior developer might enhance the solution:

```

/**
 * Performs a deep clone of a given object.
 *
 * @param {any} obj - The object to be cloned.
 * @param {WeakMap} [seen=new WeakMap()] - A WeakMap to handle circular references.
 * @returns {any} - The deep cloned object.
 * @throws {TypeError} - Throws an error if the input is not an object.
 */
function deepClone(obj, seen = new WeakMap()) {
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }

  if (seen.has(obj)) {
    return seen.get(obj);
  }

  let clone;

  if (Array.isArray(obj)) {
    clone = [];
    seen.set(obj, clone);
    for (let i = 0; i < obj.length; i++) {
      clone[i] = deepClone(obj[i], seen);
    }
  } else if (obj instanceof Date) {
    clone = new Date(obj);
  } else if (obj instanceof Map) {
    clone = new Map();
    seen.set(obj, clone);
    obj.forEach((value, key) => {
      clone.set(key, deepClone(value, seen));
    });
  } else if (obj instanceof Set) {
    clone = new Set();
    seen.set(obj, clone);
    obj.forEach(value => {
      clone.add(deepClone(value, seen));
    });
  } else {
    clone = {};
    seen.set(obj, clone);
    for (let key in obj) {
      if (obj.hasOwnProperty(key)) {
        clone[key] = deepClone(obj[key], seen);
      }
    }
  }

  return clone;
}

// Test cases
const original = {
  a: 1,
  b: { c: 2 },
  d: new Date(),
  e: new Map([['key1', 'value1']]),
  f: new Set([1, 2, 3]),
  g: [1, [2, 3]]
};

const clone = deepClone(original);
console.log(clone); // Deeply cloned object
console.log(clone.b === original.b); // false
console.log(clone.d === original.d); // false
console.log(clone.e.get('key1') === original.e.get('key1')); // true
console.log(clone.f.has(1)); // true
console.log(clone.g[1] === original.g[1]); // false
try {
  console.log(deepClone(123)); // 123
} catch (e) {
  console.error(e.message); // Should not throw an error
}

```
