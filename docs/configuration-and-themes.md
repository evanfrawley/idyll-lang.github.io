
# Configuration and Themes

## Command Line Options

The `idyll` command line tool accepts the following Options

* `--css` the path to your CSS file. You can use this to override Idyll's default styles, e.g. `$ idyll index.idl --css my-custom-styles.css`.
* `--components` the path to your custom components. By default this points to `components/`.
* `--datasets` the path to the folder containing your datasets. By default this points to `data/`.
* `--theme` the name of the theme to use. By default this is `blog`. More on themes below.
* `--build` the build flag tells Idyll to output the compiled JavaScript instead of running a server and opening your page in a web browser, `$ idyll index.idl --build > output.js`.

## Themes

Idyll currently ships with different themes that can be used to modify the page layout, allowing you to quickly test out different narrative styles 
for you project.

### Blog

This is the default theme. The `blog` theme is fairly traditional article layout with room in the margin to 
put notes and other callouts. 

![blog](images/blog.gif)

### Scroll

The scroll layout leaves more space for a fixed element, and adds margins between text sections, 
making it easy to trigger events when a certain section enters the viewport.


![scroll](images/scroll.gif)

