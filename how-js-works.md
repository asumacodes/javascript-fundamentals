# How JavaScript Works?

## Table of Contents
1. [Introduction to JavaScript](#introduction-to-javascript)
2. [JavaScript Engine](#javascript-engine)
3. [How JavaScript is Executed](#how-javascript-is-executed)
4. [Memory Allocation and Code Execution](#memory-allocation-and-code-execution)
5. [Call Stack](#call-stack)
6. [Key Takeaways](#key-takeaways)

---

## 1. Introduction to JavaScript
JavaScript is a **dynamic**, **weakly-typed** programming language primarily used for web development. Key characteristics include:
- **Single-threaded**: Executes one task at a time.
- **Synchronous**: Executes code sequentially unless specified otherwise.
- **Runtime Compilation**: Compiled to machine code just before execution.

JavaScript requires a **host environment** (like a browser or server) to run. Modern browsers come with built-in JavaScript engines (e.g., **V8** in Chrome, **SpiderMonkey** in Firefox) to execute code efficiently.

---

## 2. JavaScript Engine
The **JavaScript Engine** is the core that interprets and executes JavaScript code. Major steps involved in executing JS code include:
1. **Parsing**: Converts code into an Abstract Syntax Tree (AST).
2. **Compilation**: Translates the AST to machine code using Just-In-Time (JIT) compilation.
3. **Execution**: Runs the compiled machine code to produce results.

These steps happen within an **Execution Context**.

---

## 3. How JavaScript is Executed
The **Execution Context** is the environment where JavaScript code runs. Execution contexts determine variable scope and how code is processed, and there are two main types:

- **Global Context**: The default environment where your code runs initially.
- **Function Context**: Created every time a function is called, with its own scope and variables.

Each execution context consists of:
- **Variable Environment**: Stores variables and function declarations.
- **Thread of Execution**: Executes code line by line.

An **Execution Context** has two primary stages:
1. **Creation Phase**: Memory allocation for variables and functions.
   - Variables are initialized with `undefined`.
2. **Execution Phase**: The code runs line by line, assigning values to variables and executing functions.

Each function call creates a new execution context, which exists independently of other contexts.

---

## 4. Memory Allocation and Code Execution
JavaScript execution involves **two distinct phases**:

### 1. Memory Allocation
During this phase, JavaScript allocates memory for variables and functions:
- **Variables** are assigned memory space and given an initial value of `undefined`.
- **Functions** are assigned memory space and contain the code they’re defined with.

### 2. Code Execution
In this phase, the JavaScript engine executes code line by line:
- **Variables** get their assigned values.
- **Functions** are invoked and, if necessary, create new execution contexts for their execution.

---

## 5. Call Stack
The **Call Stack** is a data structure that keeps track of all active execution contexts in a last-in, first-out (LIFO) order. Here’s how it works:
1. **Function Call**: When a function is invoked, it’s added to the top of the stack.
2. **Return or End**: When the function completes, it’s removed from the stack.

For example:
```javascript
function first() {
    second();
    console.log('First');
}

function second() {
    console.log('Second');
}

first(); // Output: "Second" "First"
```

When `first()` is called, it’s added to the stack. Inside `first()`, `second()` is called and added to the stack, resulting in `second()` executing before `first()` completes.

The Call Stack provides a clear mechanism for understanding JavaScript's single-threaded execution and helps with debugging errors through stack traces.

---

## 6. Key Takeaways
- **Execution Context** is the environment where code is evaluated and executed.
- **Memory Allocation** assigns initial values to variables, while Code Execution runs the code line by line.
- The **Call Stack** helps manage function calls in a LIFO order, allowing JavaScript to handle nested and sequential function calls effectively.
