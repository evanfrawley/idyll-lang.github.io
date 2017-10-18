

# Built-In Components

Idyll ships with a handful of components that
handle common tasks. They are broken into
three categories:


* [Layout](#layout) - these components help manage page layout, for example putting text in the `Aside` component will render it in the article margin instead of inline with the rest of your text.
  * [Aside](#aside)
  * [Feature](#feature)
  * [Fixed](#fixed)
  * [Float](#float)
  * [Full Screen](#full-screen)
  * [Inline](#inline)
  * [Panel](#panel)
  * [Waypoint](#waypoint)

* [Presentation](#presentation) - these components render something to the screen, for example the `Chart`
component takes data as input and can display several types of charts.
  * [Action](#action)
  * [Boolean](#boolean)
  * [Button](#button)
  * [Chart](#chart)
  * [Display](#display)
  * [Dynamic](#dynamic)
  * [Equation](#equation)
  * [Gist](#gist)
  * [Header](#header)
  * [Link](#link)
  * [Radio](#radio)
  * [Range](#range)
  * [Select](#select)
  * [Slideshow](#slideshow)
  * [SVG](#svg)
  * [Table](#table)
  * [Text Input](#text-input)

* [Helpers](#helpers) - these components don't affect the page content, but help with common tasks. The `Analytics` component makes it
easy to add Google Analytics to your page.
  * [Analytics](#analytics)
  * [Meta](#meta)
  * [Preload](#preload)


All built-in components expose a property `onEnterView` that can be used to trigger events when a reader scrolls the page to
reveal specific content.

## Layout

### Aside

Content inside of an aside component will be displayed in the margin of your document. For example, the [consumer complaints](https://mathisonian.github.io/consumer-complaints/) article uses the aside component to display a small chart and caption:

![aside](images/aside.png)

```
[Aide]
  [Chart type:"time" data:complaintsByDate /]
  [caption]Complaints sent to the CFPB each month[/caption]
[/Aside]
```



### Feature

A `feature` component will lock a component in place on the reader's screen while a specified set of content
scrolls by.

![feature](images/feature.gif)

```
[Feature]
  [Feature.Content]
    This content gets locked on the screen
  [/Feature.Content]

  Anything else you put here will scroll by. The
  component will unlock after all of this content here has been shown.
[/Feature]
```

#### Props

* `value` -  the percentage of the the feature that the user has scrolled through. Bind a variable to this and it will be updated automatically.

### Fixed

Content inside of a `fixed` component will be locked in place, even when the rest of the document scrolls. The [scroll](https://idyll-lang.github.io/idyll/scroll) example uses the `fixed` component to keep the dynamic chart in place:

![fixed](images/fixed.gif)

```
[Fixed]
[Chart type:"scatter" data:dynamicData /]
[/Fixed]
```


### Float

Content inside of a float will use the CSS `float` attribute to float to the left or right of its parent container.

```
[Float position:"right"]

[/Float]
```

#### Props

* `position` -  the float position: left or right.
* `width` - the width of the component, specified in pixels or percentage.

### FullScreen

This container component will break out of the article column and take up the readers entire viewport.

```
[FullScreen]
  [MyCustomComponent /]
[/FullScreen]
```

This is useful to use in conjunction with the `Feature` component to get fullscreen background images:

```
[Feature]
  [Feature.Content]
    [FullScreen backgroundImage:"background-image.jpg"  /]
  [/Feature.Content]

  Anything else you put here will scroll by. The
  component will unlock after all of this content here has been shown.
  ...
[/Feature]
```

#### Props

* `backgroundImage` - an image to be displayed.


### Inline

The `inline` component adds the `display: inline-block` style property, so that items inside of `inline` component will
be displayed next to each other. For example, this code,

```
[div]
[Inline][img src:"..." /][/Inline]
[Inline][img src:"..." /][/Inline]
[Inline][img src:"..." /][/Inline]
[/div]
```

Will display three images side by side.

### Panel

A panel is a section that will "slide up" after a the end of a `Feature` was reached. This component must be used directly
after a `Feature` component for it to work properly.

```
[Feature]
...
[/Feature]

[Panel]
  This is the next section! The panel will slide up over
  the feature and the text will continue on.
[/Panel]
```


### Waypoint

A `Waypoint` component just adds some padding around your text to make it easier to trigger events when
a certain section has been reached.

```
[var name:"state" value:0]

[Waypoint onEnterView:`state = 0`]
  Initial state!
[/Waypoint]

[Waypoint onEnterView:`state = 1`]
  Second state.
[/Waypoint]

[Waypoint onEnterView:`state = 2`]
  Third state...
[/Waypoint]
```

## Presentation

### Action

The `action` component allows you to add event handlers to text. For example:

```
This is regular text, but when you [action onClick:`alert('clicked the text')`]click me[/action], an alert will appear.
```

#### Props

* `onClick`
* `onMouseEnter`
* `onMouseLeave`

### Boolean

This will display a checkbox.

#### Props

* `value` -  A value for the checkbox. If this value is truthy, the checkbox will be shown.

### Button

This will display a button. To control what happens when the button is clicked, add an `onClick` property:

![button](images/button.gif)

```
[button onClick`myVar += 1`]Click Me![/button]
```

### Chart

This will display a chart. It expects the following properties:

* `data` - A JSON object containing the data for this chart. It uses the [victory](https://formidable.com/open-source/victory/docs) library to handle rendering, so see those docs for more information on what types of data can be passed in.
* `type` - The type of the chart to display, can be `line`, `scatter`, `bar`, `pie`, or `time`. The time type is a line chart that expects the `x` values in the data to be in the temporal domain.

![chart](images/chart.png)

```
[var name:`dataToBeCharted` value:`[
  {x: 0, y: 0.5},
  {x: 3.5, y: 0.5},
  {x: 4, y: 0},
  {x: 4.5, y: 1},
  {x: 5, y: 0.5},
  {x: 8, y: 0.5}
]` /]

[Chart type:"line" data:dataToBeCharted /]
```

### Display

This will render the value of a variable to the screen. It is mostly useful for debugging:

![display](images/displayvar.gif)

```
[var name:"myVar" value:10 /]

[Range value:myVar min:0 max:100 /]
[Display value:myVar /]
```

### Dynamic

This will render a dynamic variable to the screen.

![dynamic](images/dynamic.gif)

```
[var name:"myVar" value:10 /]

[Dynamic value:myVar /]
```

The properties are:

* `value`: The value to display.
* `max`: The maximum value.
* `min`: The minimum value.
* `interval`: The granularity of the changes.

### Equation

This uses [KaTeX](https://github.com/Khan/KaTeX) to typeset mathematical equations. Example:

![equation](images/equation.png)

```
[Equation]
  y = \int x^2 dx
[/Equation]
```

### Header

This component makes it easy to add a title, subtitle, and byline to your article:

![header](images/header.png)

```
[Header
  title:"The Title of my Article"
  subtitle:"The subtitle of my article"
  author:"Matthew Conlen"
  authorLink:"https://github.com/mathisonian/"
  /]
```

### Gist

Embed a github gist

![gist](images/gist.png)

```
[gist gist:"0f83a12e29b268ffca39f471ecf39e91" file:"particles.idl" /]
```

### Link

This component just acts as syntactic sugar for displaying links inline in your text.

```
[link text:"the text" url:"https://some.url" /]

is equivalent to [a href:"https://some.url"]the text[/a].
```

### Range

This component displays a range slider. The properties are:

* `value`: The value to display; if this is a variable, the variable will automatically be updated when the slider is moved.
* `max`: The maximum value.
* `min`: The minimum value.
* `step`: The granularity of the slider.

![displayvar](images/displayvar.gif)

```
[var name:"myVar" value:10 /]

[Range value:myVar min:0 max:100 /]
[Display value:myVar /]
```

### Radio

This component displays a set of radio buttons.

```
[var name:"radioVal" value:"test1" /]
[Radio value:radioVal options:`["test1", "test2"]`  /]
```

#### Props

* `value` - the value of the "checked" radio button
* `options` - an array representing the different buttons. Can be an array of strings like `["val1", "val2"]` or an array of objects `[{ value: "val1", label: "Value 1" }, { value: "val2", label: "Value 2" }]`.

### Select

This component displays a selection dropdown.

```
[var name:"selectVal" value:"test1" /]
[Select value:selectVal options:`["test1", "test2"]`  /]
```

#### Props

* `value` - the currently selected value.
* `options` - an array representing the different options. Can be an array of strings like `["val1", "val2"]` or an array of objects `[{ value: "val1", label: "Value 1" }, { value: "val2", label: "Value 2" }]`.


### Slideshow

This component is used to dynamically display different content. It can be used to make slideshows,
but is generally useful for dynamically displaying different content of any type.

![slides](images/slides.gif)

```
[var name:"slide" value:1 /]

[slideshow currentSlide:slide]
  [slide]This is the content for slide 1[/slide]
  [slide]This is the content for slide 2[/slide]
  [slide]This is the content for slide 3[/slide]
[/slideshow]

[Button onClick:`slide = 1`]Slide 1[/Button]
[Button onClick:`slide = 2`]Slide 2[/Button]
[Button onClick:`slide = 3`]Slide 3[/Button]

```


### SVG

This component will display an SVG file inline using https://github.com/matthewwithanm/react-inlinesvg. This makes it
easy to style the SVG with css, as opposed to displaying the svg inside of an image tag.

Usage:

```
[SVG src:"path/to/file.svg" /]
```

### Table

Display tabular data. Uses https://github.com/glittershark/reactable under the hood to render the table.

![table](images/table.png)

```
[Table data:`[{columnName1: value, columnName2: value}, {columnName1: value, {columnName2: value}}]` /]
```

### Text Input

A user-editable text input field.

```
[var name:"textVal" value:"Hello World" /]
[TextInput value:textVal /]
```

#### Props

* `value` - the current value of the text entry box.

## Helpers

### Analytics

This component makes it easy to insert a Google Analytics code on your page.

```
[Analytics google:"UA-XXXXXXXXX" /]
```

### Meta

The meta component adds context to the page template when building your app for publication. The following variables are available and will be inserted
as `<meta>` properties into the head of your HTML page if you define them:

* `title` - the page title.
* `description` - a short description of your project.
* `url` - the canonical URL from this project.
* `twitterHandle` - the author's twitter handle, it will create a link in the twitter card.
* `shareImageUrl` - the URL of an image to be shared on social media (twitter cards, etc.). This must be a fully qualified URL, e.g. https://idyll-lang.github.io/images/logo.png.
* `shareImageWidth` - the width of the share image in pixels.
* `shareImageHeight` - the height of the share image in pixels.

Continue to read about making [custom components](/components-custom).


### Preload

This will preload an array of images, useful if you want to show them later on in the article and not have a loading flash.

#### Props

* `images` - the array of images: `["image-url-1.png", "image-url-2.jpg"]`.
