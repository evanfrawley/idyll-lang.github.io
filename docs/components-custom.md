
# Custom Components

Idyll is designed for people to use their own custom components as well.
Under the hood an Idyll component just needs to be anything that will
function as a React component. If you create a custom component in
JavaScript, point Idyll to the folder where you created it and
everything will just work, no need to worry about compiling, bundling,
or module loading.

For example, this custom component

```
const React = require('react');
const IdyllComponent = require('idyll-component');

class CustomComponent extends IdyllComponent {
  render() {
    return (
      <div {...this.props}>
        This is a custom component
      </div>
    );
  }
}

module.exports = CustomComponent;
```

could be invoked inside of an Idyll file with the
following code:

```
[CustomComponent /]
```

The `IdyllComponent` class adds an
`updateProps` method that is used to keep
variables in sync with the rest of the document, and also
adds a property `onEnteredView` that can be used to
trigger events in scroll-based narratives.

For example, a component can change the value of a
property that it receives, and Idyll will propegate
the change to any bound variables on the page.

```
const React = require('react');
const IdyllComponent = require('idyll-component');

class Incrementer extends IdyllComponent {

  increment() {
    this.updateProps({
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
[DisplayVar var:clickCount /]
```

Notice that even thought the `Incrementer` component doesn't know
anything about the variable `clickCount`, it will still correctly
update.

Of course, this trivial example could be accomplished using built-in components:

```
[var name:"clickCount" value:0 /]

[Button onClick:`clickCount+=1` ]Click Me.[/Button]
[DisplayVar var:clickCount /]
```

Custom component are meant for times when more complex and custom
code is needed. By default Idyll will look for your custom components 
inside of a folder called `components/`. If you wish to change the custom 
component path, specify it with the `--components` option, e.g. 
`idyll index.idl --css styles.css --components custom/component/path/`.