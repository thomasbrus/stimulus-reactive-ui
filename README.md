# Stimulus Reactive UI

A reactive UI system built on top of Stimulus.js that enables declarative, state-driven interfaces with minimal JavaScript. This project demonstrates how to create dynamic, interactive web applications using reactive patterns within the Stimulus framework.

## Demo

🚀 **[View Live Demo](https://thomasbrus.github.io/stimulus-reactive-ui/)**

The demo is entirely self-contained in a single `index.html` file that showcases 12 different interactive examples. Everything needed to run the demo is included:

- **Tailwind CSS** - Loaded via CDN for styling
- **Stimulus.js** - Imported via ES modules from unpkg
- **LiveController** - Custom Stimulus controller that implements the reactive system
- **Interactive Examples** - 12 demonstrations of reactive UI patterns

The demo works by extending Stimulus with a `LiveController` that:

1. Manages reactive state through JavaScript proxies
2. Processes `live:*` directives in HTML to bind state to DOM elements
3. Automatically updates the UI when state changes
4. Supports computed properties defined in `<script type="text/template">` tags

## Features

- **Declarative Reactive Bindings** - Use `live:text`, `live:class`, `live:show`, etc. to bind state to DOM elements
- **Computed Properties** - Define derived state using template scripts
- **Two-way Data Binding** - Automatic synchronization between form inputs and state
- **Conditional Rendering** - Show/hide elements based on state
- **Dynamic Styling** - Apply CSS classes and styles reactively
- **State Management** - Clean, predictable state updates with automatic UI synchronization

## How It Works

The system centers around a custom `LiveController` that extends Stimulus.js with reactive capabilities:

### State Properties

Define reactive state properties using `data-live-property` attributes on form inputs or `<script type="text/template">` tags for computed values.

### Live Directives

Bind state to DOM elements using special `live:*` attributes:

- `live:text` - Updates element text content
- `live:html` - Updates element innerHTML
- `live:class` - Conditionally applies CSS classes
- `live:style` - Dynamically sets CSS styles
- `live:show` - Shows/hides elements
- `live:disabled` - Enables/disables form elements

### Automatic Updates

The controller uses a MutationObserver to detect DOM changes and re-evaluate reactive bindings, ensuring the UI stays in sync with state changes.

## API Reference

### Live Directives

| Directive       | Description                   | Example                                     |
| --------------- | ----------------------------- | ------------------------------------------- |
| `live:text`     | Sets element text content     | `live:text="state.count"`                   |
| `live:html`     | Sets element innerHTML        | `live:html="state.content"`                 |
| `live:class`    | Conditionally applies classes | `live:class="{ 'active': state.isActive }"` |
| `live:style`    | Sets CSS styles               | `live:style="{ color: state.textColor }"`   |
| `live:show`     | Shows/hides element           | `live:show="state.isVisible"`               |
| `live:disabled` | Enables/disables element      | `live:disabled="!state.isValid"`            |

### State Properties

State properties can be defined in two ways:

1. **Form Input Binding** - Use `data-live-property="propertyName"` on inputs
2. **Computed Properties** - Use `<script type="text/template" data-live-property="propertyName">` with JavaScript expressions

## Browser Support

This project uses modern JavaScript features including:

- ES6 Modules
- Proxy objects
- MutationObserver
- Template literals

Supported in all modern browsers (Chrome 61+, Firefox 60+, Safari 12+, Edge 79+).
