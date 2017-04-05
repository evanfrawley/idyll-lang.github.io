

# Built-In Components

Idyll ships with a handful of components that
handle common tasks. They are broken into
three categories:

* [Layout](#layout) - these components help manage page layout, for example putting text in the `Aside` component will render it in the article margin instead of inline with the rest of your text.
  * [Aside](#aside)
  * [Fixed](#fixed)
  * [Inline](#inline)

* [Presentation](#presentation) - these components render something to the screen, for example the `Chart`
component takes data as input and can display several types of charts.
  * [Button](#button)
  * [Chart](#chart)
  * [DisplayVar](#displayvar)
  * [Equation](#equation)
  * [Header](#header)
  * [Link](#link)
  * [Range](#range)
  * [Slideshow / Slide](#slideshow-slide)
  * [SVG](#svg)
  * [Table](#table)
  * [VegaLite](#vegalite)

* [Helpers](#helpers) - these components don't affect the page content, but help with common tasks. The `Analytics` component makes it
easy to add Google Analytics to your page.
  * [Analytics](#analytics)
  * [Meta](#meta)

All built-in compononents expose a property `onEnteredView` that can be used to trigger events when a reader scrolls the page to
reveal specific content.

## Layout

### Aside

Content inside of an aside component will be displayed in the margin of your document. For example, the [consumer complaints](https://mathisonian.github.io/consumer-complaints/) article uses the aside component to display a small chart and caption:

![aside](images/aside.png)

```
[aside]
  [Chart type:"time" data:complaintsByDate /]
  [caption]Complaints sent to the CFPB each month[/caption]
[/aside]
```

### Fixed

Content inside of a `fixed` component will be locked in place, even when the rest of the document scrolls. The [scroll](https://idyll-lang.github.io/idyll/scroll) example uses the `fixed` component to keep the dynamic chart in place:

![fixed](images/fixed.gif)

```
[fixed]
[Chart type:"scatter" data:dynamicData /]
[/fixed]
```

### Inline

The `inline` component adds the `display: inline-block` style property, so that items inside of `inline` component will
be displayed next to eachother. For example, this code,

```
[section]
[inline][img src:"..." /][/inline]
[inline][img src:"..." /][/inline]
[inline][img src:"..." /][/inline]
[/section]
```

Will display three images side by side.

## Presentation

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

### DisplayVar

This will render the value of a variable to the screen. It is mostly useful for debugging:

![displayvar](images/displayvar.gif)

```
[var name:"myVar" value:10 /]

[Range value:myVar min:0 max:100 /]
[DisplayVar var:myVar /]
```

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

### Link

This component just acts as syntactic sugar for displaying links inline in your text.

```
[link text:"the text" url:"https://some.url" /]

is equivalent to [a href:"https://some.url"]the text[/a].
```

### Range

This component displays a range slider. The properties are:

* `value`: The value to display; if this is a variable, the variable will automatically be updated when the slider is moved.
* `man`: The maximum value.
* `min`: The minimum value.
* `step`: The granularity of the slider

![displayvar](images/displayvar.gif)

```
[var name:"myVar" value:10 /]

[Range value:myVar min:0 max:100 /]
[DisplayVar var:myVar /]
```


### Slideshow / Slide

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
[SVG src="path/to/filg.svg" /]
```

### Table

Display tabular data. Uses https://github.com/glittershark/reactable under the hood to render the table.

![table](images/table.png)

```
[Table data:`[{columnName1: value, columnName2: value}, {columnName1: value, {columnName2: value}}]` /]
```

### VegaLite

Render a [Vega Lite](https://vega.github.io/vega-lite/) spec, using https://github.com/kristw/react-vega-lite.

```
[data name:"myData" src:"my-dataset.json" /]

[VegaLite data:myData spec:`{
  mark: "bar",
  encoding: {
    x: {field: "a", type: "ordinal"},
    y: {field: "b", type: "quantitative"}
  }
}`]
```

## Helpers

### Analytics

This component makes it easy to insert a Google Analytics code on your page.

```
[Analytics google:"UA-XXXXXXXXX" /]
```

### Meta

The meta component adds context to the page template when building your app for publication. The following variables are available and will be inserted
as `<meta>` properties into the head of your HTML page if you define them:

* `title` - the page title
* `description` - a short description of your project
* `url` - the canonical URL from this project
* `twitterHandle` - the author's twitter handle, it will create a link in the twitter card
* `shareImageUrl` - the URL of an image to be shared on social media (twitter cards, etc.). This must be a fully qualified URL, e.g. https://idyll-lang.github.io/images/logo.png.
* `shareImageWidth` - the width of the share image in pixels
* `shareImageHeight` - the height of the share image in pixels

Continue to read about making [custom components](/components-custom).