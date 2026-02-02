![Photo by DATAIDEA](../assets/banner_DATAIDEA.png)

# Control Flow

Learn how to make decisions and repeat actions in JavaScript using conditional statements and loops.

## Conditional Statements

Conditional statements allow your code to make decisions and execute different code based on conditions.

## if Statement

Execute code if a condition is true:

```javascript
let age = 20;

if (age >= 18) {
    console.log('You are an adult');
}
```

### if...else Statement

Execute one block if true, another if false:

```javascript
let age = 16;

if (age >= 18) {
    console.log('You are an adult');
} else {
    console.log('You are a minor');
}
```

### if...else if...else

Multiple conditions:

```javascript
let score = 85;

if (score >= 90) {
    console.log('Grade: A');
} else if (score >= 80) {
    console.log('Grade: B');
} else if (score >= 70) {
    console.log('Grade: C');
} else {
    console.log('Grade: F');
}
```

## Comparison Operators

Used in conditions:

```javascript
let a = 10;
let b = 5;

a === b;  // false (strict equality)
a !== b;  // true (strict inequality)
a > b;    // true
a < b;    // false
a >= b;   // true
a <= b;   // false
```

### Logical Operators

Combine conditions:

```javascript
let age = 25;
let hasLicense = true;

// AND (both must be true)
if (age >= 18 && hasLicense) {
    console.log('Can drive');
}

// OR (at least one true)
if (age < 18 || !hasLicense) {
    console.log('Cannot drive');
}

// NOT (opposite)
if (!hasLicense) {
    console.log('No license');
}
```

## Ternary Operator

Shorthand for if...else:

```javascript
let age = 20;

// Traditional way
let message;
if (age >= 18) {
    message = 'Adult';
} else {
    message = 'Minor';
}

// Ternary operator
let message = age >= 18 ? 'Adult' : 'Minor';
```

### Nested Ternary

```javascript
let score = 85;
let grade = score >= 90 ? 'A' : 
            score >= 80 ? 'B' : 
            score >= 70 ? 'C' : 'F';
```

!!! tip "Use Sparingly"
    Ternary operators are great for simple conditions, but can be hard to read when nested.

## switch Statement

Alternative to multiple if...else if:

```javascript
let day = 'Monday';

switch (day) {
    case 'Monday':
        console.log('Start of work week');
        break;
    case 'Friday':
        console.log('Weekend is coming!');
        break;
    case 'Saturday':
    case 'Sunday':
        console.log('Weekend!');
        break;
    default:
        console.log('Regular day');
}
```

### break Statement

Prevents "falling through" to next case:

```javascript
let num = 1;

switch (num) {
    case 1:
        console.log('One');
        // Missing break - will continue to case 2!
    case 2:
        console.log('Two');
        break;
}
// Output: 'One' 'Two' (unintended)
```

## Loops

Loops repeat code multiple times.

## for Loop

Repeat code a specific number of times:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
// Output: 0, 1, 2, 3, 4
```

**Structure:**
- Initialization: `let i = 0`
- Condition: `i < 5`
- Increment: `i++`

### for Loop Examples

```javascript
// Count from 1 to 10
for (let i = 1; i <= 10; i++) {
    console.log(i);
}

// Count backwards
for (let i = 10; i >= 1; i--) {
    console.log(i);
}

// Count by 2s
for (let i = 0; i <= 10; i += 2) {
    console.log(i);
}
```

## while Loop

Repeat while condition is true:

```javascript
let i = 0;

while (i < 5) {
    console.log(i);
    i++;
}
```

### Infinite Loops Warning

```javascript
// ❌ Wrong - infinite loop!
let i = 0;
while (i < 5) {
    console.log(i);
    // Forgot to increment i!
}

// ✅ Correct
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

## do...while Loop

Execute at least once, then check condition:

```javascript
let i = 0;

do {
    console.log(i);
    i++;
} while (i < 5);
```

## for...of Loop (Arrays)

Iterate over array elements:

```javascript
const fruits = ['apple', 'banana', 'orange'];

for (let fruit of fruits) {
    console.log(fruit);
}
// Output: 'apple', 'banana', 'orange'
```

## for...in Loop (Objects)

Iterate over object properties:

```javascript
const person = {
    name: 'John',
    age: 30,
    city: 'New York'
};

for (let key in person) {
    console.log(key + ': ' + person[key]);
}
// Output: 'name: John', 'age: 30', 'city: New York'
```

## Loop Control

### break

Exit loop immediately:

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break; // Exit loop
    }
    console.log(i);
}
// Output: 0, 1, 2, 3, 4
```

### continue

Skip to next iteration:

```javascript
for (let i = 0; i < 10; i++) {
    if (i % 2 === 0) {
        continue; // Skip even numbers
    }
    console.log(i);
}
// Output: 1, 3, 5, 7, 9
```

## Nested Loops

Loops inside loops:

```javascript
// Multiplication table
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        console.log(`${i} x ${j} = ${i * j}`);
    }
}
```

## Complete Examples

### Grade Calculator

```javascript
function calculateGrade(score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

console.log(calculateGrade(95)); // 'A'
console.log(calculateGrade(75)); // 'C'
console.log(calculateGrade(55)); // 'F'
```

### Number Guessing Game Logic

```javascript
let secretNumber = 7;
let guess = 5;

if (guess === secretNumber) {
    console.log('Correct!');
} else if (guess < secretNumber) {
    console.log('Too low!');
} else {
    console.log('Too high!');
}
```

### Countdown Timer

```javascript
for (let i = 10; i >= 0; i--) {
    if (i === 0) {
        console.log('Blast off!');
    } else {
        console.log(i);
    }
}
```

### Sum Numbers

```javascript
let sum = 0;

for (let i = 1; i <= 10; i++) {
    sum += i;
}

console.log(sum); // 55
```

### Find Even Numbers

```javascript
for (let i = 1; i <= 20; i++) {
    if (i % 2 === 0) {
        console.log(i);
    }
}
```

## Best Practices

1. **Use strict equality:** `===` instead of `==`
2. **Keep conditions simple:** Break complex conditions into variables
3. **Avoid deep nesting:** Use early returns or extract functions
4. **Use meaningful variable names:** `i` is fine for loops, but `index` is clearer
5. **Be careful with infinite loops:** Always ensure loop conditions can become false
6. **Use appropriate loop type:** `for` for known iterations, `while` for unknown

## Common Mistakes

### 1. Using Assignment Instead of Comparison

```javascript
// ❌ Wrong
if (x = 5) { } // Assigns 5 to x, always true!

// ✅ Correct
if (x === 5) { } // Compares x to 5
```

### 2. Missing break in switch

```javascript
// ❌ Wrong
switch (day) {
    case 'Monday':
        console.log('Monday');
    case 'Tuesday':
        console.log('Tuesday');
        break;
}
// Outputs both!

// ✅ Correct
switch (day) {
    case 'Monday':
        console.log('Monday');
        break;
    case 'Tuesday':
        console.log('Tuesday');
        break;
}
```

### 3. Infinite Loop

```javascript
// ❌ Wrong
let i = 0;
while (i < 10) {
    console.log(i);
    // Forgot i++
}

// ✅ Correct
let i = 0;
while (i < 10) {
    console.log(i);
    i++;
}
```

## Practice Exercise

Write code for:

1. Check if a number is positive, negative, or zero
2. Print all numbers from 1 to 100
3. Print only even numbers from 1 to 50
4. Calculate the sum of numbers from 1 to 100
5. Create a simple calculator using switch statement
6. Print a multiplication table for 5 (1x5 to 10x5)

## What's Next?

Now that you understand control flow, learn to:

- **Work with Arrays** - Store and manipulate lists of data
- **Use Objects** - Organize related data
- **DOM Manipulation** - Change web page content
- **Handle Events** - Respond to user interactions

---

**Previous Tutorial:** [Functions and Scope](03_functions_scope.md)  
**Next Tutorial:** [DOM Manipulation](05_dom_manipulation.md)

