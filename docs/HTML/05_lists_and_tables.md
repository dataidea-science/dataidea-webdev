# Lists and Tables

Learn how to organize information using lists and display structured data with tables.

## Lists

HTML provides three types of lists: unordered (bulleted), ordered (numbered), and description lists.

## Unordered Lists

Unordered lists use bullet points. Created with `<ul>` (unordered list) and `<li>` (list item).

### Basic Unordered List

```html
<ul>
    <li>Apple</li>
    <li>Banana</li>
    <li>Orange</li>
</ul>
```

**Displays as:**
- Apple
- Banana
- Orange

### Nested Lists

You can nest lists inside other lists:

```html
<ul>
    <li>Fruits
        <ul>
            <li>Apple</li>
            <li>Banana</li>
        </ul>
    </li>
    <li>Vegetables
        <ul>
            <li>Carrot</li>
            <li>Broccoli</li>
        </ul>
    </li>
</ul>
```

## Ordered Lists

Ordered lists use numbers. Created with `<ol>` (ordered list) and `<li>` (list item).

### Basic Ordered List

```html
<ol>
    <li>First item</li>
    <li>Second item</li>
    <li>Third item</li>
</ol>
```

**Displays as:**
1. First item
2. Second item
3. Third item

### Ordered List Attributes

#### Start Number

```html
<ol start="5">
    <li>Fifth item</li>
    <li>Sixth item</li>
</ol>
```

#### Reversed List

```html
<ol reversed>
    <li>Third item</li>
    <li>Second item</li>
    <li>First item</li>
</ol>
```

#### List Type

```html
<!-- Numbers (default) -->
<ol type="1">
    <li>Item one</li>
    <li>Item two</li>
</ol>

<!-- Uppercase letters -->
<ol type="A">
    <li>Item A</li>
    <li>Item B</li>
</ol>

<!-- Lowercase letters -->
<ol type="a">
    <li>Item a</li>
    <li>Item b</li>
</ol>

<!-- Uppercase Roman numerals -->
<ol type="I">
    <li>Item I</li>
    <li>Item II</li>
</ol>

<!-- Lowercase Roman numerals -->
<ol type="i">
    <li>Item i</li>
    <li>Item ii</li>
</ol>
```

### Nested Ordered Lists

```html
<ol>
    <li>Chapter 1
        <ol>
            <li>Section 1.1</li>
            <li>Section 1.2</li>
        </ol>
    </li>
    <li>Chapter 2
        <ol>
            <li>Section 2.1</li>
            <li>Section 2.2</li>
        </ol>
    </li>
</ol>
```

## Description Lists

Description lists pair terms with their descriptions. Use `<dl>` (description list), `<dt>` (description term), and `<dd>` (description definition).

### Basic Description List

```html
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language - the standard markup language for web pages.</dd>
    
    <dt>CSS</dt>
    <dd>Cascading Style Sheets - used to style HTML elements.</dd>
    
    <dt>JavaScript</dt>
    <dd>A programming language that adds interactivity to web pages.</dd>
</dl>
```

### Multiple Descriptions

```html
<dl>
    <dt>Web Browser</dt>
    <dd>Chrome</dd>
    <dd>Firefox</dd>
    <dd>Safari</dd>
</dl>
```

## Using Lists in Navigation

Lists are commonly used for navigation menus:

```html
<nav>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="contact.html">Contact</a></li>
    </ul>
</nav>
```

## Tables

Tables display data in rows and columns. Essential for structured information.

## Basic Table Structure

```html
<table>
    <tr>
        <th>Name</th>
        <th>Age</th>
        <th>City</th>
    </tr>
    <tr>
        <td>John</td>
        <td>30</td>
        <td>New York</td>
    </tr>
    <tr>
        <td>Jane</td>
        <td>25</td>
        <td>London</td>
    </tr>
</table>
```

### Table Elements

- `<table>` - Container for the entire table
- `<tr>` - Table row
- `<th>` - Table header (bold, centered by default)
- `<td>` - Table data cell

## Table Headers

### Header Row

```html
<table>
    <tr>
        <th>Product</th>
        <th>Price</th>
        <th>Stock</th>
    </tr>
    <tr>
        <td>Laptop</td>
        <td>$999</td>
        <td>15</td>
    </tr>
</table>
```

### Column Headers

```html
<table>
    <tr>
        <th>Name</th>
        <th>Email</th>
    </tr>
    <tr>
        <td>John Doe</td>
        <td>john@example.com</td>
    </tr>
</table>
```

## Advanced Table Structure

### Table Sections

For better organization, use table sections:

```html
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Score</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Alice</td>
            <td>95</td>
        </tr>
        <tr>
            <td>Bob</td>
            <td>87</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Average</td>
            <td>91</td>
        </tr>
    </tfoot>
</table>
```

- `<thead>` - Header section (column headers)
- `<tbody>` - Body section (main data)
- `<tfoot>` - Footer section (summaries, totals)

### Table Caption

```html
<table>
    <caption>Student Grades</caption>
    <tr>
        <th>Name</th>
        <th>Grade</th>
    </tr>
    <tr>
        <td>Alice</td>
        <td>A</td>
    </tr>
</table>
```

## Table Attributes

### Column Span

Make a cell span multiple columns:

```html
<table>
    <tr>
        <th colspan="2">Name</th>
        <th>Age</th>
    </tr>
    <tr>
        <td>John</td>
        <td>Doe</td>
        <td>30</td>
    </tr>
</table>
```

### Row Span

Make a cell span multiple rows:

```html
<table>
    <tr>
        <th rowspan="2">Name</th>
        <th>Q1</th>
    </tr>
    <tr>
        <th>Q2</th>
    </tr>
    <tr>
        <td>John</td>
        <td>100</td>
        <td>95</td>
    </tr>
</table>
```

## Complete Examples

### Navigation Menu with Lists

```html
<nav>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a>
            <ul>
                <li><a href="team.html">Team</a></li>
                <li><a href="history.html">History</a></li>
            </ul>
        </li>
        <li><a href="contact.html">Contact</a></li>
    </ul>
</nav>
```

### Product Comparison Table

```html
<table>
    <caption>Product Comparison</caption>
    <thead>
        <tr>
            <th>Feature</th>
            <th>Basic</th>
            <th>Pro</th>
            <th>Enterprise</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Price</td>
            <td>$9/month</td>
            <td>$29/month</td>
            <td>$99/month</td>
        </tr>
        <tr>
            <td>Users</td>
            <td>1</td>
            <td>5</td>
            <td>Unlimited</td>
        </tr>
        <tr>
            <td>Storage</td>
            <td>10 GB</td>
            <td>100 GB</td>
            <td>1 TB</td>
        </tr>
    </tbody>
</table>
```

### Complete Page Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lists and Tables</title>
</head>
<body>
    <h1>My Website</h1>
    
    <nav>
        <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#products">Products</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>
    
    <section id="products">
        <h2>Our Products</h2>
        <ul>
            <li>Web Development</li>
            <li>Mobile Apps</li>
            <li>Data Analysis</li>
        </ul>
    </section>
    
    <section id="pricing">
        <h2>Pricing</h2>
        <table>
            <thead>
                <tr>
                    <th>Plan</th>
                    <th>Price</th>
                    <th>Features</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Basic</td>
                    <td>$9/month</td>
                    <td>5 projects</td>
                </tr>
                <tr>
                    <td>Pro</td>
                    <td>$29/month</td>
                    <td>Unlimited projects</td>
                </tr>
            </tbody>
        </table>
    </section>
</body>
</html>
```

## Best Practices

### For Lists

1. **Use semantic lists:** Use lists for actual list content, not just styling
2. **Keep items concise:** List items should be brief
3. **Use nested lists** for hierarchical information
4. **Use description lists** for term-definition pairs

### For Tables

1. **Use headers:** Always include `<th>` for column headers
2. **Use table sections:** Organize with `<thead>`, `<tbody>`, `<tfoot>`
3. **Add captions:** Help users understand the table
4. **Keep it simple:** Complex tables can be hard to read
5. **Consider accessibility:** Use proper headers and structure

!!! warning "Don't Use Tables for Layout"
    Tables are for data, not page layout. Use CSS for layout instead.

## Common Mistakes

### 1. Missing List Item Tags

```html
<!-- ❌ Wrong -->
<ul>
    Item one
    Item two
</ul>

<!-- ✅ Correct -->
<ul>
    <li>Item one</li>
    <li>Item two</li>
</ul>
```

### 2. Using Tables for Layout

```html
<!-- ❌ Wrong (using table for page layout) -->
<table>
    <tr>
        <td>Sidebar</td>
        <td>Main content</td>
    </tr>
</table>

<!-- ✅ Correct (use CSS for layout) -->
<div class="sidebar">Sidebar</div>
<div class="main">Main content</div>
```

### 3. Missing Table Headers

```html
<!-- ❌ Wrong -->
<table>
    <tr>
        <td>Name</td>
        <td>Age</td>
    </tr>
</table>

<!-- ✅ Correct -->
<table>
    <tr>
        <th>Name</th>
        <th>Age</th>
    </tr>
</table>
```

## Practice Exercise

Create an HTML page with:

1. An unordered list with at least 5 items
2. A nested list (list within a list)
3. An ordered list with custom numbering
4. A description list with 3 term-definition pairs
5. A table with:
   - Headers
   - At least 3 rows of data
   - A caption
   - Table sections (thead, tbody)

## What's Next?

Now that you can organize data, learn to:

- **Create Forms** - Collect user input
- **Use Semantic HTML** - Modern HTML5 elements
- **Add Multimedia** - Audio and video elements
- **Structure Pages** - Layout and organization

---

**Previous Tutorial:** [Links and Images](04_links_and_images.md)  
**Next Tutorial:** [Forms](06_forms.md)

