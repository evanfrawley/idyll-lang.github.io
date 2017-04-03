
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
layed out on the page: width, columns, etc. The `theme` option allows you to choose diffent stylesheets to change the aesthetics of the content. 

### Layout

Idyll currently ships with two different page layouts that can be used to modify the structure of how to content is displayed on the page, allowing you to quickly test out different narrative styles 
for you project.

#### Blog

This is the default layout. The `blog` layout is fairly traditional article layout with room in the margin to 
put notes and other callouts. 

![blog](images/blog.gif)

#### Scroll

The scroll layout leaves more space for a fixed element, and adds margins between text sections, 
making it easy to trigger events when a certain section enters the viewport.


![scroll](images/scroll.gif)


### Themes

There currently is only one default theme, expect more soon. 


Continue to the next section to learn about [Idyll components](/components-overview).