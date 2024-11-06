# JavaScript Hoisting Explained 🚀

## What is Hoisting?

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their respective scopes during the compilation phase, while the assignments stay in place.
Before code executes, memory is allocated to the variables and functions present in the scope.

## Types of Hoisting

### 1. Variable Hoisting 📝

#### var Declarations
```javascript
console.log(name); // undefined
var name = "John";

// Behind the scenes:
var name;         // declaration is hoisted
console.log(name);
name = "John";    // assignment stays
```

#### let and const Declarations
```javascript
console.log(age); // ReferenceError: Cannot access 'age' before initialization
let age = 25;

// let and const are hoisted but not initialized (Temporal Dead Zone)
```

## Temporal Dead Zone
The area of a block where a variable is inaccessible until the moment it gets initialized with a value.

### 2. Function Hoisting 🔄

#### Function Declarations
```javascript
sayHello(); // "Hello World!"

function sayHello() {
    console.log("Hello World!");
}
// Function declarations are completely hoisted with their implementation
```

#### Function Expressions
```javascript
greet(); // TypeError: greet is not a function

var greet = function() {
    console.log("Good morning!");
};
// Only the variable declaration is hoisted
```

### 3. Arrow Functions vs Regular Functions ⚡

```javascript
// Regular Function - Hoisted
regularFunc(); // Works!
function regularFunc() {
    console.log("I'm hoisted!");
}

// Arrow Function - Not hoisted
arrowFunc(); // Error!
const arrowFunc = () => {
    console.log("I'm not hoisted!");
};
```

## Best Practices 💡

1. **Always declare first**
   ```javascript
   // Bad
   x = 5;
   var x;

   // Good
   let x;
   x = 5;
   ```

2. **Use let/const over var**
   ```javascript
   // Avoid
   var x = 1;

   // Prefer
   const x = 1;
   let y = 2;
   ```

3. **Function Declarations vs Expressions**
   ```javascript
   // Preferred when hoisting is needed
   function doSomething() {
       // ...
   }

   // Preferred when hoisting should be prevented
   const doSomethingElse = () => {
       // ...
   };
   ```

## Common Pitfalls ⚠️

### 1. The Temporal Dead Zone (TDZ)
```javascript
console.log(x); // ReferenceError
let x = 1;
```

### 2. Function Expression Hoisting
```javascript
sayHi(); // TypeError: sayHi is not a function
var sayHi = function() {
    console.log("Hi!");
};
```

## Tips for Debugging 🔍

1. Always check variable declarations
2. Be aware of function declaration placement
3. Watch out for the Temporal Dead Zone with let/const

## Additional Resources 📚

- [MDN Web Docs - Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- [JavaScript.info - Variables](https://javascript.info/variables)

## Contributing

Feel free to contribute to this document by creating a pull request or opening an issue!

---
Created with 💻 by AsumaCodes
