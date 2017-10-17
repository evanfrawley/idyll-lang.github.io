
# Custom Components

## Overview

Idyll is designed for people to use their own custom components as well.
Under the hood an Idyll component just needs to be anything that will
function as a React component. If you create a custom component in
JavaScript, point Idyll to the folder where you created it and
everything will just work, no need to worry about compiling, bundling,
or module loading.

For example, this custom component

```js
const React = require('react');

class Custom extends IdyllComponent {
  render() {
    const { hasError, updateProps, ...props } = this.props;

    return (
      <div {...props}>
        This is a custom component
      </div>
    );
  }
}

module.exports = Custom;
```

could be invoked inside of an Idyll file with the
following code:

```
[Custom /]
```

## Idyll component

Idyll adds an `updateProps` method to the components input props.
This function can be called to update variable values and propagate
those changes to the rest of the Idyll document.

### Example

For example, a component can change the value of a
property that it receives, and Idyll will propagate
the change to any bound variables on the page.

```js
const React = require('react');
class Incrementer extends React.Component {

  increment() {
    this.props.updateProps({
      value: this.props.value + 1
    })
  }

  render() {
    return (
      <div onClick={this.increment.bind(this)}>
        Click me.
      </div>
    );
  }
}

module.exports = Incrementer;
```

The `Incrementer` component could then be used as follows:

```
[var name:"clickCount" value:0 /]

[Incrementer value:clickCount /]
[Display value:clickCount /]
```

Notice that even thought the `Incrementer` component doesn't know
anything about the variable `clickCount`, it will still correctly
update.


## Name resolution

Components lookup is based on filenames. If your component name
is `MyComponent`, it will match files like `mycomponent.js` or `my-component.js`.
The component filenames are case insensitive.

Custom component are meant for times when more complex and custom
code is needed. By default Idyll will look for your custom components
inside of a folder called `components/`. If you wish to change the custom
component path, specify it with the `--components` option, e.g.
`idyll index.idl --css styles.css --components custom/component/path/`.

Continue to learn how to use [references](/components-refs) to make your page more dynamic.