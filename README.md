# Stimulus Reactive UI

A reactive UI system built on top of Stimulus.js that enables declarative, state-driven interfaces with minimal JavaScript. This project demonstrates how to create dynamic, interactive web applications using reactive patterns within the Stimulus framework.

## Demo

> [!TIP]
> 🚀 **[View Live Demo](https://thomasbrus.github.io/stimulus-reactive-ui/)**

---

<a href="https://thomasbrus.github.io/stimulus-reactive-ui/">
<img src="https://raw.githubusercontent.com/thomasbrus/stimulus-reactive-ui/refs/heads/main/demo.png" alt="Stimulus Reactive UI Demo" />
</a>

---

```html
<div data-controller="live">
  <!-- State -->
  <input type="hidden" data-live-state="count" value="0" />

  <!-- Computed properties -->
  <script type="text/template" data-live-computed="isPositive">
    state.count > 0
  </script>
  <script type="text/template" data-live-computed="statusText">
    state.count < 0 ? 'negative' : 'positive'
  </script>

  <!-- Demo -->
  <h2 live:text="state.count">0</h2>
  <p live:class="{ 'bg-green-100': computed.isPositive, 'bg-red-100': !computed.isPositive }">
    Counter is <span live:text="computed.statusText">positive</span>
  </p>

  <button data-action="click->live#update" data-live-update-param="state.count++">Increment</button>
  <button data-action="click->live#update" data-live-update-param="state.count--">Decrement</button>
</div>
```

The demo is entirely self-contained in a single `index.html` file that showcases 11 different interactive examples. Everything needed to run the demo is included:

- **Tailwind CSS** - Loaded via CDN for styling
- **Stimulus.js** - Imported via ES modules from unpkg
- **LiveController** - Custom Stimulus controller that implements the reactive system
- **Interactive Examples** - 11 demonstrations of reactive UI patterns

## Features

- **Declarative Reactive Bindings** - Use `live:text`, `live:class`, `live:show`, etc. to bind state to DOM elements
- **Computed States** - Define derived state using template scripts
- **Two-way Data Binding** - Automatic synchronization between form inputs and state
- **Conditional Rendering** - Show/hide elements based on state
- **Dynamic Styling** - Apply CSS classes and styles reactively
- **State Management** - Clean, predictable state updates with automatic UI synchronization

## Usage

### Live States

Define reactive state properties that can be bound to form inputs or calculated dynamically.

**Form Input Binding** - Use `data-live-state="propertyName"` on inputs:

```html
<input type="text" data-live-state="username" value="john" />
<input type="checkbox" data-live-state="isActive" />
<select data-live-state="theme">
  <option value="light">Light</option>
  <option value="dark">Dark</option>
</select>
```

**Computed States** - Use `<script type="text/template" data-live-computed="propertyName">` with JavaScript expressions:

```html
<script type="text/template" data-live-computed="fullName">
  state.firstName + ' ' + state.lastName
</script>
<script type="text/template" data-live-computed="isValid">
  state.username.length > 3 && state.email.includes('@')
</script>
```

> **Important:** Within computed property definitions, use `state.` to reference base state properties and `computed.` to reference other computed properties. In your HTML templates, use `computed.` to reference computed properties and `state.` for base state properties.

```html
<!-- In computed definitions -->
<script type="text/template" data-live-computed="greeting">
  'Hello, ' + state.firstName + ' ' + state.lastName
</script>
<script type="text/template" data-live-computed="formalGreeting">
  computed.greeting + '! Welcome to our application.'
</script>

<!-- In HTML templates -->
<h1 live:text="computed.greeting">Hello</h1>
<p live:text="computed.formalGreeting">Welcome</p>
```

### Live Attributes

Bind state to DOM elements using special `live:*` attributes that automatically update when state changes.

| Attribute       | Description                   | Example                                     |
| --------------- | ----------------------------- | ------------------------------------------- |
| `live:text`     | Sets element text content     | `live:text="state.count"`                   |
| `live:html`     | Sets element innerHTML        | `live:html="state.content"`                 |
| `live:class`    | Conditionally applies classes | `live:class="{ 'active': state.isActive }"` |
| `live:style`    | Sets CSS styles               | `live:style="{ color: state.textColor }"`   |
| `live:show`     | Shows/hides element           | `live:show="state.isVisible"`               |
| `live:disabled` | Enables/disables element      | `live:disabled="!state.isValid"`            |

**Examples:**

```html
<!-- Text and HTML content -->
<h1 live:text="state.title">Default Title</h1>
<div live:html="computed.htmlContent"></div>

<!-- Conditional styling -->
<button
  live:class="{
  'btn-primary': computed.isActive,
  'btn-secondary': !computed.isActive,
  'disabled': computed.isLoading
}"
>
  Submit
</button>

<!-- Dynamic styles -->
<div
  live:style="{
  width: computed.progress + '%',
  backgroundColor: state.color
}"
></div>

<!-- Show/hide and enable/disable -->
<div live:show="computed.showDetails">Details content</div>
<button live:disabled="!computed.isValid">Save</button>
```

**State Updates** - Trigger state changes using the `live#update` action:

```html
<button data-action="click->live#update" data-live-update-param="state.count++">Increment</button>
<button data-action="click->live#update" data-live-update-param="state.isVisible = !state.isVisible">Toggle</button>
```

## Browser Support

This project uses modern JavaScript features including:

- ES6 Modules
- Proxy objects
- MutationObserver
- Template literals

Supported in all modern browsers (Chrome 61+, Firefox 60+, Safari 12+, Edge 79+).

## Security Considerations

When implementing reactive UI systems that interpolate user input, it's important to consider security implications. This demo evaluates dynamic code using `new Function()`, which is safer and more performant than `eval()` but still carries risks with untrusted input.

For production applications planning to interpolate user input, it is recommended to restrict JavaScript execution to a safe subset using libraries like [jse-eval](https://www.npmjs.com/package/jse-eval), which provides secure expression evaluation without full JavaScript access. Always validate and sanitize user input before incorporating it into reactive expressions to prevent cross-site scripting (XSS) and code injection vulnerabilities.
