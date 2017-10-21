
# Syntax

*Note: Idyll tries to maintain parity with popular markdown implementations, but sometimes doesn't get things exactly right. If something seems off, feel free to open [an issue](https://github.com/idyll-lang/idyll/issues?q=is%3Aissue+is%3Aopen+label%3ACompiler).*

We provide syntax highlighting plugins for several editors:

* [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=mathisonian.idyll-syntax)
* [Atom](https://atom.io/packages/language-idyll)

## Text

By default everything in Idyll is text. To make common
formatting tasks easier, Idyll borrows some syntax from markdown.

#### Bold, italic

Text surrounded by asterisks (`*`) will be bolded,
e.g. `*italic*` becomes *italic*, and `**bold**` becomes
**bold**.

#### Headers

Use a pound sign (`#`) to denote a header:

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

### Component properties

Properties can be passed into components
in the following ways:

#### Literals: number, string, boolean

Number, string, or boolean literals may be used.

```
[Component propName:10 /]
[Component propName:"propValue" /]
[Component propName:false /]
```

#### Variable or dataset

A variable or dataset can be passed in directly, this will
automatically create a binding between that variable and property,
more on this in the section on [variables and datasets](/components-variables-and-datasets).

```
[Component propName:myVar /]
```

If the variable changes that update will immediately be reflected in the
state of the component.

#### Expression

Use backticks to pass an evaluated expression:

```
[Component propName:`2 * 2 * 2` /]
[Component propName:`{ an: "object" }` /]
```

Note that because Idyll is reactive, if a variable changes any expressions that reference that
variable will immediately be recomputed. See this utilized to create reactive vega-lite specifications:
https://idyll-lang.github.io/examples/csv/.

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


#### Refs

There is a special property called `ref` that allows you to create a reference to specific
component on the page. This is primarily used to keep track of elements on the page as
a reader scrolls. See the section on [refs](/components-refs) for more details.


## Variables

Variables can be declared at any point in an Idyll file. Variables use
the same syntax as a component, but must defined a `name` and a `value`
property.

```
[var name:"x" value:10 /]
```

The above code defines a variable `x`, with the initial value of `10`.

### Derived variables

A derived variable is similar to a `var`, but its value is derived from
other variables, and is recomputed whenever values change:

```
[derived name:"xSquared" value:`x * x` /]
```

The above code defines a derived variable `xSquared` that depends
on the value of `x`. The value of `xSquared` is automatically updated
based on the value of `x`.

## Datasets

A dataset is similar to a variable, except instead of expecting a
`value`, datasets must be provided with a `source` (the name of the data file).

Example:

```
[data name:"myData" source:"myData.csv" /]
[Table data:myData /]
```

The above code declares a dataset, and uses it as input to a `Table` component.
Datasets can be either `.csv` or `.json` files. CSV files will automatically be
converted to a JSON object.

Continue to the next section to learn about [customizing Idyll](/configuration-and-styles).

