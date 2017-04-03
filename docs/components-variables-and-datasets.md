
# Variables and Datasets

In addition to rendered components, Idyll supports datasets and variables.
These are declared in the same way:

```
[var name:"myVar" value:5 /]
[data name:"myDataset" source:"data.json" /]
```

The above code declares a variable `myVar` and initializes it
with the value 5. It also imports a dataset from a JSON file.

Once a variable or dataset is initialized it can be used as an input to a component.
For example, the following code declares a variable `myVar`, and uses
it as input to two components.

```
[var name:"myVar" value:5 /]
[Range min:0 max:10 value:myVar /]
[DisplayVar var:myVar /]
```

Idyll handles all of the updating and rerendering of components for you,
so when someone interacts with the range slider, the display will be updated
automatically!
