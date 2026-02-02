![Photo by DATAIDEA](../assets/banner_DATAIDEA.png)

# Text Formatting and Headings

Learn how to structure and format text content in HTML using headings, paragraphs, and text formatting tags.

## Headings

HTML provides six levels of headings, from `<h1>` (most important) to `<h6>` (least important).

### Heading Levels

```html
<h1>Main Title (Largest)</h1>
<h2>Section Heading</h2>
<h3>Subsection Heading</h3>
<h4>Minor Heading</h4>
<h5>Small Heading</h5>
<h6>Smallest Heading</h6>
```

### Visual Hierarchy

Headings create a visual hierarchy on your page:

```html
<h1>My Website</h1>
    <h2>About Me</h2>
        <h3>Early Life</h3>
        <h3>Education</h3>
    <h2>My Projects</h2>
        <h3>Web Development</h3>
        <h3>Data Science</h3>
```

### Best Practices for Headings

1. **Use `<h1>` Once:** Only one `<h1>` per page (usually the main title)
2. **Don't Skip Levels:** Don't jump from `<h1>` to `<h3>` - use `<h2>` first
3. **Use for Structure:** Headings organize content, not just for styling
4. **Be Descriptive:** Headings should clearly describe the content below

!!! warning "Don't Use Headings for Styling"
    Use headings to structure content, not just to make text bigger. Use CSS for visual styling.

## Paragraphs

The `<p>` tag creates paragraphs of text:

```html
<p>This is a paragraph. It contains multiple sentences and will automatically wrap to fit the width of the container.</p>

<p>This is another paragraph. Paragraphs are separated by blank lines in the browser.</p>
```

### Multiple Paragraphs

```html
<p>First paragraph of text.</p>
<p>Second paragraph of text.</p>
<p>Third paragraph of text.</p>
```

### Line Breaks

Use `<br>` for line breaks within a paragraph:

```html
<p>This is the first line.<br>
This is the second line.<br>
This is the third line.</p>
```

!!! tip "Use `<br>` Sparingly"
    Usually, separate paragraphs with `<p>` tags rather than using `<br>` multiple times.

## Text Formatting Tags

### Bold Text

Two ways to make text bold:

```html
<!-- Strong emphasis (semantic - preferred) -->
<p>This is <strong>important</strong> text.</p>

<!-- Bold (visual only) -->
<p>This is <b>bold</b> text.</p>
```

**Difference:**
- `<strong>` - Indicates importance (semantic meaning)
- `<b>` - Just makes text bold (visual only)

!!! tip "Prefer `<strong>` over `<b>`"
    `<strong>` has semantic meaning and is better for accessibility.

### Italic Text

Two ways to make text italic:

```html
<!-- Emphasis (semantic - preferred) -->
<p>This is <em>emphasized</em> text.</p>

<!-- Italic (visual only) -->
<p>This is <i>italic</i> text.</p>
```

**Difference:**
- `<em>` - Indicates emphasis (semantic meaning)
- `<i>` - Just makes text italic (visual only)

### Combining Formatting

```html
<p>This is <strong><em>bold and italic</em></strong> text.</p>
<p>This is <em><strong>emphasized and important</strong></em> text.</p>
```

### Underline

```html
<p>This is <u>underlined</u> text.</p>
```

!!! warning "Avoid Underlining"
    Underlined text looks like links. Use underlining sparingly, if at all.

### Strikethrough

```html
<p>This is <s>strikethrough</s> text.</p>
<p>This is <del>deleted</del> text.</p>
```

**Difference:**
- `<s>` - Strikethrough for text that's no longer relevant
- `<del>` - Indicates deleted text (often used with `<ins>`)

### Marked/Highlighted Text

```html
<p>This is <mark>highlighted</mark> text.</p>
```

### Subscript and Superscript

```html
<p>H<sub>2</sub>O is water.</p>
<p>E = mc<sup>2</sup></p>
```

## Semantic Text Elements

HTML5 introduced semantic elements that describe the meaning of text:

### Code

```html
<p>Use the <code>console.log()</code> function to print output.</p>
```

For multiple lines of code, use `<pre>` with `<code>`:

```html
<pre><code>
function greet() {
    console.log("Hello, World!");
}
</code></pre>
```

### Keyboard Input

```html
<p>Press <kbd>Ctrl</kbd> + <kbd>C</kbd> to copy.</p>
```

### Sample Output

```html
<p>Your computer says: <samp>File not found</samp></p>
```

### Variables

```html
<p>The variable <var>x</var> equals 5.</p>
```

### Abbreviations

```html
<p><abbr title="HyperText Markup Language">HTML</abbr> is the foundation of web pages.</p>
```

Hovering over "HTML" shows the full expansion.

### Citations

```html
<p>As <cite>Albert Einstein</cite> once said...</p>
<blockquote>
    <p>Imagination is more important than knowledge.</p>
    <cite>— Albert Einstein</cite>
</blockquote>
```

### Definitions

```html
<p><dfn>HTML</dfn> stands for HyperText Markup Language.</p>
```

### Small Print

```html
<p>Regular text <small>and small print</small>.</p>
```

## Block Quotes

For longer quotations:

```html
<blockquote>
    <p>The only way to do great work is to love what you do.</p>
    <cite>— Steve Jobs</cite>
</blockquote>
```

## Horizontal Rule

The `<hr>` tag creates a horizontal line (often used to separate sections):

```html
<p>Section one content.</p>
<hr>
<p>Section two content.</p>
```

## Complete Example

Here's a complete example using various text formatting:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Text Formatting Example</title>
</head>
<body>
    <h1>My Blog Post</h1>
    
    <h2>Introduction</h2>
    <p>This is a <strong>sample</strong> blog post demonstrating various HTML text formatting options.</p>
    
    <h2>Key Concepts</h2>
    <p>In HTML, we use tags like <code>&lt;p&gt;</code> for paragraphs and <code>&lt;h1&gt;</code> for headings.</p>
    
    <h3>Important Note</h3>
    <p><em>Remember</em> to use semantic HTML elements whenever possible.</p>
    
    <blockquote>
        <p>Good code is its own best documentation.</p>
        <cite>— Steve McConnell</cite>
    </blockquote>
    
    <hr>
    
    <h2>Conclusion</h2>
    <p>For more information, visit the <abbr title="World Wide Web Consortium">W3C</abbr> website.</p>
</body>
</html>
```

## Practice Exercise

Create an HTML page with:

1. A main heading (`<h1>`) for the page title
2. At least two section headings (`<h2>`)
3. Multiple paragraphs with:
   - Bold text using `<strong>`
   - Italic text using `<em>`
   - A code snippet using `<code>`
   - An abbreviation using `<abbr>`
4. A blockquote with a citation
5. A horizontal rule to separate sections

## Common Mistakes

### 1. Using Headings for Size Only

```html
<!-- ❌ Wrong -->
<h1>Normal text</h1>
<h1>More normal text</h1>

<!-- ✅ Correct -->
<h1>Main Title</h1>
<p>Normal text</p>
<p>More normal text</p>
```

### 2. Forgetting to Close Tags

```html
<!-- ❌ Wrong -->
<p>This is <strong>bold text
<p>This is another paragraph

<!-- ✅ Correct -->
<p>This is <strong>bold text</strong></p>
<p>This is another paragraph</p>
```

### 3. Overusing `<br>`

```html
<!-- ❌ Wrong -->
<p>Line one<br><br><br>Line two</p>

<!-- ✅ Correct -->
<p>Line one</p>
<p>Line two</p>
```

## What's Next?

Now that you can format text, learn to:

- **Create Links** - Connect pages together
- **Add Images** - Make your pages visual
- **Build Lists** - Organize information
- **Create Tables** - Display structured data

---

**Previous Tutorial:** [Basic HTML Structure](02_basic_structure.md)  
**Next Tutorial:** [Links and Images](04_links_and_images.md)

