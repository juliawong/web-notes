[Course](http://courses.reactjsprogram.com/courses/reactjsfundamentals)

# React.js Fundamentals Curriculum


## Intro
* Mostly declarative, deals with what to do via functions
* Based on components
* `setState` changes the state
* React router maps URLs to components
  * Use IndexRoute for default
* Webpack bundles code in a file, transforms and bundles
* Babel deals with translation e.g. JSX->JS
* AXIOS deals with HTTP requests

## NPM, Babel, Webpack and React Component
### NPM
* Allows for modules to be shared without CSN or local copies
* Manages different packages
* `npm init` to create a new npm proj
* `package.json` contains metadata about the project such as packages
* `npm install <package?  --save` installs a new package to the project and adds as a dep to package.json
* We can add scripts to package.json and run them with `npm run script_name`

### Webpack
* Code bundler - takes code, transforms, bundles and produces new code
* Main steps, what we need to provide
  1. root JS file
  2. Transformations to make
  3. Location to save code
* Loaders deal with transformation, we provide
  * File type
  * Dirs to include or exclude
  * Specific loader to run
* `__dirname` is referencing the name of the dir that the script resides in

* Problem might be that we have /app and /dist both containing index.txt
* Instead of manually copying and changing we'll use the *html-webpack-plugin*
* We provide
  * Template
  * Filename
  * Where to inject script i.e. head or body
* Plugin detects output filename of new file and adds it in new index.html

* `webpack -w` watches files and re-executes webpack upon changes
* `webpack -p` is for production, minifies code

``` JavaScript
// In webpack.config.js
var HtmlWebpackPlugin = require('html-webpack-plugin')
var HTMLWebpackPluginConfig = new HtmlWebpackPlugin({
  template: __dirname + '/app/index.html',
  filename: 'index.html',
  inject: 'body'
});
module.exports = {
  entry: [
    './app/index.js'
  ],
  output: {
    path: __dirname + '/dist',
    filename: "index_bundle.js"
  },
  module: {
    loaders: [
      {test: /\.js$/, exclude: /node_modules/, loader: "babel-loader"}
    ]
  },
  plugins: [HTMLWebpackPluginConfig]
};
```

#### Babel
* Deals with the specific transformation of the code
* e.g. JSX -> JS
* Give webpack `babel-loader`
* We create a `.babelrc` for each babel transformation
* Tells babel-loader which transformations to actually make
``` JavaScript
{
  "presets": [
    "react"
  ]
}
```

### React Component
* Components are defined in JS or JSX
* Data is received from a parent's component or contained in the component itself
* `createClass` pass a description of the component
  * Must have a `render` method
* `ReactDOM.render` takes 2 args - component to render, DOM node to render
* virtual DOM is a JavaScript representation of the actual DOM
* React uses virtual DOM to minimise manipulations to the actual DOM


## Pure Functions. f(d)=v. Props and Nesting Components.


## this.props.children and getting started with React Router


## Container vs Presentational Components, PropTypes, and Stateless Functional Components


## Life Cycle Events and Conditional Rendering


## Axios, Promises, and the Github API


## Rendering UI


## More Container vs Presentational Components


## Private Functional Stateless Components


## Building a Highly Reusable React Component


## React Router Transition Animation and Webpack's CSS Loader
