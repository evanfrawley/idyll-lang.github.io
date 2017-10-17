
# Refs

Idyll exposes the `ref` property to allow you to refer to specific components in
property expressions.

```
[Component ref:"thisComponent" propName:`refs.thisComponent`  /]
```

The ref property allows you to update the state of one component based on properties of another. Idyll
provides some utilities automatically, for example keeping track of the position
of a component on the page, and how far through a component's content the reader has
scrolled.

Each ref object has the following properties:

```js
{
  domNode: node,
  scrollProgress: {
    x: number,
    y: number
  },
  size: {
    x: number,
    y: number
  },
  position: {
    left: number,
    top: number,
    right: number,
    bottom: number
  }
}
```

For example:

```
[section ref:'section' style:`{ opacity: 1 - refs.section.scrollProgress.y }`]

Lorem ipsum...
...
lots of text here
...

[/section]
```

The above code will create a section of text that fades out as the user scrolls to the bottom of it.
`scrollProgress.y` in this case is a value from 0 to 1 that Idyll automatically computes,
providing the percentage that a user has scrolled through a certain component.


You've learned all about Idyll! All that's left is [deploying your project to the web](/publishing-deploying-to-the-web).