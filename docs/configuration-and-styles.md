
# Configuration and Styles

## Command Line Options

The `idyll` command line tool accepts the following options

* `--css` the path to your CSS file. You can use this to override Idyll's default styles, e.g. `$ idyll index.idl --css my-custom-styles.css`.
* `--components` the path to your custom components. By default this points to `components/`.
* `--datasets` the path to the folder containing your datasets. By default this points to `data/`.
* `--layout` the name of the layout to use. By default this is `blog`. More on layouts below.
* `--theme` the name of the theme to use. By default this is `idyll`. More on themes below.
* `--build` the build flag tells Idyll to output the compiled JavaScript instead of running a server and opening your page in a web browser, `$ idyll index.idl --build > output.js`.

If you are using Idyll via the project generator, open `package.json` to change these options.

## Themes and Page Layout

Idyll exposes two options to help you style your project, `layout` and `theme`. `layout` deals with CSS styles related to how your content is
layed out on the page: width, columns, etc. The `theme` option allows you to choose diffent stylesheets to change the style of the content itself (text color, font, and so on).

### Layout

Idyll currently ships with several page layouts that can be used to modify the structure of how to content is displayed on the page, allowing you to quickly test out different narrative styles
for you project.

#### Centered

This is the default layout. It puts your content in the center of the page and is mobile responsive.

#### Blog

The `blog` layout is fairly traditional article layout with room in the margin to
put notes and other callouts. See https://mathisonian.github.io/trig/etymology/ for an example of this layout.

#### None

If you set `--layout none` Idyll won't provide any structural CSS, allowing you to customize things to your
heart's content.

### Themes

#### Github

This is the default theme, it uses CSS that resembles the styles in GitHub READMEs.

#### Idyll

This theme uses custom styles that go along with Idyll's look and feel. See https://mathisonian.github.io/trig/etymology/ for an example of this style.

## Using Idyll as an API

You can use Idyll directly from JavaScript as well.

### API:

`idyll(idyllFile, options, callback)`

### Example

```
var idyll = require('idyll');

idyll('index.idl', {
  output: 'build/',
  htmlTemplate: '_index.html',
  componentFolder: './components/',
  defaultComponents: './components/default/',
  dataFolder: './data',
  layout: 'centered',
  theme: 'github',
  compilerOptions: {
    spellcheck: true
  },
  build: true
}, function() {
  // calls when Idyll is finished building
});
```

Continue to the next section to learn about [Idyll components](/components-overview).

