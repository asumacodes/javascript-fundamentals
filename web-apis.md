# JavaScript Web APIs Guide 🌐

## Introduction to Web APIs
Web APIs are browser-provided interfaces that extend JavaScript's capabilities for web development.

## Core Web APIs 🛠️

### 1. DOM (Document Object Model) API
```javascript
// Selecting elements
const element = document.querySelector('.my-class');
const elements = document.querySelectorAll('div');

// Modifying elements
element.textContent = 'New text';
element.classList.add('active');
element.style.backgroundColor = 'blue';

// Creating elements
const newDiv = document.createElement('div');
document.body.appendChild(newDiv);
```

### 2. Fetch API
```javascript
// Basic GET request
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));

// POST request
fetch('https://api.example.com/posts', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ title: 'foo', body: 'bar' })
});
```

### 3. Storage APIs
```javascript
// LocalStorage
localStorage.setItem('user', JSON.stringify({ name: 'John' }));
const user = JSON.parse(localStorage.getItem('user'));

// SessionStorage
sessionStorage.setItem('token', 'abc123');
const token = sessionStorage.getItem('token');

// Cookies
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2023 12:00:00 UTC; path=/";
```

### 4. Geolocation API
```javascript
if ("geolocation" in navigator) {
    navigator.geolocation.getCurrentPosition(
        position => {
            const { latitude, longitude } = position.coords;
            console.log(`Lat: ${latitude}, Long: ${longitude}`);
        },
        error => console.error('Error:', error)
    );
}
```

### 5. Canvas API
```javascript
const canvas = document.querySelector('canvas');
const ctx = canvas.getContext('2d');

// Drawing
ctx.fillStyle = 'red';
ctx.fillRect(10, 10, 100, 100);

// Paths
ctx.beginPath();
ctx.arc(100, 100, 50, 0, Math.PI * 2);
ctx.stroke();
```

## Event Handling 🎯

### Common Events
```javascript
// Click events
element.addEventListener('click', (e) => {
    console.log('Clicked!', e);
});

// Form events
form.addEventListener('submit', (e) => {
    e.preventDefault();
    // Handle form submission
});

// Keyboard events
document.addEventListener('keydown', (e) => {
    console.log('Key pressed:', e.key);
});
```

### Custom Events
```javascript
// Creating custom event
const event = new CustomEvent('userAction', {
    detail: { name: 'John' }
});

// Dispatching event
element.dispatchEvent(event);

// Listening for custom event
element.addEventListener('userAction', (e) => {
    console.log('User:', e.detail.name);
});
```

## Modern APIs 🚀

### 1. Intersection Observer
```javascript
const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
});

observer.observe(document.querySelector('.target'));
```

### 2. ResizeObserver
```javascript
const resizeObserver = new ResizeObserver(entries => {
    for (let entry of entries) {
        console.log('Element size:', entry.contentRect);
    }
});

resizeObserver.observe(element);
```

### 3. Web Workers
```javascript
// Main thread
const worker = new Worker('worker.js');

worker.postMessage({ data: 'Process this' });

worker.onmessage = (e) => {
    console.log('Result:', e.data);
};

// worker.js
self.onmessage = (e) => {
    // Process data
    self.postMessage(result);
};
```

## Security Considerations 🔒

### CORS (Cross-Origin Resource Sharing)
```javascript
fetch('https://api.example.com/data', {
    headers: {
        'Origin': 'https://myapp.com'
    },
    credentials: 'include'
});
```

### Content Security Policy
```html
<meta http-equiv="Content-Security-Policy" 
    content="default-src 'self'; img-src https://*;">
```

## Performance Tips 💪

1. **Use Passive Event Listeners**
```javascript
element.addEventListener('scroll', handler, { passive: true });
```

2. **Batch DOM Operations**
```javascript
const fragment = document.createDocumentFragment();
items.forEach(item => {
    const div = document.createElement('div');
    div.textContent = item;
    fragment.appendChild(div);
});
document.body.appendChild(fragment);
```

## Browser Support 🌍
- Check compatibility on MDN
- Use feature detection
- Implement fallbacks when needed

```javascript
if ('IntersectionObserver' in window) {
    // Use IntersectionObserver
} else {
    // Fallback
}
```

## Debugging Tools 🔧

1. Browser DevTools
   - Network tab for Fetch
   - Application tab for Storage
   - Performance monitoring

2. Console Methods
```javascript
console.log('Basic logging');
console.table(arrayOfObjects);
console.time('operation');
// ... code ...
console.timeEnd('operation');
```

## Resources 📚
- [MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)
- [Can I Use](https://caniuse.com/)
- [Web.dev](https://web.dev/)

## Contributing
Contributions welcome! Submit issues or PRs.

---
Created with 💻 by Web API Enthusiasts
