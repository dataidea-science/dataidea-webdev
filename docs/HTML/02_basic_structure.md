# Basic HTML Structure

Learn the fundamental structure of an HTML document and the essential elements every web page needs.

## The HTML Document Template

Every HTML document starts with this basic template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document Title</title>
</head>
<body>
    <!-- Page content goes here -->
</body>
</html>
```

Let's break down each part:

## DOCTYPE Declaration

```html
<!DOCTYPE html>
```

- **Purpose:** Tells the browser this is an HTML5 document
- **Location:** Must be the very first line
- **Why:** Ensures the browser renders your page correctly
- **Note:** This is the only tag that doesn't need a closing tag

!!! tip "Always Include DOCTYPE"
    Without `<!DOCTYPE html>`, browsers may render your page in "quirks mode," which can cause display issues.

## The `<html>` Element

```html
<html lang="en">
    <!-- All other HTML goes inside here -->
</html>
```

- **Purpose:** Root element that wraps all HTML content
- **`lang` Attribute:** Specifies the language (e.g., "en" for English, "es" for Spanish)
- **Why `lang` matters:** Helps screen readers and search engines understand your content

### Common Language Codes

```html
<html lang="en">  <!-- English -->
<html lang="es">  <!-- Spanish -->
<html lang="fr">  <!-- French -->
<html lang="de">  <!-- German -->
<html lang="zh">  <!-- Chinese -->
```

## The `<head>` Section

The `<head>` contains metadata - information about your page that isn't visible to users.

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Web Page</title>
</head>
```

### Character Encoding

```html
<meta charset="UTF-8">
```

- **Purpose:** Tells the browser which character set to use
- **UTF-8:** Supports all characters from all languages
- **Why it matters:** Without this, special characters might display incorrectly

### Viewport Meta Tag

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- **Purpose:** Makes your page responsive on mobile devices
- **`width=device-width`:** Sets page width to match device width
- **`initial-scale=1.0`:** Sets initial zoom level
- **Why it matters:** Without this, mobile browsers may zoom out, making text tiny

### The `<title>` Tag

```html
<title>My Web Page</title>
```

- **Purpose:** Sets the page title shown in:
  - Browser tab
  - Bookmarks
  - Search engine results
- **Best Practice:** Keep titles descriptive and under 60 characters

### Other Common Head Elements

```html
<head>
    <!-- Character encoding -->
    <meta charset="UTF-8">
    
    <!-- Viewport for mobile -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- Page description (for search engines) -->
    <meta name="description" content="A brief description of your page">
    
    <!-- Page title -->
    <title>My Web Page</title>
    
    <!-- Link to CSS file -->
    <link rel="stylesheet" href="styles.css">
    
    <!-- Link to favicon (small icon in browser tab) -->
    <link rel="icon" href="favicon.ico">
</head>
```

## The `<body>` Section

The `<body>` contains all visible content on your web page.

```html
<body>
    <h1>Welcome to My Website</h1>
    <p>This is where your content goes.</p>
</body>
```

Everything users see - text, images, links, buttons - goes inside the `<body>` tag.

## Complete Example

Here's a complete, properly structured HTML document:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="A simple example of HTML structure">
    <title>HTML Structure Example</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is a properly structured HTML document.</p>
</body>
</html>
```

## HTML Comments

Comments are notes in your code that browsers ignore. They're useful for documentation:

```html
<!-- This is a comment. It won't appear on the page. -->

<!-- 
    This is a multi-line comment.
    You can write multiple lines here.
-->

<h1>This heading will be visible</h1>
<!-- This comment explains what the heading is for -->
```

### When to Use Comments

- Explain complex code
- Mark sections of your page
- Temporarily disable code
- Leave notes for yourself or other developers

## Indentation and Formatting

Proper indentation makes your code readable:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Example</title>
</head>
<body>
    <h1>Main Heading</h1>
    <div>
        <p>Paragraph inside a div.</p>
        <ul>
            <li>List item 1</li>
            <li>List item 2</li>
        </ul>
    </div>
</body>
</html>
```

### Indentation Rules

- Use consistent spacing (2 or 4 spaces, or tabs)
- Indent nested elements
- Align closing tags with their opening tags
- Keep related elements together

## Common Mistakes to Avoid

### 1. Missing DOCTYPE

```html
<!-- ❌ Wrong -->
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <p>Content</p>
</body>
</html>

<!-- ✅ Correct -->
<!DOCTYPE html>
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <p>Content</p>
</body>
</html>
```

### 2. Forgetting to Close Tags

```html
<!-- ❌ Wrong -->
<p>This is a paragraph
<p>This is another paragraph

<!-- ✅ Correct -->
<p>This is a paragraph</p>
<p>This is another paragraph</p>
```

### 3. Incorrect Nesting

```html
<!-- ❌ Wrong -->
<p>This is <strong>bold text</p></strong>

<!-- ✅ Correct -->
<p>This is <strong>bold text</strong></p>
```

### 4. Missing Quotes in Attributes

```html
<!-- ❌ Wrong -->
<html lang=en>
<meta charset=UTF-8>

<!-- ✅ Correct -->
<html lang="en">
<meta charset="UTF-8">
```

## Practice Exercise

Create an HTML file with the following structure:

1. Proper DOCTYPE declaration
2. HTML element with `lang="en"`
3. Head section with:
   - Character encoding
   - Viewport meta tag
   - A descriptive title
4. Body section with:
   - A main heading
   - A paragraph
   - A comment explaining your code

Save it as `structure.html` and open it in your browser.

## Validating Your HTML

Always validate your HTML to catch errors:

1. **Online Validator:** Visit [validator.w3.org](https://validator.w3.org/)
2. **Upload your file** or paste your code
3. **Check for errors** and fix them

!!! tip "Validate Regularly"
    Validating your HTML helps you learn correct syntax and catch mistakes early.

## What's Next?

Now that you understand HTML structure, you're ready to add content:

- **Headings and Paragraphs** - Basic text elements
- **Text Formatting** - Making text bold, italic, and more
- **Links and Images** - Connecting pages and adding visuals
- **Lists** - Organizing information

---

**Previous Tutorial:** [Introduction to HTML](01_introduction.md)  
**Next Tutorial:** [Text Formatting and Headings](03_text_formatting.md)

