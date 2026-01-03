# Variables and Data Types

Learn how to store and work with data in JavaScript using variables and understand the different types of data.

## Variables

Variables are containers that store data values. Think of them as labeled boxes where you can put things.

### Declaring Variables

Three ways to declare variables in JavaScript:

#### let (Modern, Recommended)

```javascript
let name = 'John';
let age = 30;
```

- Can be reassigned
- Block-scoped (we'll learn about scope later)
- Use for values that change

#### const (Modern, Recommended)

```javascript
const pi = 3.14159;
const company = 'Acme Corp';
```

- Cannot be reassigned
- Block-scoped
- Use for values that don't change

#### var (Legacy, Avoid)

```javascript
var oldWay = 'Not recommended';
```

- Can be reassigned
- Function-scoped
- Avoid in modern JavaScript

!!! tip "Use let and const"
    Always use `let` for variables that change and `const` for constants. Avoid `var`.

### Variable Naming Rules

```javascript
// ✅ Valid names
let userName = 'John';
let user_name = 'John';
let userName123 = 'John';
let $price = 100;
let _count = 5;

// ❌ Invalid names
let 123name = 'John';     // Can't start with number
let user-name = 'John';   // Can't use hyphens
let let = 'John';         // Can't use reserved words
```

**Rules:**
- Must start with letter, `$`, or `_`
- Can contain letters, numbers, `$`, and `_`
- Case-sensitive (`name` ≠ `Name`)
- Cannot use reserved words (`let`, `const`, `if`, etc.)

### Naming Conventions

```javascript
// camelCase (recommended for variables)
let userName = 'John';
let firstName = 'Jane';

// Descriptive names
let userAge = 25;        // ✅ Good
let a = 25;             // ❌ Bad - not descriptive
```

## Data Types

JavaScript has several data types. Let's explore them:

### Primitive Types

#### String

Text data:

```javascript
let name = 'John';
let message = "Hello, World!";
let greeting = `Hello, ${name}`; // Template literal
```

**String Methods:**
```javascript
let text = 'Hello World';

text.length;              // 11
text.toUpperCase();      // 'HELLO WORLD'
text.toLowerCase();      // 'hello world'
text.includes('Hello');  // true
text.indexOf('World');   // 6
```

#### Number

Numeric data:

```javascript
let age = 30;
let price = 19.99;
let temperature = -5;
```

**Number Operations:**
```javascript
let a = 10;
let b = 3;

a + b;  // 13 (addition)
a - b;  // 7 (subtraction)
a * b;  // 30 (multiplication)
a / b;  // 3.333... (division)
a % b;  // 1 (modulus - remainder)
a ** b; // 1000 (exponentiation)
```

#### Boolean

True or false:

```javascript
let isLoggedIn = true;
let isActive = false;
let hasPermission = true;
```

#### Undefined

Variable declared but not assigned:

```javascript
let name;
console.log(name); // undefined
```

#### Null

Intentionally empty value:

```javascript
let user = null;
```

#### Symbol

Unique identifier (advanced, rarely used):

```javascript
let id = Symbol('id');
```

### typeof Operator

Check the type of a value:

```javascript
typeof 'Hello';        // 'string'
typeof 42;             // 'number'
typeof true;            // 'boolean'
typeof undefined;      // 'undefined'
typeof null;           // 'object' (this is a bug in JavaScript)
```

## Type Conversion

### Converting to String

```javascript
let num = 42;
String(num);        // '42'
num.toString();     // '42'
num + '';           // '42' (concatenation)
```

### Converting to Number

```javascript
let str = '42';
Number(str);        // 42
parseInt(str);      // 42 (integer)
parseFloat('3.14'); // 3.14 (decimal)
+str;               // 42 (unary plus)
```

### Converting to Boolean

```javascript
Boolean(1);          // true
Boolean(0);          // false
Boolean('');         // false
Boolean('text');     // true
!!value;             // Convert to boolean
```

## Template Literals

Modern way to create strings with variables:

```javascript
let name = 'John';
let age = 30;

// Old way
let message = 'My name is ' + name + ' and I am ' + age + ' years old';

// New way (template literal)
let message = `My name is ${name} and I am ${age} years old`;
```

**Benefits:**
- Cleaner syntax
- Multi-line strings
- Expression evaluation

```javascript
let a = 10;
let b = 5;
let result = `The sum of ${a} and ${b} is ${a + b}`;
// 'The sum of 10 and 5 is 15'
```

## Operators

### Arithmetic Operators

```javascript
let a = 10;
let b = 3;

a + b;  // 13
a - b;  // 7
a * b;  // 30
a / b;  // 3.333...
a % b;  // 1 (remainder)
a ** b; // 1000 (power)
```

### Assignment Operators

```javascript
let x = 10;

x += 5;  // x = x + 5 (15)
x -= 3;  // x = x - 3 (12)
x *= 2;  // x = x * 2 (24)
x /= 4;  // x = x / 4 (6)
```

### Comparison Operators

```javascript
let a = 5;
let b = 10;

a == b;   // false (loose equality)
a === b;  // false (strict equality)
a != b;   // true (loose inequality)
a !== b;  // true (strict inequality)
a < b;    // true
a > b;    // false
a <= b;   // true
a >= b;   // false
```

!!! tip "Use Strict Equality"
    Always use `===` and `!==` instead of `==` and `!=` for more predictable results.

### Logical Operators

```javascript
let x = true;
let y = false;

x && y;  // false (AND - both must be true)
x || y;  // true (OR - at least one true)
!x;      // false (NOT - opposite)
```

## Constants

Use `const` for values that don't change:

```javascript
const PI = 3.14159;
const MAX_USERS = 100;
const API_URL = 'https://api.example.com';
```

**Naming Convention:** UPPER_SNAKE_CASE for constants.

## Variable Scope

### Block Scope (let, const)

```javascript
{
    let x = 10;
    const y = 20;
}
// x and y are not accessible here
```

### Global Scope

```javascript
let globalVar = 'I am global';

function myFunction() {
    console.log(globalVar); // Accessible
}
```

## Complete Examples

### User Information

```javascript
const firstName = 'John';
const lastName = 'Doe';
let age = 30;
const email = 'john.doe@example.com';
let isActive = true;

console.log(`Name: ${firstName} ${lastName}`);
console.log(`Age: ${age}`);
console.log(`Email: ${email}`);
console.log(`Active: ${isActive}`);
```

### Calculator

```javascript
const num1 = 10;
const num2 = 5;

let sum = num1 + num2;
let difference = num1 - num2;
let product = num1 * num2;
let quotient = num1 / num2;

console.log(`Sum: ${sum}`);
console.log(`Difference: ${difference}`);
console.log(`Product: ${product}`);
console.log(`Quotient: ${quotient}`);
```

## Best Practices

1. **Use const by default:** Only use `let` when you need to reassign
2. **Descriptive names:** `userName` not `u` or `n`
3. **camelCase:** For variable names
4. **UPPER_SNAKE_CASE:** For constants
5. **Initialize variables:** Always give variables an initial value
6. **Use strict equality:** `===` instead of `==`

## Common Mistakes

### 1. Using var

```javascript
// ❌ Wrong
var name = 'John';

// ✅ Correct
let name = 'John';
const name = 'John';
```

### 2. Not Using const for Constants

```javascript
// ❌ Wrong
let pi = 3.14159;

// ✅ Correct
const PI = 3.14159;
```

### 3. Loose Equality

```javascript
// ❌ Wrong
if (age == '30') { }

// ✅ Correct
if (age === 30) { }
```

### 4. Undeclared Variables

```javascript
// ❌ Wrong
name = 'John'; // Creates global variable

// ✅ Correct
let name = 'John';
```

## Practice Exercise

Create variables for:

1. Your name (string)
2. Your age (number)
3. Whether you're a student (boolean)
4. Your favorite number (constant)
5. Calculate: age + 10
6. Create a message using template literals: "My name is [name] and I am [age] years old"

## What's Next?

Now that you understand variables and data types, learn to:

- **Create Functions** - Organize and reuse code
- **Control Flow** - Make decisions with if/else
- **Loops** - Repeat actions
- **Work with Arrays** - Store multiple values
- **Use Objects** - Store related data

---

**Previous Tutorial:** [Introduction to JavaScript](01_introduction.md)  
**Next Tutorial:** [Functions and Scope](03_functions_scope.md)

