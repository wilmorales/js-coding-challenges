# Array Chunking

Write a function that splits an array into chunks of a specified size.

Example

```
chunkArray([1, 2, 3, 4, 5, 6, 7], 3) // [[1, 2, 3], [4, 5, 6], [7]]
```

# Evaluation

## Senior Developer Considerations

A senior developer might go beyond these basic solutions and consider additional aspects such as:

- Parameter Validation: Ensuring inputs are valid and handling edge cases more explicitly.
- Documentation: Including JSDoc comments or other forms of documentation.
- Modularity and Reusability: Making the function more robust and reusable.
- Performance Considerations: Considering the performance implications for very large arrays.

Here’s how a senior developer might enhance the solution:

```

/**
 * Splits an array into chunks of a specified size.
 *
 * @param {Array} array - The array to be chunked.
 * @param {number} size - The size of each chunk.
 * @returns {Array[]} - A new array containing the chunked arrays.
 * @throws {Error} - Throws an error if size is not a positive integer.
 */
function chunkArray(array, size) {
  if (!Array.isArray(array)) throw new TypeError('First argument must be an array');
  if (typeof size !== 'number' || size <= 0) throw new TypeError('Size must be a positive number');

  const chunked = [];
  for (let i = 0; i < array.length; i += size) {
    chunked.push(array.slice(i, i + size));
  }
  return chunked;
}

```

## Junior Developer Perspective

A junior developer is more likely to:

- Focus on getting the correct output without considering all edge cases.
- Use simpler and more straightforward constructs without extensive error handling or optimization.
- Potentially overlook edge cases or input validation.

```
function chunkArray(array, size) {
  const chunked = [];
  let index = 0;
  while (index < array.length) {
    chunked.push(array.slice(index, index + size));
    index += size;
  }
  return chunked;
}

// Basic test case
console.log(chunkArray([1, 2, 3, 4, 5, 6, 7], 3)); // [[1, 2, 3], [4, 5, 6], [7]]


```
