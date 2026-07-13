# Advanced JavaScript Activity: Answer Template

---

## Task 1: Data Structures & References

```javascript
const library = {
  name: "City Library",
  books: [
    { title: "1984", author: "George Orwell", isAvailable: true },
    { title: "Brave New World", author: "Aldous Huxley", isAvailable: true },
    { title: "Fahrenheit 451", author: "Ray Bradbury", isAvailable: false }
  ]
};

// 1. Create a shallow copy of the library object
const copiedLibrary = { ...library };

// 2. Change the isAvailable status of one book in the COPIED library
copiedLibrary.books[0].isAvailable = false;

// 3. Log both
console.log("Original Library:", library);
console.log("Copied Library:", copiedLibrary);

/*
The reason modifying the copy messed up the original library has to do with how JavaScript manages memory. The spread operator (...) creates what's called a "shallow copy." This means it duplicates the main top-level properties (like the library's name), but it takes a shortcut with nested objects or arrays (like our books). Instead of cloning that entire nested list, it just duplicates the memory pointer to the original array. Since both libraries point to the exact same array in memory, changing a book in one affects both. To get a completely independent copy where nested items are fully duplicated, you need a "deep copy." The cleanest way to do this in modern JS is: const trueClone = structuredClone(library);
*/
```

## Task 2: Advanced Conditional Logic (Validation)

```javascript
function validatePassword(password) {
  if (password.length < 8) {
    return "Error: Password must be at least 8 characters long.";
  }
  if (!/[A-Z]/.test(password)) {
    return "Error: Password must contain at least one uppercase letter.";
  }
  if (!/[0-9]/.test(password)) {
    return "Error: Password must contain at least one number.";
  }
  if (password.toLowerCase().includes("password")) {
    return "Error: Password must not contain the word \"password\".";
  }
  return "Strong Password";
}

// Test cases
console.log(validatePassword("short1A"));      // fails: too short
console.log(validatePassword("longenough1"));  // fails: no uppercase
console.log(validatePassword("LongEnough"));   // fails: no number
console.log(validatePassword("MyPassword123")); // fails: contains "password"
console.log(validatePassword("MySecure123"));  // "Strong Password"
```

## Task 3: Complex Iteration (Algorithms)

```javascript
function generateFibonacci(n) {
  const sequence = [];

  for (let i = 0; i < n; i++) {
    if (i === 0) {
      sequence.push(0);
    } else if (i === 1) {
      sequence.push(1);
    } else {
      sequence.push(sequence[i - 1] + sequence[i - 2]);
    }
  }

  return sequence;
}

console.log(generateFibonacci(7)); // [0, 1, 1, 2, 3, 5, 8]
```

## Task 4: Higher-Order Functions & Callbacks

```javascript
function processData(dataArray, callback) {
  const result = [];

  for (let i = 0; i < dataArray.length; i++) {
    result.push(callback(dataArray[i]));
  }

  return result;
}

// Test: square every number using an anonymous arrow function
const numbers = [1, 2, 3, 4, 5];
const squaredNumbers = processData(numbers, (num) => num * num);

console.log(squaredNumbers); // [1, 4, 9, 16, 25]
```

## Task 5: Functional Array Methods (Map, Filter, Reduce)

```javascript
const transactions = [
  { type: "deposit", amount: 150 },
  { type: "withdrawal", amount: 50 },
  { type: "deposit", amount: 200 },
  { type: "withdrawal", amount: 80 }
];

const finalBalance = transactions.reduce((balance, transaction) => {
  return transaction.type === "deposit"
    ? balance + transaction.amount
    : balance - transaction.amount;
}, 0);

console.log(finalBalance); // 220
```
