
# Building your Idyll project for the web

Once you are happy with your project, the `idyll` command-line tool can also be used to 
build a stand alone JavaScript bundle. If you used the Idyll project generator, npm tasks
to build and deploy the project to github pages are available. Once you've initialized your 
project with a repo on github, run the command 

```sh
$ npm run deploy
``` 

this will compile the assets and push it to github 
pages. To learn more about how this works, continue reading.

If you want to use the `idyll` command line tool directly and build the JavaScript bundle, pass in
the `--build` flag.

```sh
$ idyll my-file.idl --build > bundle.js
```

This can be combined with other
useful tools to quickly generate a webpage. For example, 
the `indexhtmlify` package will create a barebones HTML page,
properly inserting the 

```
$ npm install -g indexhtmlify
$ idyll my-file.idl --build | indexhtmlify --style styles.css > idyll.html
```

The command that the generator uses is 

```
$ cp -r {images,styles.css} build/; idyll index.idl --build | uglifyjs > build/index.js && gh-pages -d ./build
```

which copies default static asset folders to the build directory, compiles and minifies the JavaScript, and 
then uses the `gh-pages` package to push the resulting folder to your `gh-pages` branch on Github.