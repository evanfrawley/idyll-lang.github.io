# Components

Components are the basic building block for adding interactivity in Idyll.

### Built-in components

See [Idyll's built-in components](/components-built-in).

### Installing components from `npm`

See [installing components from npm](/components-npm).

### Custom components

See [custom Idyll components](/components-custom).


## Component resolution

Components are resolved according to following algorithm:

* If there is a custom component with this name, use it.
* If there is a component installed from npm with this name, use it.
* If there is a built-in component with this name, use it.
* If there is a valid HTML tag with this name, use it.

Continue to read about [Idyll's built-in components](/components-built-in).
