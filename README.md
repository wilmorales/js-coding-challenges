# Array Chunking

Write a function to flatten a nested array. You must account for varying levels of nesting.

Example

```
flattenArray([1, [2, [3, 4], [[5]]]]); // [1, 2, 3, 4, 5]
```

# Evaluation

## Junior Developer Perspective

A junior developer might use a straightforward recursive approach without considering all edge cases or optimizing for performance.

- Correctness: The solution correctly flattens nested arrays.
- Code Readability and Style: The code is readable and follows basic JavaScript conventions.
- Efficiency: The recursive approach works but might not be optimized for deeply nested arrays.
- Use of Language Features: Uses basic JavaScript features like recursion, Array.isArray, and concat.
- Error Handling: No explicit error handling or edge case consideration.
- Code Structure: Simple and straightforward, but may struggle with very large or deeply nested arrays.

```
function flattenArray(arr) {
  let result = [];

  for (let element of arr) {
    if (Array.isArray(element)) {
      result = result.concat(flattenArray(element));
    } else {
      result.push(element);
    }
  }

  return result;
}

// Basic test case
console.log(flattenArray([1, [2, [3, 4], [[5]]]])); // [1, 2, 3, 4, 5]

```

## Senior Developer Considerations

A senior developer would enhance the function by considering performance optimizations, adding error handling, and using modern JavaScript features. Additionally, they might add documentation and tests.

- Correctness: The solution correctly flattens nested arrays and handles a variety of inputs.
- Code Readability and Style: The code is readable, well-documented, and follows good JavaScript practices.
- Efficiency: The use of a stack and iterative approach avoids the potential pitfalls of deep recursion (stack overflow), making it more efficient for deeply nested arrays.
- Use of Language Features: Uses modern JavaScript features like the spread operator and array methods effectively.
- Error Handling: Includes type checking and throws meaningful errors for invalid input.
- Code Structure: Modular and reusable, with clear separation of concerns and robust error handling.

Here’s how a senior developer might enhance the solution:

```

/**
 * Flattens a nested array.
 *
 * @param {Array} arr - The input nested array.
 * @returns {Array} - The flattened array.
 * @throws {TypeError} - Throws an error if the input is not an array.
 */
function flattenArray(arr) {
  if (!Array.isArray(arr)) {
    throw new TypeError('Input must be an array');
  }

  const result = [];
  const stack = [...arr];

  while (stack.length) {
    const next = stack.pop();

    if (Array.isArray(next)) {
      stack.push(...next);
    } else {
      result.push(next);
    }
  }

  return result.reverse();
}

// Test cases
console.log(flattenArray([1, [2, [3, 4], [[5]]]])); // [1, 2, 3, 4, 5]
console.log(flattenArray([])); // []
console.log(flattenArray([1, 2, 3])); // [1, 2, 3]
console.log(flattenArray([1, [2, [3, 4, [5, [6, 7]]]]])); // [1, 2, 3, 4, 5, 6, 7]
try {
  console.log(flattenArray(123)); // Throws error
} catch (e) {
  console.error(e.message); // "Input must be an array"
}


```
