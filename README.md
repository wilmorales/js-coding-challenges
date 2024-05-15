# Find the Longest Word

Write a function that finds the longest word in a given string.

Example

```
findLongestWord("The quick brown fox jumps over the lazy dog") // "quick"
```

# Evaluation

## Junior Developer Perspective

A junior developer might focus on getting the correct result with a straightforward approach, potentially without considering edge cases or optimization.

- Correctness: The solution correctly identifies the longest word in the given string.
- Code Readability and Style: The code is readable and follows basic JavaScript conventions.
- Efficiency: The solution is efficient for typical inputs, iterating through the words once.
- Use of Language Features: Uses basic JavaScript features like split and for...of.
- Error Handling: No explicit error handling or edge case consideration.
- Code Structure: Simple and straightforward, but not robust.

```
function findLongestWord(str) {
  const words = str.split(' ');
  let longestWord = '';

  for (let word of words) {
    if (word.length > longestWord.length) {
      longestWord = word;
    }
  }

  return longestWord;
}

// Basic test case
console.log(findLongestWord("The quick brown fox jumps over the lazy dog")); // "quick"

```

## Senior Developer Perspective

A senior developer would enhance the function by adding error handling, considering edge cases, and potentially using more concise or modern JavaScript syntax. Additionally, they might add documentation and tests.

- Correctness: The solution correctly identifies the longest word and handles edge cases like empty strings and strings with only numbers.
- Code Readability and Style: The code is readable and well-documented with JSDoc comments.
- Efficiency: The solution is efficient and performs similarly to the junior solution but with additional error handling.
- Use of Language Features: Uses split with a regex for robustness and for...of for iteration, demonstrating a good grasp of JavaScript.
- Error Handling: Includes type checking and throws meaningful errors for invalid input.
- Code Structure: Modular and reusable, with clear separation of concerns and robust error handling.

```

/**
 * Finds the longest word in a given string.
 *
 * @param {string} str - The input string.
 * @returns {string} - The longest word in the string.
 * @throws {TypeError} - Throws an error if the input is not a string.
 */
function findLongestWord(str) {
  if (typeof str !== 'string') {
    throw new TypeError('Input must be a string');
  }

  const words = str.split(/\s+/); // Split by one or more whitespace characters
  let longestWord = '';

  for (let word of words) {
    if (word.length > longestWord.length) {
      longestWord = word;
    }
  }

  return longestWord;
}

// Test cases
console.log(findLongestWord("The quick brown fox jumps over the lazy dog")); // "quick"
console.log(findLongestWord("")); // ""
console.log(findLongestWord("a abc ab")); // "abc"
console.log(findLongestWord("123 12345 12")); // "12345"
try {
  console.log(findLongestWord(123)); // Throws error
} catch (e) {
  console.error(e.message); // "Input must be a string"
}


```
