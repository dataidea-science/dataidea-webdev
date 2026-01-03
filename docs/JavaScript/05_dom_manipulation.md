# DOM Manipulation

Learn how to interact with and modify web pages using JavaScript and the Document Object Model (DOM).

## What is the DOM?

The DOM (Document Object Model) is a representation of your HTML page that JavaScript can interact with. It's like a tree structure of all the elements on your page.

### DOM Tree Structure

```
Document (root)
└── html
    ├── head
    │   ├── title
    │   └── meta
    └── body
        ├── h1
        ├── p
        └── div
            └── button
```

## Selecting Elements

### getElementById

Select element by ID:

```javascript
const header = document.getElementById('header');
```

**HTML:**
```html
<div id="header">Header Content</div>
```

### querySelector

Select first matching element (modern, recommended):

```javascript
const button = document.querySelector('.my-button');
const header = document.querySelector('#header');
const paragraph = document.querySelector('p');
```

### querySelectorAll

Select all matching elements:

```javascript
const paragraphs = document.querySelectorAll('p');
const buttons = document.querySelectorAll('.button');
```

Returns a NodeList (array-like object).

### Other Selection Methods

```javascript
// Get elements by class name
const items = document.getElementsByClassName('item');

// Get elements by tag name
const divs = document.getElementsByTagName('div');
```

## Modifying Content

### textContent

Get or set text content:

```javascript
const heading = document.querySelector('h1');
heading.textContent = 'New Heading';
console.log(heading.textContent); // 'New Heading'
```

### innerHTML

Get or set HTML content:

```javascript
const div = document.querySelector('.content');
div.innerHTML = '<p>New paragraph</p>';
```

!!! warning "Security Risk"
    `innerHTML` can be dangerous if used with user input. Use `textContent` for user-generated content.

### innerText

Get or set visible text (respects CSS):

```javascript
const element = document.querySelector('p');
element.innerText = 'New text';
```

## Modifying Attributes

### getAttribute / setAttribute

```javascript
const link = document.querySelector('a');

// Get attribute
const href = link.getAttribute('href');

// Set attribute
link.setAttribute('href', 'https://example.com');
link.setAttribute('target', '_blank');
```

### Direct Property Access

```javascript
const image = document.querySelector('img');

// Set properties
image.src = 'new-image.jpg';
image.alt = 'New image';
image.width = 300;
```

## Modifying Styles

### style Property

Change CSS styles:

```javascript
const element = document.querySelector('.box');

element.style.color = 'red';
element.style.backgroundColor = 'blue';
element.style.fontSize = '20px';
element.style.display = 'none';
```

**Note:** Use camelCase for CSS properties (`backgroundColor` not `background-color`).

### classList

Add, remove, or toggle CSS classes:

```javascript
const button = document.querySelector('button');

// Add class
button.classList.add('active');

// Remove class
button.classList.remove('active');

// Toggle class
button.classList.toggle('active');

// Check if has class
if (button.classList.contains('active')) {
    console.log('Button is active');
}
```

## Creating Elements

### createElement

Create new HTML elements:

```javascript
const newParagraph = document.createElement('p');
newParagraph.textContent = 'This is a new paragraph';
```

### appendChild

Add element to page:

```javascript
const container = document.querySelector('.container');
const newDiv = document.createElement('div');
newDiv.textContent = 'New div';
container.appendChild(newDiv);
```

### insertBefore

Insert element before another:

```javascript
const container = document.querySelector('.container');
const newDiv = document.createElement('div');
const existingDiv = document.querySelector('.existing');
container.insertBefore(newDiv, existingDiv);
```

### removeChild

Remove element:

```javascript
const element = document.querySelector('.to-remove');
element.parentNode.removeChild(element);

// Modern way (ES6+)
element.remove();
```

## Complete Examples

### Change Text Content

```html
<h1 id="title">Original Title</h1>
<button onclick="changeTitle()">Change Title</button>

<script>
function changeTitle() {
    const title = document.getElementById('title');
    title.textContent = 'New Title';
}
</script>
```

### Add New Element

```html
<div id="container"></div>
<button onclick="addItem()">Add Item</button>

<script>
function addItem() {
    const container = document.getElementById('container');
    const newItem = document.createElement('div');
    newItem.textContent = 'New Item';
    newItem.className = 'item';
    container.appendChild(newItem);
}
</script>
```

### Toggle Visibility

```html
<div id="content">This content can be hidden</div>
<button onclick="toggleContent()">Toggle</button>

<script>
function toggleContent() {
    const content = document.getElementById('content');
    if (content.style.display === 'none') {
        content.style.display = 'block';
    } else {
        content.style.display = 'none';
    }
}

// Better way using classList
function toggleContent() {
    const content = document.getElementById('content');
    content.classList.toggle('hidden');
}
</script>

<style>
.hidden {
    display: none;
}
</style>
```

### Change Multiple Elements

```html
<p class="text">Paragraph 1</p>
<p class="text">Paragraph 2</p>
<p class="text">Paragraph 3</p>
<button onclick="changeAll()">Change All</button>

<script>
function changeAll() {
    const paragraphs = document.querySelectorAll('.text');
    paragraphs.forEach(p => {
        p.style.color = 'blue';
        p.style.fontSize = '20px';
    });
}
</script>
```

### Dynamic List

```html
<ul id="list"></ul>
<input type="text" id="itemInput" placeholder="Add item">
<button onclick="addListItem()">Add</button>

<script>
function addListItem() {
    const input = document.getElementById('itemInput');
    const list = document.getElementById('list');
    
    if (input.value.trim() !== '') {
        const li = document.createElement('li');
        li.textContent = input.value;
        list.appendChild(li);
        input.value = ''; // Clear input
    }
}
</script>
```

## Traversing the DOM

### parentNode

Get parent element:

```javascript
const child = document.querySelector('.child');
const parent = child.parentNode;
```

### children

Get child elements:

```javascript
const container = document.querySelector('.container');
const children = container.children;
```

### nextSibling / previousSibling

Get adjacent elements:

```javascript
const element = document.querySelector('.middle');
const next = element.nextSibling;
const previous = element.previousSibling;
```

## Best Practices

1. **Cache selections:** Store selected elements in variables
2. **Use querySelector:** Modern and flexible
3. **Prefer classList:** Over direct style manipulation
4. **Use textContent:** For user-generated content (security)
5. **Check if element exists:** Before manipulating
6. **Use event delegation:** For dynamic content

## Common Mistakes

### 1. Not Waiting for DOM to Load

```javascript
// ❌ Wrong
const element = document.getElementById('myElement');
element.textContent = 'Hello'; // Element might not exist yet

// ✅ Correct
document.addEventListener('DOMContentLoaded', function() {
    const element = document.getElementById('myElement');
    element.textContent = 'Hello';
});
```

### 2. Using innerHTML with User Input

```javascript
// ❌ Wrong - Security risk!
const userInput = '<script>alert("XSS")</script>';
element.innerHTML = userInput;

// ✅ Correct
element.textContent = userInput;
```

### 3. Selecting Non-Existent Elements

```javascript
// ❌ Wrong
const element = document.getElementById('nonexistent');
element.textContent = 'Hello'; // Error!

// ✅ Correct
const element = document.getElementById('nonexistent');
if (element) {
    element.textContent = 'Hello';
}
```

## Practice Exercise

Create a page with:

1. A heading that changes when a button is clicked
2. A button that adds new paragraphs to a container
3. A button that toggles a div's visibility
4. An input field that adds items to a list
5. Buttons that change text color of all paragraphs
6. A counter that increments when clicked

## What's Next?

Now that you can manipulate the DOM, learn to:

- **Handle Events** - Respond to clicks, inputs, and other user actions
- **Form Validation** - Validate user input
- **Create Interactive UIs** - Build dynamic user interfaces
- **Work with APIs** - Fetch and display data

---

**Previous Tutorial:** [Control Flow](04_control_flow.md)  
**Next Tutorial:** [Events and Interactivity](06_events.md)

