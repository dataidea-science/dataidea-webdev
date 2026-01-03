# Links and Images

Learn how to create hyperlinks and add images to your web pages - essential skills for building connected, visual websites.

## Creating Links

Links connect web pages together. They're created using the `<a>` (anchor) tag.

### Basic Link Syntax

```html
<a href="https://www.example.com">Click here</a>
```

- `<a>` - Anchor tag (creates the link)
- `href` - Hypertext reference (the URL to link to)
- Text between tags - What users see and click

### Link to External Websites

```html
<a href="https://www.google.com">Visit Google</a>
<a href="https://github.com">Go to GitHub</a>
```

!!! tip "Always Include https://"
    For external links, always include the full URL starting with `https://` or `http://`.

### Link to Other Pages on Your Site

```html
<!-- Link to a page in the same folder -->
<a href="about.html">About Us</a>

<!-- Link to a page in a subfolder -->
<a href="pages/contact.html">Contact</a>

<!-- Link to a page in a parent folder -->
<a href="../index.html">Home</a>
```

### Relative vs Absolute Paths

**Absolute Path:**
```html
<a href="https://www.example.com/page.html">Link</a>
```

**Relative Path:**
```html
<a href="page.html">Link</a>
```

Relative paths are relative to the current file's location.

### Link to Sections on the Same Page

First, add an `id` to the target element:

```html
<h2 id="section1">Section One</h2>
<p>Content here...</p>
```

Then link to it using `#`:

```html
<a href="#section1">Go to Section One</a>
```

### Link to Email Addresses

```html
<a href="mailto:contact@example.com">Send Email</a>
```

Clicking this opens the user's email client.

### Link to Phone Numbers

```html
<a href="tel:+1234567890">Call Us</a>
```

On mobile devices, this allows users to call directly.

## Link Attributes

### Open Link in New Tab

```html
<a href="https://example.com" target="_blank">Open in New Tab</a>
```

The `target="_blank"` attribute opens the link in a new browser tab.

!!! tip "Add rel for Security"
    When using `target="_blank"`, add `rel="noopener noreferrer"` for security:
    ```html
    <a href="https://example.com" target="_blank" rel="noopener noreferrer">Link</a>
    ```

### Link Titles (Tooltips)

```html
<a href="https://example.com" title="Visit our homepage">Home</a>
```

Hovering over the link shows a tooltip with the title.

### Download Links

```html
<a href="document.pdf" download>Download PDF</a>
```

This prompts the user to download the file instead of opening it.

## Styling Links

Links have different states you can style with CSS:

- **Normal:** Unvisited link
- **Visited:** Previously visited link
- **Hover:** When mouse is over the link
- **Active:** When link is being clicked

## Adding Images

Images are added using the `<img>` tag. This is a self-closing tag (no closing tag needed).

### Basic Image Syntax

```html
<img src="image.jpg" alt="Description of image">
```

- `src` - Source (path to the image file)
- `alt` - Alternative text (required for accessibility)

### Image from Same Folder

```html
<img src="photo.jpg" alt="A beautiful sunset">
```

### Image from Subfolder

```html
<img src="images/logo.png" alt="Company logo">
```

### Image from External URL

```html
<img src="https://example.com/image.jpg" alt="External image">
```

!!! warning "Use External Images Carefully"
    External images may break if the source website changes or removes them. Always have permission to use external images.

## Image Attributes

### Alt Text (Required)

```html
<img src="cat.jpg" alt="A fluffy orange cat sitting on a windowsill">
```

**Why alt text matters:**
- Screen readers use it for visually impaired users
- Shows if image fails to load
- Helps with SEO (search engine optimization)

!!! tip "Write Descriptive Alt Text"
    Describe what's in the image, not just "image" or "photo."

### Image Dimensions

```html
<img src="photo.jpg" alt="Photo" width="500" height="300">
```

Or use CSS for better control (recommended):

```html
<img src="photo.jpg" alt="Photo" style="width: 500px; height: 300px;">
```

### Image Titles

```html
<img src="photo.jpg" alt="Photo" title="This is a tooltip">
```

Hovering over the image shows the title.

## Image Formats

Common web image formats:

| Format | Best For | File Extension |
|--------|----------|----------------|
| **JPEG/JPG** | Photos, complex images | `.jpg`, `.jpeg` |
| **PNG** | Graphics with transparency | `.png` |
| **GIF** | Simple animations | `.gif` |
| **SVG** | Scalable vector graphics | `.svg` |
| **WebP** | Modern, optimized images | `.webp` |

## Combining Links and Images

You can make an image clickable by wrapping it in a link:

```html
<a href="https://example.com">
    <img src="logo.png" alt="Company logo">
</a>
```

### Image as a Link with Text

```html
<a href="product.html">
    <img src="product.jpg" alt="Product image">
    <p>View Product</p>
</a>
```

## Figure and Figcaption

For images with captions, use `<figure>` and `<figcaption>`:

```html
<figure>
    <img src="landscape.jpg" alt="Mountain landscape">
    <figcaption>A beautiful mountain landscape at sunset.</figcaption>
</figure>
```

## Complete Examples

### Navigation Menu with Links

```html
<nav>
    <a href="index.html">Home</a>
    <a href="about.html">About</a>
    <a href="contact.html">Contact</a>
    <a href="https://github.com" target="_blank" rel="noopener noreferrer">GitHub</a>
</nav>
```

### Image Gallery

```html
<figure>
    <img src="photo1.jpg" alt="Photo 1" width="300">
    <figcaption>First photo</figcaption>
</figure>

<figure>
    <img src="photo2.jpg" alt="Photo 2" width="300">
    <figcaption>Second photo</figcaption>
</figure>
```

### Complete Page Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Links and Images</title>
</head>
<body>
    <h1>My Website</h1>
    
    <nav>
        <a href="#home">Home</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
    </nav>
    
    <section id="home">
        <h2>Welcome</h2>
        <img src="welcome.jpg" alt="Welcome banner">
        <p>Visit our <a href="https://example.com">partner website</a>.</p>
    </section>
    
    <section id="about">
        <h2>About Us</h2>
        <figure>
            <img src="team.jpg" alt="Our team">
            <figcaption>Our amazing team</figcaption>
        </figure>
    </section>
    
    <section id="contact">
        <h2>Contact</h2>
        <p>Email us at <a href="mailto:contact@example.com">contact@example.com</a></p>
    </section>
</body>
</html>
```

## Best Practices

### For Links

1. **Use descriptive text:** "Click here" is not helpful
2. **Make links obvious:** Users should know something is clickable
3. **Test all links:** Make sure they work
4. **Use relative paths** for internal links
5. **Add `rel="noopener noreferrer"`** when using `target="_blank"`

### For Images

1. **Always include alt text:** Required for accessibility
2. **Optimize images:** Compress large images before uploading
3. **Use appropriate formats:** JPEG for photos, PNG for graphics
4. **Specify dimensions:** Helps page load faster
5. **Don't use images for text:** Use actual text instead

## Common Mistakes

### 1. Missing Alt Text

```html
<!-- ❌ Wrong -->
<img src="photo.jpg">

<!-- ✅ Correct -->
<img src="photo.jpg" alt="Description">
```

### 2. Broken Image Paths

```html
<!-- ❌ Wrong (if image is in images folder) -->
<img src="photo.jpg" alt="Photo">

<!-- ✅ Correct -->
<img src="images/photo.jpg" alt="Photo">
```

### 3. Non-descriptive Link Text

```html
<!-- ❌ Wrong -->
<a href="about.html">Click here</a>

<!-- ✅ Correct -->
<a href="about.html">Learn more about us</a>
```

## Practice Exercise

Create an HTML page with:

1. A navigation menu with at least 3 links
2. An external link that opens in a new tab
3. A link to an email address
4. At least 3 images with proper alt text
5. One image wrapped in a link
6. A figure with an image and caption

## What's Next?

Now that you can add links and images, learn to:

- **Create Lists** - Organize information
- **Build Tables** - Display structured data
- **Create Forms** - Collect user input
- **Use Semantic HTML** - Modern best practices

---

**Previous Tutorial:** [Text Formatting and Headings](03_text_formatting.md)  
**Next Tutorial:** [Lists and Tables](05_lists_and_tables.md)

