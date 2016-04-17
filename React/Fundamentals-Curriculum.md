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
* `--save-dev` is used to save the package for dev e.g. unit tests, minification
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

### Nested Components and Props
* Props are used to pass data from one component to another, similar to arguments
* e.g. the `name` attribute is passed
``` JavaScript
var HelloUser = React.createClass({
  render: function(){
    return (
      <div> Hello, {this.props.name}</div>
    )
  }
});
ReactDOM.render(<HelloUser name="Tyler"/>, document.getElementById('app'));
```

### Building UIs with Pure Functions and Function Composition
* f(d)=V, function takes in data and returns a view
* Compose functions to get some UI
* Pure functions are consistent and predictable
  * Same args always gives the same results
  * Exe doesn't depend on state of app
  * Don't modify vars outside of scope

## this.props.children and getting started with React Router

### this.props.children
* Access specific data between opening and closing elements
* `this.props.children` is an array of components when there are multiple nested components

### React Router
* Follow [this tutorial](https://github.com/reactjs/react-router-tutorial/tree/master/lessons)
* React Router is a component
* hashHistory manages routing history with hash in URL
* Create components in modules/ and import them in your routes

``` JavaScript
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
    <Route path="/repos" component={Repos}/>
    <Route path="/about" component={About}/>
  </Router>
```

* `Link` component is aware of the Router it was rendered in
* Nested routes allow us to render a common object on every screen and change the contents of a section
  * e.g. navigation
* Move routes underneath a root route, that root routes component will always be rendered
  * Render children inside root route with `{this.props.children}`

``` JavaScript
<Router history={hashHistory}>
    <Route path="/" component={App}>
      {/* make them children of `App` */}
      <Route path="/repos" component={Repos}/>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
```

* Link components have the `activeClassName` attribute so you can style active links
* Can create a wrapper class to make the app more composable
  * Use spread attribute `...` - properties of the object that you pass in are copied onto the component's props

``` JavaScript
 render() {
    return <Link {...this.props} activeClassName="active"/>
  }
```

* Parameters
  * Paths starting with `:` are URL params
  * Route components can access using `this.props.params[name]`
  * Add route `<Route path="/repos/:userName/:repoName" component={Repo}/>`
  * Use param `{this.props.params.repoName}`

* Index
  * `<IndexRoute component={Home}/>`
  * Becomes `this.props.children` of parent when parents route matches
  * Use `IndexLink` to edit properties like activeClassName
    * Otherwise Home will always be active as / is the parent of everything
    * Alternatively use `onlyActiveOnIndex={true}`

## Container vs Presentational Components, PropTypes, and Stateless Functional Components


## Life Cycle Events and Conditional Rendering


## Axios, Promises, and the Github API


## Rendering UI


## More Container vs Presentational Components


## Private Functional Stateless Components


## Building a Highly Reusable React Component


## React Router Transition Animation and Webpack's CSS Loader
