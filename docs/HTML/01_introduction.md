![Photo by DATAIDEA](../assets/banner_DATAIDEA.png)

# Introduction to HTML

HTML (HyperText Markup Language) is the foundation of every web page. It's the standard language used to create and structure content on the web.

## What is HTML?

HTML is a markup language that uses tags to define the structure and content of web pages. It tells browsers how to display text, images, links, and other elements.

### Key Characteristics

- **Markup Language:** Uses tags (like `<p>`, `<div>`, `<h1>`) to structure content
- **Not a Programming Language:** HTML describes structure, not logic
- **Universal:** Works in all browsers (Chrome, Firefox, Safari, Edge)
- **Foundation:** Every website uses HTML as its base

## Why Learn HTML?

### Essential for Web Development

- **First Step:** HTML is the starting point for all web development
- **Required Knowledge:** You can't build websites without understanding HTML
- **Works Everywhere:** HTML works on desktop, mobile, and tablet devices
- **Foundation for CSS & JavaScript:** HTML provides the structure that CSS styles and JavaScript enhances

### Career Opportunities

- **Frontend Developer:** Build user interfaces
- **Full-Stack Developer:** Work on both frontend and backend
- **Web Designer:** Create visually appealing websites
- **Content Manager:** Understand how web content is structured

## How HTML Works

HTML documents are plain text files with a `.html` extension. When you open an HTML file in a browser, the browser reads the HTML tags and displays the content according to those tags.

### Simple Example

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First Page</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is my first web page.</p>
</body>
</html>
```

When viewed in a browser, this displays:
- A page title "My First Page" (in the browser tab)
- A large heading "Hello, World!"
- A paragraph with "This is my first web page."

## HTML Tags Explained

HTML uses **tags** to mark up content. Tags are keywords surrounded by angle brackets:

- **Opening Tag:** `<tagname>` - starts an element
- **Closing Tag:** `</tagname>` - ends an element
- **Content:** The text or other elements between the tags

### Example

```html
<p>This is a paragraph.</p>
```

- `<p>` is the opening tag
- `This is a paragraph.` is the content
- `</p>` is the closing tag

### Self-Closing Tags

Some tags don't need closing tags because they don't contain content:

```html
<img src="photo.jpg" alt="A photo">
<br>
<hr>
```

## Basic HTML Document Structure

Every HTML document follows this basic structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
</head>
<body>
    <!-- Your content goes here -->
</body>
</html>
```

### Structure Breakdown

1. **`<!DOCTYPE html>`** - Declares this is an HTML5 document
2. **`<html>`** - Root element that contains everything
3. **`<head>`** - Contains metadata (not visible on the page)
4. **`<body>`** - Contains visible content

## HTML Versions

| Version | Year | Description |
|---------|------|-------------|
| HTML 4.01 | 1999 | Last version before HTML5 |
| XHTML | 2000 | Stricter version of HTML |
| **HTML5** | 2014 | Current standard (what we'll learn) |

!!! tip "We'll Use HTML5"
    All modern tutorials and examples use HTML5, which is the current standard and what you should learn.

## Setting Up Your Environment

### What You Need

1. **Text Editor:** Any plain text editor works
   - **Recommended:** VS Code, Sublime Text, Atom, or Notepad++
   - **Avoid:** Word processors (Word, Google Docs) - they add formatting

2. **Web Browser:** Any modern browser
   - Chrome, Firefox, Safari, or Edge

### Creating Your First HTML File

1. Open your text editor
2. Create a new file
3. Save it with a `.html` extension (e.g., `index.html`)
4. Open it in your browser

### Quick Test

Create a file called `test.html` with this content:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Test Page</title>
</head>
<body>
    <h1>It Works!</h1>
    <p>If you can see this, HTML is working correctly.</p>
</body>
</html>
```

Save the file and double-click it to open in your browser.

## HTML vs CSS vs JavaScript

Understanding the relationship between these three technologies:

| Technology | Purpose | Analogy |
|------------|---------|---------|
| **HTML** | Structure and content | The skeleton of a house |
| **CSS** | Styling and appearance | The paint and decoration |
| **JavaScript** | Interactivity and behavior | The electricity and plumbing |

### Example

```html
<!-- HTML: Structure -->
<div id="box">
    <p>Click me!</p>
</div>

<!-- CSS: Styling (in a separate file or <style> tag) -->
<style>
    #box {
        background-color: blue;
        color: white;
        padding: 20px;
    }
</style>

<!-- JavaScript: Behavior (in a separate file or <script> tag) -->
<script>
    document.getElementById('box').addEventListener('click', function() {
        alert('You clicked the box!');
    });
</script>
```

## Best Practices

1. **Use Semantic HTML:** Choose tags that describe the content's meaning
2. **Write Clean Code:** Proper indentation and organization
3. **Validate Your HTML:** Use validators to check for errors
4. **Keep It Simple:** Start simple, add complexity gradually
5. **Test in Multiple Browsers:** Ensure compatibility

## Common HTML Elements Overview

Here are some elements you'll learn about:

- **Headings:** `<h1>` to `<h6>` - Different heading levels
- **Paragraphs:** `<p>` - Text blocks
- **Links:** `<a>` - Hyperlinks to other pages
- **Images:** `<img>` - Display pictures
- **Lists:** `<ul>`, `<ol>`, `<li>` - Bulleted and numbered lists
- **Tables:** `<table>`, `<tr>`, `<td>` - Structured data
- **Forms:** `<form>`, `<input>` - User input
- **Containers:** `<div>`, `<span>` - Grouping elements

## Resources

- [MDN Web Docs - HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) - Comprehensive HTML reference
- [W3Schools HTML Tutorial](https://www.w3schools.com/html/) - Beginner-friendly tutorials
- [HTML Validator](https://validator.w3.org/) - Check your HTML for errors
- [Can I Use](https://caniuse.com/) - Browser compatibility checker

## What's Next?

In the following tutorials, you'll learn:

1. **Basic HTML Structure** - Document structure, head, body, and essential tags
2. **Text Formatting** - Headings, paragraphs, text styling, and semantic elements
3. **Links and Images** - Creating hyperlinks and adding images to your pages
4. **Lists and Tables** - Organizing content with lists and displaying data in tables
5. **Forms** - Creating interactive forms for user input
6. **Semantic HTML** - Modern HTML5 elements and best practices

!!! success "You're Ready!"
    You now understand what HTML is and why it's important. Let's start building your first web pages!

---

**Next Tutorial:** [Basic HTML Structure](02_basic_structure.md)

