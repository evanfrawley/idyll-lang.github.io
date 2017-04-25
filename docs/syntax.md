
# Syntax

## Text

By default everything in Idyll is text. To make common
formatting tasks easier, Idyll borrows some syntax from markdown.

#### Bold, Italic

Text surrounded by asterisks (*) will be bolded,
e.g. `*italic*` becomes *italic*, and `**bold**` becomes
**bold**.

#### Headers

Use a pound sign (#) to denote a header:

```
# Title h1
## Title h2
### Title h3
#### Title h4
##### Title h5
###### Title h6
```

#### Code

Text placed between backticks (\`) will be displayed inline
as code: `` `y = x * x` `` becomes `y = x * x`.

Text placed between groups of three backticks will be displayed as
a code block.

```
This is a code block
```

The above code block is created with this code:
````
```
This is a code block
```
````

## Components

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


Continue to the next section to learn about [customizing Idyll](/configuration-and-styles).