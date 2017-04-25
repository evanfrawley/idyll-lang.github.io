# Components

Components are the basic building block for adding interactivity in Idyll.

### Built-in Components

See [Idyll's built-in components](/components-built-in).

### Custom Components

See [custom Idyll components](/components-custom).

## Component Resolution

Components are resolved according to following algorithm:

* If there is a custom component with this name, use it.
* If there is a built-in component with this name, use it.
* If there is a valid HTML tag with this name, use it.
* If none of the above, just use a div, but give it the class of the component name

So, for example, assume we have one custom component, named `Custom`.

```
// Renders our custom component
[Custom /]

// Renders the built-in range component
[Range /]

// Renders `<img />` because it is a valid  HTML tag
[Img /]

// Renders `<div class="SomethingElse"></div>`
[SomethingElse /]
```

Continue to read about [Idyll's built-in components](/components-built-in).
