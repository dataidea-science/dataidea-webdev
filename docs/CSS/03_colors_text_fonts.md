![Photo by DATAIDEA](../assets/banner_DATAIDEA.png)

# Colors, Text, and Fonts

Learn how to control colors, typography, and text styling to make your web pages visually appealing and readable.

## Colors

CSS offers multiple ways to specify colors.

### Color Keywords

Simple color names:

```css
p {
    color: red;
    background-color: blue;
}
```

Common keywords: `red`, `blue`, `green`, `black`, `white`, `gray`, `yellow`, `orange`, `purple`, `pink`, `cyan`, `magenta`.

<div class="css-example" style="border: 2px solid #444; border-radius: 8px; padding: 20px; margin: 20px 0; background-color: #1e1e1e;">
<h3 style="margin-top: 0; color: #fff;">Try it yourself:</h3>
<div style="background-color: #fff; padding: 20px; border-radius: 4px;">
<style>
.css-example .color-keywords p {
    color: red;
    background-color: blue;
    padding: 10px;
    color: white;
}
</style>
<div class="color-keywords">
<p>This text uses color keywords - red text on blue background</p>
</div>
</div>
</div>

### Hexadecimal Colors

Most common method. Uses 6 hexadecimal digits:

```css
h1 {
    color: #FF0000; /* Red */
    background-color: #0000FF; /* Blue */
}

p {
    color: #333333; /* Dark gray */
}
```

**Format:** `#RRGGBB`
- `#FF0000` = Red (FF red, 00 green, 00 blue)
- `#00FF00` = Green
- `#0000FF` = Blue
- `#000000` = Black
- `#FFFFFF` = White

**Shorthand:** For colors like `#FFCC00`, you can use `#FC0`.

<div class="css-example" style="border: 2px solid #444; border-radius: 8px; padding: 20px; margin: 20px 0; background-color: #1e1e1e;">
<h3 style="margin-top: 0; color: #fff;">Try it yourself:</h3>
<div style="background-color: #fff; padding: 20px; border-radius: 4px;">
<style>
.css-example .hex-demo h1 {
    color: #FF0000;
    background-color: #0000FF;
    padding: 10px;
    color: white;
}
.css-example .hex-demo p {
    color: #333333;
}
</style>
<div class="hex-demo">
<h1>Red text on blue background (#FF0000 on #0000FF)</h1>
<p>Dark gray text using #333333</p>
</div>
</div>
</div>

### RGB Colors

Red, Green, Blue values (0-255):

```css
h1 {
    color: rgb(255, 0, 0); /* Red */
    background-color: rgb(0, 0, 255); /* Blue */
}
```

### RGBA Colors

RGB with alpha (transparency) channel (0-1):

```css
div {
    background-color: rgba(0, 0, 255, 0.5); /* Semi-transparent blue */
    color: rgba(255, 0, 0, 0.8); /* 80% opaque red */
}
```

<div class="css-example" style="border: 2px solid #444; border-radius: 8px; padding: 20px; margin: 20px 0; background-color: #1e1e1e;">
<h3 style="margin-top: 0; color: #fff;">Try it yourself:</h3>
<div style="background-color: #fff; padding: 20px; border-radius: 4px; background-image: linear-gradient(45deg, #ccc 25%, transparent 25%), linear-gradient(-45deg, #ccc 25%, transparent 25%), linear-gradient(45deg, transparent 75%, #ccc 75%), linear-gradient(-45deg, transparent 75%, #ccc 75%); background-size: 20px 20px; background-position: 0 0, 0 10px, 10px -10px, -10px 0px;">
<style>
.css-example .rgba-demo div {
    background-color: rgba(0, 0, 255, 0.5);
    color: rgba(255, 0, 0, 0.8);
    padding: 15px;
    border-radius: 4px;
    margin: 10px 0;
}
</style>
<div class="rgba-demo">
<div>Semi-transparent blue background (50% opacity) with red text (80% opacity). Notice the checkered pattern shows through!</div>
</div>
</div>
</div>

### HSL Colors

Hue, Saturation, Lightness:

```css
p {
    color: hsl(0, 100%, 50%); /* Red */
    background-color: hsl(240, 100%, 50%); /* Blue */
}
```

- **Hue:** 0-360 (color wheel)
- **Saturation:** 0-100% (intensity)
- **Lightness:** 0-100% (brightness)

### HSLA Colors

HSL with alpha:

```css
div {
    background-color: hsla(240, 100%, 50%, 0.5);
}
```

## Text Color

Control text color with the `color` property:

```css
h1 {
    color: #333;
}

p {
    color: rgb(100, 100, 100);
}

.error {
    color: red;
}
```

## Background Color

Set background colors:

```css
body {
    background-color: #f5f5f5;
}

.header {
    background-color: blue;
}

.highlight {
    background-color: yellow;
}
```

## Typography Properties

### Font Family

Specify which font to use:

```css
p {
    font-family: Arial, sans-serif;
}
```

**Font Stack:** List multiple fonts. Browser uses the first available.

**Common Font Stacks:**
```css
/* Sans-serif (modern, clean) */
font-family: Arial, Helvetica, sans-serif;
font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;

/* Serif (traditional, readable) */
font-family: Georgia, 'Times New Roman', serif;

/* Monospace (code, fixed-width) */
font-family: 'Courier New', Courier, monospace;
```

**Web Fonts:**
```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

h1 {
    font-family: 'Roboto', sans-serif;
}
```

### Font Size

Control text size:

```css
h1 {
    font-size: 32px;
}

p {
    font-size: 16px;
}

.small {
    font-size: 12px;
}
```

**Units:**
- `px` - Pixels (absolute)
- `em` - Relative to parent (1em = parent's font size)
- `rem` - Relative to root (1rem = root font size)
- `%` - Percentage of parent
- `vw/vh` - Viewport width/height

```css
/* Responsive sizing */
h1 {
    font-size: 2rem; /* 2x root font size */
}

p {
    font-size: 1em; /* Same as parent */
}
```

### Font Weight

Control boldness:

```css
p {
    font-weight: normal; /* 400 */
}

strong {
    font-weight: bold; /* 700 */
}

.light {
    font-weight: 300;
}

.heavy {
    font-weight: 900;
}
```

**Values:** `normal`, `bold`, `100-900` (100=thin, 400=normal, 700=bold, 900=black)

### Font Style

Control italic text:

```css
p {
    font-style: normal;
}

em {
    font-style: italic;
}

.oblique {
    font-style: oblique;
}
```

### Font Shorthand

Combine multiple font properties:

```css
p {
    font: italic bold 16px/1.5 Arial, sans-serif;
}
```

**Order:** `style weight size/line-height family`

## Text Properties

### Text Alignment

```css
p {
    text-align: left; /* Default */
}

.center {
    text-align: center;
}

.right {
    text-align: right;
}

.justify {
    text-align: justify;
}
```

<div class="css-example" style="border: 2px solid #444; border-radius: 8px; padding: 20px; margin: 20px 0; background-color: #1e1e1e;">
<h3 style="margin-top: 0; color: #fff;">Try it yourself:</h3>
<div style="background-color: #fff; padding: 20px; border-radius: 4px;">
<style>
.css-example .alignment-demo .left {
    text-align: left;
}
.css-example .alignment-demo .center {
    text-align: center;
}
.css-example .alignment-demo .right {
    text-align: right;
}
.css-example .alignment-demo .justify {
    text-align: justify;
}
</style>
<div class="alignment-demo">
<p class="left">This text is aligned left (default)</p>
<p class="center">This text is centered</p>
<p class="right">This text is aligned right</p>
<p class="justify">This text is justified. It spreads evenly across the width of the container, creating a clean edge on both sides.</p>
</div>
</div>
</div>

### Text Decoration

```css
a {
    text-decoration: none; /* Remove underline */
}

.underline {
    text-decoration: underline;
}

.line-through {
    text-decoration: line-through;
}
```

### Text Transform

```css
.uppercase {
    text-transform: uppercase;
}

.lowercase {
    text-transform: lowercase;
}

.capitalize {
    text-transform: capitalize;
}
```

### Letter Spacing

```css
h1 {
    letter-spacing: 2px;
}

.tight {
    letter-spacing: -1px;
}
```

### Word Spacing

```css
p {
    word-spacing: 5px;
}
```

### Line Height

Control spacing between lines:

```css
p {
    line-height: 1.5; /* 1.5x font size */
}

.tight {
    line-height: 1.2;
}

.spacious {
    line-height: 2;
}
```

### Text Shadow

Add shadow to text:

```css
h1 {
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
```

**Format:** `offset-x offset-y blur color`

<div class="css-example" style="border: 2px solid #444; border-radius: 8px; padding: 20px; margin: 20px 0; background-color: #1e1e1e;">
<h3 style="margin-top: 0; color: #fff;">Try it yourself:</h3>
<div style="background-color: #fff; padding: 20px; border-radius: 4px;">
<style>
.css-example .shadow-demo h1 {
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    font-size: 32px;
    margin: 10px 0;
}
</style>
<div class="shadow-demo">
<h1>Text with shadow effect</h1>
</div>
</div>
</div>

## Complete Typography Example

```css
/* Body text */
body {
    font-family: 'Helvetica Neue', Arial, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
}

/* Headings */
h1 {
    font-family: Georgia, serif;
    font-size: 2.5rem;
    font-weight: bold;
    color: #2c3e50;
    text-align: center;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

h2 {
    font-size: 2rem;
    color: #34495e;
    margin-top: 2em;
}

/* Paragraphs */
p {
    font-size: 1rem;
    line-height: 1.8;
    color: #555;
    margin-bottom: 1em;
}

/* Links */
a {
    color: #3498db;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}

/* Special text */
.highlight {
    background-color: #ffeb3b;
    padding: 2px 4px;
}

.error {
    color: #e74c3c;
    font-weight: bold;
}
```

## Web Fonts

Use custom fonts from Google Fonts or other sources:

### Google Fonts

1. **Import in CSS:**
```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
```

2. **Use the font:**
```css
body {
    font-family: 'Roboto', sans-serif;
}
```

### Self-Hosted Fonts

```css
@font-face {
    font-family: 'MyFont';
    src: url('myfont.woff2') format('woff2'),
         url('myfont.woff') format('woff');
}

body {
    font-family: 'MyFont', sans-serif;
}
```

## Best Practices

1. **Limit Font Families:** Use 2-3 fonts maximum
2. **Choose Readable Fonts:** Sans-serif for body, serif for headings
3. **Maintain Contrast:** Ensure text is readable on backgrounds
4. **Use Relative Sizes:** `rem` or `em` for responsive design
5. **Set Line Height:** 1.5-1.8 for comfortable reading
6. **Test Readability:** Ensure text is easy to read

## Color Contrast

Ensure sufficient contrast for accessibility:

- **WCAG AA:** 4.5:1 for normal text, 3:1 for large text
- **WCAG AAA:** 7:1 for normal text, 4.5:1 for large text

```css
/* Good contrast */
p {
    color: #333; /* Dark gray */
    background-color: #fff; /* White */
}

/* Poor contrast - avoid */
p {
    color: #ccc; /* Light gray */
    background-color: #fff; /* White */
}
```

## Common Mistakes

### 1. Too Many Fonts

```css
/* ❌ Wrong */
h1 { font-family: Font1; }
h2 { font-family: Font2; }
p { font-family: Font3; }
span { font-family: Font4; }

/* ✅ Correct */
h1, h2 { font-family: 'Heading Font', serif; }
p, span { font-family: 'Body Font', sans-serif; }
```

### 2. Poor Color Contrast

```css
/* ❌ Wrong */
p {
    color: #f0f0f0;
    background-color: #ffffff;
}

/* ✅ Correct */
p {
    color: #333333;
    background-color: #ffffff;
}
```

### 3. Inconsistent Sizing

```css
/* ❌ Wrong */
h1 { font-size: 24px; }
h2 { font-size: 18px; }
h3 { font-size: 15px; }

/* ✅ Correct */
h1 { font-size: 2.5rem; }
h2 { font-size: 2rem; }
h3 { font-size: 1.5rem; }
```

## Practice Exercise

Create CSS that:

1. Sets body text to a readable sans-serif font, 16px, with 1.6 line height
2. Styles h1 with a serif font, 2.5rem, centered, with a subtle text shadow
3. Makes links blue with no underline, but underline on hover
4. Creates a `.highlight` class with yellow background
5. Styles error messages in red, bold
6. Uses a Google Font for headings

## What's Next?

Now that you can style text, learn to:

- **Understand the Box Model** - How spacing and sizing work
- **Control Layout** - Position and arrange elements
- **Use Flexbox** - Modern layout system
- **Create Responsive Designs** - Work on all screen sizes

---

**Previous Tutorial:** [CSS Syntax and Selectors](02_syntax_and_selectors.md)  
**Next Tutorial:** [Box Model and Layout](04_box_model_layout.md)


