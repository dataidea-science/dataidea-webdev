# Events and Interactivity

Learn how to make your web pages interactive by responding to user actions like clicks, keyboard input, and form submissions.

## What are Events?

Events are actions that happen in the browser, such as:
- User clicks a button
- User types in an input field
- Page finishes loading
- User submits a form
- Mouse moves over an element

JavaScript can "listen" for these events and respond to them.

## Event Listeners

### addEventListener

The modern way to handle events:

```javascript
const button = document.querySelector('button');

button.addEventListener('click', function() {
    alert('Button clicked!');
});
```

**Syntax:**
```javascript
element.addEventListener(event, function, options);
```

### Inline Event Handlers (Not Recommended)

```html
<!-- Works but not recommended -->
<button onclick="alert('Clicked!')">Click Me</button>
```

!!! tip "Use addEventListener"
    Always use `addEventListener` instead of inline handlers for better code organization.

## Common Events

### Mouse Events

```javascript
// Click
button.addEventListener('click', function() {
    console.log('Clicked!');
});

// Double click
element.addEventListener('dblclick', function() {
    console.log('Double clicked!');
});

// Mouse enter
element.addEventListener('mouseenter', function() {
    console.log('Mouse entered');
});

// Mouse leave
element.addEventListener('mouseleave', function() {
    console.log('Mouse left');
});

// Mouse move
element.addEventListener('mousemove', function() {
    console.log('Mouse moved');
});
```

### Keyboard Events

```javascript
const input = document.querySelector('input');

// Key down
input.addEventListener('keydown', function(event) {
    console.log('Key pressed:', event.key);
});

// Key up
input.addEventListener('keyup', function(event) {
    console.log('Key released:', event.key);
});

// Key press
input.addEventListener('keypress', function(event) {
    console.log('Character:', event.key);
});
```

### Form Events

```javascript
const form = document.querySelector('form');

// Submit
form.addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent form submission
    console.log('Form submitted');
});

// Input change
const input = document.querySelector('input');
input.addEventListener('input', function() {
    console.log('Input changed:', input.value);
});

// Focus
input.addEventListener('focus', function() {
    console.log('Input focused');
});

// Blur
input.addEventListener('blur', function() {
    console.log('Input lost focus');
});
```

### Window Events

```javascript
// Page loaded
window.addEventListener('load', function() {
    console.log('Page loaded');
});

// DOM ready
document.addEventListener('DOMContentLoaded', function() {
    console.log('DOM ready');
});

// Resize
window.addEventListener('resize', function() {
    console.log('Window resized');
});

// Scroll
window.addEventListener('scroll', function() {
    console.log('Page scrolled');
});
```

## Event Object

Event handlers receive an event object with useful information:

```javascript
button.addEventListener('click', function(event) {
    console.log(event.type);        // 'click'
    console.log(event.target);      // The element that was clicked
    console.log(event.clientX);     // Mouse X position
    console.log(event.clientY);     // Mouse Y position
});
```

### preventDefault()

Prevent default browser behavior:

```javascript
const link = document.querySelector('a');

link.addEventListener('click', function(event) {
    event.preventDefault(); // Don't follow the link
    console.log('Link clicked but not followed');
});
```

### stopPropagation()

Stop event from bubbling up:

```javascript
button.addEventListener('click', function(event) {
    event.stopPropagation(); // Don't trigger parent's click
    console.log('Button clicked');
});
```

## Event Delegation

Attach event listener to parent, handle events from children:

```html
<ul id="list">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

```javascript
const list = document.getElementById('list');

list.addEventListener('click', function(event) {
    if (event.target.tagName === 'LI') {
        console.log('Clicked:', event.target.textContent);
    }
});
```

**Benefits:**
- Works with dynamically added elements
- More efficient (one listener instead of many)
- Easier to manage

## Removing Event Listeners

```javascript
function handleClick() {
    console.log('Clicked');
}

button.addEventListener('click', handleClick);

// Remove later
button.removeEventListener('click', handleClick);
```

!!! tip "Named Functions for Removal"
    Use named functions if you need to remove event listeners later.

## Complete Examples

### Interactive Button

```html
<button id="myButton">Click Me</button>
<p id="counter">Clicks: 0</p>

<script>
let count = 0;
const button = document.getElementById('myButton');
const counter = document.getElementById('counter');

button.addEventListener('click', function() {
    count++;
    counter.textContent = `Clicks: ${count}`;
    
    if (count === 10) {
        button.textContent = 'Enough!';
        button.disabled = true;
    }
});
</script>
```

### Form Validation

```html
<form id="myForm">
    <input type="email" id="email" placeholder="Email" required>
    <input type="password" id="password" placeholder="Password" required>
    <button type="submit">Submit</button>
    <p id="error"></p>
</form>

<script>
const form = document.getElementById('myForm');
const email = document.getElementById('email');
const password = document.getElementById('password');
const error = document.getElementById('error');

form.addEventListener('submit', function(event) {
    event.preventDefault();
    
    if (email.value === '') {
        error.textContent = 'Email is required';
        return;
    }
    
    if (password.value.length < 6) {
        error.textContent = 'Password must be at least 6 characters';
        return;
    }
    
    error.textContent = '';
    alert('Form submitted successfully!');
});
</script>
```

### Dynamic List with Delete

```html
<input type="text" id="itemInput" placeholder="Add item">
<button id="addButton">Add</button>
<ul id="itemList"></ul>

<script>
const input = document.getElementById('itemInput');
const addButton = document.getElementById('addButton');
const list = document.getElementById('itemList');

function addItem() {
    const text = input.value.trim();
    if (text === '') return;
    
    const li = document.createElement('li');
    li.textContent = text;
    
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = 'Delete';
    deleteBtn.addEventListener('click', function() {
        li.remove();
    });
    
    li.appendChild(deleteBtn);
    list.appendChild(li);
    input.value = '';
}

addButton.addEventListener('click', addItem);

input.addEventListener('keypress', function(event) {
    if (event.key === 'Enter') {
        addItem();
    }
});
</script>
```

### Hover Effects

```html
<div class="box">Hover over me</div>

<script>
const box = document.querySelector('.box');

box.addEventListener('mouseenter', function() {
    box.style.backgroundColor = 'lightblue';
    box.style.transform = 'scale(1.1)';
});

box.addEventListener('mouseleave', function() {
    box.style.backgroundColor = '';
    box.style.transform = 'scale(1)';
});
</script>
```

### Keyboard Shortcuts

```javascript
document.addEventListener('keydown', function(event) {
    // Ctrl/Cmd + S
    if ((event.ctrlKey || event.metaKey) && event.key === 's') {
        event.preventDefault();
        console.log('Save shortcut pressed');
    }
    
    // Escape key
    if (event.key === 'Escape') {
        console.log('Escape pressed');
    }
});
```

## Best Practices

1. **Use addEventListener:** Instead of inline handlers
2. **Event Delegation:** For dynamic content
3. **preventDefault:** When needed, but use carefully
4. **Remove Listeners:** When elements are removed
5. **Named Functions:** For listeners you might need to remove
6. **Check Event Target:** In delegated events

## Common Mistakes

### 1. Not Preventing Default

```javascript
// ❌ Wrong
form.addEventListener('submit', function() {
    // Form still submits and page reloads
    console.log('Submitted');
});

// ✅ Correct
form.addEventListener('submit', function(event) {
    event.preventDefault();
    console.log('Submitted');
});
```

### 2. Adding Listeners Before DOM Loads

```javascript
// ❌ Wrong
const button = document.querySelector('button'); // null if script runs before HTML
button.addEventListener('click', function() {});

// ✅ Correct
document.addEventListener('DOMContentLoaded', function() {
    const button = document.querySelector('button');
    button.addEventListener('click', function() {});
});
```

### 3. Not Using Event Delegation for Dynamic Content

```javascript
// ❌ Wrong - won't work for new items
const items = document.querySelectorAll('.item');
items.forEach(item => {
    item.addEventListener('click', function() {});
});

// ✅ Correct - works for all items
const container = document.querySelector('.container');
container.addEventListener('click', function(event) {
    if (event.target.classList.contains('item')) {
        // Handle click
    }
});
```

## Practice Exercise

Create interactive features:

1. A button that changes color when clicked
2. A counter that increments/decrements with buttons
3. A form that validates email on submit
4. A list where you can add and delete items
5. An input that shows character count
6. A button that toggles dark mode

## What's Next?

Congratulations! You've learned the fundamentals of JavaScript. Continue with:

- **Arrays and Objects** - Work with complex data structures
- **Async JavaScript** - Promises, async/await, and API calls
- **Modern JavaScript** - ES6+ features and best practices
- **JavaScript Frameworks** - React, Vue, or Angular
- **Node.js** - JavaScript on the server

---

**Previous Tutorial:** [DOM Manipulation](05_dom_manipulation.md)  
**Next Steps:** Practice building interactive websites, or explore advanced JavaScript topics!

