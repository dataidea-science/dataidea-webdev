![Photo by DATAIDEA](../assets/banner_DATAIDEA.png)

# Forms

Learn how to create interactive forms that collect user input - essential for login pages, contact forms, surveys, and more.

## What are Forms?

Forms allow users to submit data to a server. They're used for:
- Login and registration
- Contact forms
- Search boxes
- Surveys and polls
- E-commerce checkout
- And much more

## Basic Form Structure

All forms start with the `<form>` tag:

```html
<form>
    <!-- Form elements go here -->
</form>
```

### Form Attributes

```html
<form action="/submit" method="post">
    <!-- Form content -->
</form>
```

- `action` - Where to send the form data (URL)
- `method` - How to send data (`get` or `post`)

!!! note "Backend Required"
    Forms typically need a backend server to process the data. For now, we'll focus on the HTML structure.

## Text Input

The most common form element for single-line text:

```html
<form>
    <label for="username">Username:</label>
    <input type="text" id="username" name="username">
</form>
```

### Input Attributes

```html
<input type="text" 
       id="username" 
       name="username" 
       placeholder="Enter your username"
       required
       maxlength="20"
       value="default">
```

- `type` - Type of input (text, email, password, etc.)
- `id` - Unique identifier (used with `<label>`)
- `name` - Name sent to server (required for submission)
- `placeholder` - Hint text shown in empty field
- `required` - Field must be filled
- `maxlength` - Maximum characters allowed
- `value` - Default value

## Labels

Labels make forms accessible and user-friendly:

```html
<!-- Method 1: Using 'for' attribute -->
<label for="email">Email:</label>
<input type="email" id="email" name="email">

<!-- Method 2: Wrapping input -->
<label>
    Email:
    <input type="email" name="email">
</label>
```

!!! tip "Always Use Labels"
    Labels improve accessibility and make forms easier to use. Clicking a label focuses its input field.

## Input Types

HTML5 provides many input types for different data:

### Text Inputs

```html
<!-- Single-line text -->
<input type="text" name="name" placeholder="Your name">

<!-- Password (hidden characters) -->
<input type="password" name="password" placeholder="Password">

<!-- Email (validates email format) -->
<input type="email" name="email" placeholder="your@email.com">

<!-- Number -->
<input type="number" name="age" min="0" max="120">

<!-- URL -->
<input type="url" name="website" placeholder="https://example.com">

<!-- Telephone -->
<input type="tel" name="phone" placeholder="123-456-7890">

<!-- Search -->
<input type="search" name="query" placeholder="Search...">
```

### Date and Time

```html
<!-- Date -->
<input type="date" name="birthday">

<!-- Time -->
<input type="time" name="appointment">

<!-- Date and Time -->
<input type="datetime-local" name="event">

<!-- Month -->
<input type="month" name="month">

<!-- Week -->
<input type="week" name="week">
```

### Other Input Types

```html
<!-- Color picker -->
<input type="color" name="favorite-color">

<!-- File upload -->
<input type="file" name="document">

<!-- Range slider -->
<input type="range" name="volume" min="0" max="100" value="50">

<!-- Hidden field (not visible to user) -->
<input type="hidden" name="user-id" value="123">
```

## Textarea

For multi-line text input:

```html
<label for="message">Message:</label>
<textarea id="message" name="message" rows="4" cols="50" placeholder="Enter your message"></textarea>
```

Attributes:
- `rows` - Number of visible rows
- `cols` - Number of visible columns
- `placeholder` - Hint text
- `required` - Field must be filled

## Select Dropdown

For choosing from a list of options:

```html
<label for="country">Country:</label>
<select id="country" name="country">
    <option value="">Select a country</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
    <option value="ca">Canada</option>
</select>
```

### Multiple Selection

```html
<label for="languages">Languages (hold Ctrl to select multiple):</label>
<select id="languages" name="languages" multiple>
    <option value="html">HTML</option>
    <option value="css">CSS</option>
    <option value="js">JavaScript</option>
</select>
```

### Option Groups

```html
<select name="car">
    <optgroup label="European">
        <option value="bmw">BMW</option>
        <option value="mercedes">Mercedes</option>
    </optgroup>
    <optgroup label="American">
        <option value="ford">Ford</option>
        <option value="chevrolet">Chevrolet</option>
    </optgroup>
</select>
```

## Checkboxes

For multiple selections (yes/no options):

```html
<fieldset>
    <legend>Select your interests:</legend>
    
    <input type="checkbox" id="coding" name="interests" value="coding">
    <label for="coding">Coding</label><br>
    
    <input type="checkbox" id="design" name="interests" value="design">
    <label for="design">Design</label><br>
    
    <input type="checkbox" id="music" name="interests" value="music">
    <label for="music">Music</label>
</fieldset>
```

### Checked by Default

```html
<input type="checkbox" id="newsletter" name="newsletter" value="yes" checked>
<label for="newsletter">Subscribe to newsletter</label>
```

## Radio Buttons

For single selection from multiple options:

```html
<fieldset>
    <legend>Choose your plan:</legend>
    
    <input type="radio" id="basic" name="plan" value="basic">
    <label for="basic">Basic</label><br>
    
    <input type="radio" id="pro" name="plan" value="pro">
    <label for="pro">Pro</label><br>
    
    <input type="radio" id="enterprise" name="plan" value="enterprise">
    <label for="enterprise">Enterprise</label>
</fieldset>
```

!!! tip "Same 'name' for Radio Buttons"
    Radio buttons with the same `name` are grouped together - only one can be selected.

## Fieldset and Legend

Group related form fields:

```html
<fieldset>
    <legend>Personal Information</legend>
    
    <label for="first-name">First Name:</label>
    <input type="text" id="first-name" name="first-name"><br><br>
    
    <label for="last-name">Last Name:</label>
    <input type="text" id="last-name" name="last-name">
</fieldset>

<fieldset>
    <legend>Contact Information</legend>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email"><br><br>
    
    <label for="phone">Phone:</label>
    <input type="tel" id="phone" name="phone">
</fieldset>
```

## Buttons

### Submit Button

```html
<button type="submit">Submit</button>
<!-- OR -->
<input type="submit" value="Submit">
```

### Reset Button

```html
<button type="reset">Reset Form</button>
<!-- OR -->
<input type="reset" value="Reset">
```

### Regular Button

```html
<button type="button">Click Me</button>
```

!!! tip "Use <button> Tag"
    The `<button>` tag is more flexible and can contain HTML content, not just text.

## Complete Form Example

Here's a complete contact form:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contact Form</title>
</head>
<body>
    <h1>Contact Us</h1>
    
    <form action="/submit-contact" method="post">
        <fieldset>
            <legend>Your Information</legend>
            
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required><br><br>
            
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required><br><br>
            
            <label for="phone">Phone:</label>
            <input type="tel" id="phone" name="phone"><br><br>
        </fieldset>
        
        <fieldset>
            <legend>Your Message</legend>
            
            <label for="subject">Subject:</label>
            <select id="subject" name="subject" required>
                <option value="">Select a subject</option>
                <option value="general">General Inquiry</option>
                <option value="support">Support</option>
                <option value="sales">Sales</option>
            </select><br><br>
            
            <label for="message">Message:</label><br>
            <textarea id="message" name="message" rows="5" cols="40" required></textarea><br><br>
        </fieldset>
        
        <fieldset>
            <legend>Preferences</legend>
            
            <input type="checkbox" id="newsletter" name="newsletter" value="yes">
            <label for="newsletter">Subscribe to newsletter</label><br><br>
            
            <p>How did you hear about us?</p>
            <input type="radio" id="google" name="source" value="google">
            <label for="google">Google</label><br>
            
            <input type="radio" id="friend" name="source" value="friend">
            <label for="friend">Friend</label><br>
            
            <input type="radio" id="other" name="source" value="other">
            <label for="other">Other</label>
        </fieldset>
        
        <button type="submit">Send Message</button>
        <button type="reset">Clear Form</button>
    </form>
</body>
</html>
```

## Form Validation

HTML5 provides built-in validation:

### Required Fields

```html
<input type="text" name="name" required>
```

### Pattern Matching

```html
<!-- Only letters and spaces -->
<input type="text" name="name" pattern="[A-Za-z ]+" title="Only letters and spaces allowed">

<!-- Phone number format -->
<input type="tel" name="phone" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" placeholder="123-456-7890">
```

### Min/Max Values

```html
<input type="number" name="age" min="18" max="100">
<input type="date" name="birthday" max="2005-12-31">
```

### Custom Validation Messages

```html
<input type="email" name="email" required 
       oninvalid="this.setCustomValidity('Please enter a valid email address')"
       oninput="this.setCustomValidity('')">
```

## Best Practices

1. **Always use labels:** Improves accessibility and usability
2. **Group related fields:** Use `<fieldset>` and `<legend>`
3. **Use appropriate input types:** Helps with validation and mobile keyboards
4. **Provide placeholders:** Give users hints about expected input
5. **Mark required fields:** Use the `required` attribute
6. **Validate on both client and server:** HTML5 validation is not enough
7. **Provide clear error messages:** Help users fix mistakes
8. **Keep forms simple:** Don't ask for unnecessary information

## Common Mistakes

### 1. Missing Labels

```html
<!-- ❌ Wrong -->
<input type="text" name="name">

<!-- ✅ Correct -->
<label for="name">Name:</label>
<input type="text" id="name" name="name">
```

### 2. Missing Name Attributes

```html
<!-- ❌ Wrong (won't submit data) -->
<input type="text" id="email">

<!-- ✅ Correct -->
<input type="text" id="email" name="email">
```

### 3. Not Grouping Related Fields

```html
<!-- ❌ Wrong -->
<input type="text" name="first-name">
<input type="text" name="last-name">
<input type="email" name="email">

<!-- ✅ Correct -->
<fieldset>
    <legend>Personal Information</legend>
    <input type="text" name="first-name">
    <input type="text" name="last-name">
    <input type="email" name="email">
</fieldset>
```

## Practice Exercise

Create a registration form with:

1. Text inputs for first name, last name, username
2. Email and password fields
3. Date of birth (date input)
4. Country selection (dropdown)
5. At least 3 checkboxes for interests
6. Radio buttons for subscription plan
7. A textarea for additional comments
8. Submit and reset buttons
9. Proper labels and fieldset grouping
10. Required field validation

## What's Next?

Congratulations! You've learned the fundamentals of HTML. Next steps:

- **CSS** - Style your HTML pages
- **JavaScript** - Add interactivity
- **Semantic HTML5** - Modern best practices
- **Accessibility** - Make your sites usable for everyone
- **Responsive Design** - Make sites work on all devices

---

**Previous Tutorial:** [Lists and Tables](05_lists_and_tables.md)  
**Next Steps:** Learn CSS to style your HTML, or JavaScript to add interactivity!

