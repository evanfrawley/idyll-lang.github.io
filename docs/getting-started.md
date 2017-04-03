
# Getting Started

The easiest way to get started with Idyll is to use the project generator.
It will help get you set up using custom components, datasets, and stylesheets. 
To use the generator:

```sh
$ npm install -g yo generator-idyll
$ yo idyll
```

The generator will produce a structure that looks like this:

```sh
$  tree -I node_modules
.
├── _index.html
├── components
│   └── custom-component.js
├── data
│   └── example-data.json
├── images
│   └── idyll.png
├── index.idl
├── package.json
└── styles.css

3 directories, 7 files
```

The files do the following:

* `index.idl` - The main Idyll file, write your text in here.
* `styles.css` - By putting CSS in here you can override the default styles.
* `components/` - The folder for custom components. Any component defined in this folder can be invoked in the .idl file.
* `data/` - If you want to include a dataset in your project, put it in here.
* `images/` - A folder for static images.
* `_index.html` - A barebones HTML file that will be used if you publish your project to the web.
* `package.json` - This file contains all the metadata for your project.

To get started, from a terminal in that directory run `npm start` and Idyll will compile your 
file and open it in your web browser. Every time you save the `index.idl` file, the system will automatically recompile 
everything and update the page in the browser.

If you instead just want to test things out quickly, the simplest way is to
install it from npm, create a new file and start writing:

```sh
$ npm install -g idyll
$ idyll my-file.idl
```

The `idyll` command will automatically compile everything and load the
interactive page in your web browser.

To use a custom stylesheet, use the `--css` flag.

```sh
$ idyll my-file.idl --css styles.css
```

Continue to the [next section](/configuration-and-styles) to learn more.