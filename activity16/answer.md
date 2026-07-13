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
Why did the original change too?

A shallow copy (using {...library} or Object.assign({}, library)) only
copies the library object's TOP-LEVEL properties. The `books` property
holds an array, and arrays/objects in JavaScript are reference types —
so the copy's `books` property doesn't get a new array, it just gets a
copy of the REFERENCE (memory address) pointing to the same array the
original uses. copiedLibrary.books and library.books are therefore two
different variables pointing at the exact same array and the exact same
book objects inside it. Mutating a book (copiedLibrary.books[0].isAvailable
= false) changes that shared object, so the change is visible through
library.books[0] as well.

How to prevent it — use a DEEP copy instead, which recursively copies
every nested object/array so no references are shared:
  - structuredClone(library)              // modern, built-in
  - JSON.parse(JSON.stringify(library))   // simple, but loses functions/dates
  - a hand-written recursive clone function

With a true deep copy, editing copiedLibrary.books[0] would leave
library.books[0] completely untouched.
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
