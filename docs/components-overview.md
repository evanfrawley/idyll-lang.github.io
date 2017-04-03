
# Components 

## Syntax 

Besides text, components are the other basic building block of an Idyll document. 
Components are denoted with brackets, and can be invoked in one of two ways: they can be self
closing,

```
[Range min:0 max:10 value:value /]
```

or have a closing and opening tag with content in between.

```
[Button]
Click Me
[/Button]
```

## Component Properties

Properties can be passed into components
in the following ways:

### Number, String

Numbers or string literals may be used.

```
[Component propName:10 /]
[Component propName:"propValue" /]
```

### Variable or Dataset

A variable or dataset can be passed in directly, this will
automatically create a binding between that variable and property,
more on this in the next section.

```
[Component propName:myVar /]
```

### Expression

Use backticks to pass an evaluated expression:

```
[Component propName:`2 * 2 * 2` /]
[Component propName:`{ an: "object" }` /]
```

If the property expects a function,
the expression will automatically be
converted to a callback. This is convenient
for updating variables on events, for example.

```
[Component onClick:`myVar++` /]
```

Idyll uses naming conventions to determine if the expression should be converted to a callback.
Properties that are named `onXxxxx` (e.g. `onClick`) or `handleYyyyy` (e.g. `handleMouseMove`) are 
assumed to expect callbacks.


## Component Name Resolution

Components are resolved according to following algorithm. First, map the 
name of your component in camel case to kebab case (e.g. `ComponentName` becomes `component-name`)

* If there is a custom component with this name, use it.
* If there is a built-in component with this name, use it.
* If there is a valid HTML tag with this name, use it.
* If none of the above, just use a div, but give it the class of the component name

So, for example,

```
// Renders `<img />` because it is a valid  HTML tag
[img /]

// Renders `<div class="somethingElse"></div>`,
// assuming a custom component somethingElse doesn't
// exist.
[somethingElse /]
```
