![Photo by DATAIDEA](../assets/banner_DATAIDEA.png)

# Functions and Scope

Learn how to create reusable code blocks with functions and understand variable scope in JavaScript.

## What are Functions?

Functions are reusable blocks of code that perform specific tasks. They help you:
- Avoid repeating code
- Organize your code
- Make code easier to understand and maintain

### Why Use Functions?

```javascript
// Without functions (repetitive)
console.log('Hello, John!');
console.log('Hello, Jane!');
console.log('Hello, Bob!');

// With functions (reusable)
function greet(name) {
    console.log(`Hello, ${name}!`);
}

greet('John');
greet('Jane');
greet('Bob');
```

## Function Declarations

### Basic Function

```javascript
function greet() {
    console.log('Hello, World!');
}

greet(); // Call the function
```

### Function with Parameters

```javascript
function greet(name) {
    console.log(`Hello, ${name}!`);
}

greet('John');  // 'Hello, John!'
greet('Jane');  // 'Hello, Jane!'
```

### Multiple Parameters

```javascript
function introduce(name, age) {
    console.log(`My name is ${name} and I am ${age} years old`);
}

introduce('John', 30);
```

### Function with Return

```javascript
function add(a, b) {
    return a + b;
}

let result = add(5, 3);
console.log(result); // 8
```

### Return Statement

```javascript
function multiply(x, y) {
    return x * y;
}

let product = multiply(4, 5); // 20
```

!!! tip "Return Early"
    Functions can have multiple return statements:
    ```javascript
    function isPositive(num) {
        if (num > 0) {
            return true;
        }
        return false;
    }
    ```

## Function Expressions

Store functions in variables:

```javascript
const greet = function(name) {
    console.log(`Hello, ${name}!`);
};

greet('John');
```

## Arrow Functions (ES6)

Modern, concise function syntax:

```javascript
// Traditional function
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => {
    return a + b;
};

// Arrow function (shorthand - single expression)
const add = (a, b) => a + b;
```

### Arrow Function Examples

```javascript
// No parameters
const sayHello = () => {
    console.log('Hello!');
};

// Single parameter (parentheses optional)
const double = x => x * 2;

// Multiple parameters
const multiply = (a, b) => a * b;

// Multiple statements
const greet = (name) => {
    const message = `Hello, ${name}!`;
    console.log(message);
    return message;
};
```

## Function Parameters

### Default Parameters

```javascript
function greet(name = 'Guest') {
    console.log(`Hello, ${name}!`);
}

greet('John');  // 'Hello, John!'
greet();        // 'Hello, Guest!'
```

### Rest Parameters

Collect multiple arguments:

```javascript
function sum(...numbers) {
    let total = 0;
    for (let num of numbers) {
        total += num;
    }
    return total;
}

sum(1, 2, 3);        // 6
sum(1, 2, 3, 4, 5);  // 15
```

## Scope

Scope determines where variables are accessible.

### Global Scope

Variables declared outside functions:

```javascript
let globalVar = 'I am global';

function myFunction() {
    console.log(globalVar); // Accessible
}

console.log(globalVar); // Accessible
```

### Local Scope (Function Scope)

Variables declared inside functions:

```javascript
function myFunction() {
    let localVar = 'I am local';
    console.log(localVar); // Accessible
}

console.log(localVar); // Error: localVar is not defined
```

### Block Scope

Variables declared with `let` or `const` inside blocks `{}`:

```javascript
if (true) {
    let blockVar = 'I am in a block';
    console.log(blockVar); // Accessible
}

console.log(blockVar); // Error: blockVar is not defined
```

### Scope Chain

Inner scopes can access outer scopes:

```javascript
let outer = 'I am outer';

function outerFunction() {
    let middle = 'I am middle';
    
    function innerFunction() {
        let inner = 'I am inner';
        console.log(outer);  // ✅ Accessible
        console.log(middle);  // ✅ Accessible
        console.log(inner);   // ✅ Accessible
    }
    
    innerFunction();
    console.log(outer);  // ✅ Accessible
    console.log(middle); // ✅ Accessible
    // console.log(inner); // ❌ Error: not accessible
}
```

## Hoisting

Function declarations are "hoisted" - moved to the top:

```javascript
// This works!
sayHello();

function sayHello() {
    console.log('Hello!');
}
```

Function expressions are NOT hoisted:

```javascript
// This doesn't work!
sayHello(); // Error

const sayHello = function() {
    console.log('Hello!');
};
```

## Higher-Order Functions

Functions that accept other functions as parameters:

```javascript
function greet(name) {
    console.log(`Hello, ${name}!`);
}

function processUser(name, callback) {
    console.log('Processing user...');
    callback(name);
}

processUser('John', greet);
```

## Complete Examples

### Calculator Functions

```javascript
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

function multiply(a, b) {
    return a * b;
}

function divide(a, b) {
    if (b === 0) {
        return 'Cannot divide by zero';
    }
    return a / b;
}

console.log(add(10, 5));        // 15
console.log(subtract(10, 5));  // 5
console.log(multiply(10, 5));  // 50
console.log(divide(10, 5));    // 2
```

### User Validation

```javascript
function validateEmail(email) {
    if (email.includes('@')) {
        return true;
    }
    return false;
}

function validateAge(age) {
    return age >= 18 && age <= 120;
}

function createUser(name, email, age) {
    if (!validateEmail(email)) {
        return 'Invalid email';
    }
    
    if (!validateAge(age)) {
        return 'Invalid age';
    }
    
    return {
        name: name,
        email: email,
        age: age
    };
}

let user = createUser('John', 'john@example.com', 30);
console.log(user);
```

### Arrow Function Examples

```javascript
// Simple calculations
const square = x => x * x;
const cube = x => x ** 3;

// Array operations
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);

// Event handlers
button.addEventListener('click', () => {
    console.log('Button clicked!');
});
```

## Best Practices

1. **Use descriptive names:** `calculateTotal` not `calc`
2. **Keep functions small:** One function, one task
3. **Use arrow functions:** For simple, concise functions
4. **Avoid global variables:** Use local scope when possible
5. **Return values:** Functions should return something useful
6. **Use default parameters:** Make functions more flexible

## Common Mistakes

### 1. Not Returning Values

```javascript
// ❌ Wrong
function add(a, b) {
    a + b; // No return
}

let result = add(5, 3); // undefined

// ✅ Correct
function add(a, b) {
    return a + b;
}

let result = add(5, 3); // 8
```

### 2. Variable Scope Issues

```javascript
// ❌ Wrong
function myFunction() {
    if (true) {
        var x = 10; // Function-scoped
    }
    console.log(x); // Works but confusing
}

// ✅ Correct
function myFunction() {
    if (true) {
        let x = 10; // Block-scoped
    }
    // x is not accessible here
}
```

### 3. Forgetting to Call Functions

```javascript
// ❌ Wrong
function greet() {
    console.log('Hello!');
}
greet; // Doesn't call the function

// ✅ Correct
greet(); // Calls the function
```

## Practice Exercise

Create functions for:

1. A function that greets a person by name
2. A function that calculates the area of a rectangle
3. A function that checks if a number is even
4. A function that returns the maximum of two numbers
5. An arrow function that doubles a number
6. A function with default parameters for greeting

## What's Next?

Now that you understand functions, learn to:

- **Control Flow** - Make decisions with if/else statements
- **Loops** - Repeat actions with for and while loops
- **Arrays** - Store and work with lists of data
- **Objects** - Organize related data

---

**Previous Tutorial:** [Variables and Data Types](02_variables_data_types.md)  
**Next Tutorial:** [Control Flow](04_control_flow.md)

