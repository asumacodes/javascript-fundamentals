# JavaScript Event Loop Explained 🔄

## The JavaScript Runtime Environment 🏗️

### Core Components
1. Call Stack
2. Event Loop
3. Callback Queue (Task Queue)
4. Microtask Queue
5. Heap Memory

## Call Stack 📚

### What is the Call Stack?
The call stack is a data structure that records where in the program we are, tracking function calls.

```javascript
function firstFunction() {
    secondFunction();
    console.log('First');
}

function secondFunction() {
    console.log('Second');
}

firstFunction();

// Call Stack Sequence:
// 1. firstFunction()
// 2. secondFunction()
// 3. console.log('Second')
// 4. console.log('First')
```

### Stack Overflow
```javascript
function recurse() {
    recurse(); // Don't try this at home!
}

recurse(); // Stack overflow error
```

## Event Loop Mechanism 🔄

### Basic Flow
1. Execute synchronous code
2. Check microtask queue
3. Check callback queue
4. Update rendering
5. Repeat

```javascript
console.log('Start'); // 1

setTimeout(() => {
    console.log('Timeout'); // 4
}, 0);

Promise.resolve()
    .then(() => console.log('Promise')); // 3

console.log('End'); // 2

// Output:
// Start
// End
// Promise
// Timeout
```

## Queue Types 📋

### 1. Callback Queue (Task Queue)
- setTimeout/setInterval callbacks
- DOM events
- AJAX responses
- requestAnimationFrame

```javascript
setTimeout(() => console.log('Timeout 1'), 0);
setTimeout(() => console.log('Timeout 2'), 0);

// Output after all sync code:
// Timeout 1
// Timeout 2
```

### 2. Microtask Queue
- Promise callbacks
- queueMicrotask()
- MutationObserver

```javascript
Promise.resolve('Promise 1').then(console.log);
Promise.resolve('Promise 2').then(console.log);
queueMicrotask(() => console.log('Microtask'));

// Output after sync code:
// Promise 1
// Promise 2
// Microtask
```

## Real-World Examples 🌟

### Async/Await Flow
```javascript
async function example() {
    console.log('1');
    
    await Promise.resolve();
    console.log('2');
    
    setTimeout(() => console.log('3'), 0);
    
    await Promise.resolve();
    console.log('4');
}

example();
console.log('5');

// Output:
// 1
// 5
// 2
// 4
// 3
```

### Event Handler Queue
```javascript
button.addEventListener('click', () => {
    console.log('Button clicked');
    
    Promise.resolve()
        .then(() => console.log('Promise'));
        
    setTimeout(() => console.log('Timeout'), 0);
});
```

## Common Pitfalls ⚠️

### Blocking the Event Loop
```javascript
// Bad practice
function longLoop() {
    for(let i = 0; i < 1000000000; i++) {
        // Blocking operation
    }
}

// Better practice
function nonBlocking(i = 0) {
    if (i >= 1000000000) return;
    setTimeout(() => nonBlocking(i + 1000), 0);
}
```

### Race Conditions
```javascript
let data = null;

fetch('api/data')
    .then(response => response.json())
    .then(result => data = result);

console.log(data); // Still null!
```

## Best Practices 💡

1. **Avoid Long-Running Tasks**
   ```javascript
   // Break into smaller chunks
   function processArray(array, chunk = 1000) {
       const process = (index) => {
           if (index >= array.length) return;
           
           // Process chunk
           setTimeout(() => process(index + chunk), 0);
       };
       
       process(0);
   }
   ```

2. **Handle Errors in Async Operations**
   ```javascript
   async function safeOperation() {
       try {
           await riskyOperation();
       } catch (error) {
           console.error('Operation failed:', error);
       }
   }
   ```

## Debugging Tips 🔍

1. Use Chrome DevTools Performance tab
2. Monitor task durations
3. Look for long-running scripts
4. Check queue handling

## Resources 📚
- [MDN Web Docs - Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- [JZ Info - Event Loop](https://javascript.info/event-loop)

## Contributing

Feel free to contribute to this document by creating a pull request or opening an issue!

---
Created with 💻 by AsumaCodes
