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
 
* Passing params in routes
  * Define route e.g. `<Route path='playerOne' header='Player One' component={PromptContainer} />`
  * We want to extract what's in *header*
  * In PromptContainer.js we can use `{this.props.route.header}`

* Index
  * `<IndexRoute component={Home}/>`
  * Becomes `this.props.children` of parent when parents route matches
  * Use `IndexLink` to edit properties like activeClassName
    * Otherwise Home will always be active as / is the parent of everything
    * Alternatively use `onlyActiveOnIndex={true}`

## Container vs Presentational Components, PropTypes, and Stateless Functional Components

### Stateless Functional Components

* Most components take in data via props and output some UI
* Ideal paradigm for splitting components into containers and presentational components
* e.g. the following can become a stateless functional component by removing the render method
* Use when just dealing with UI and PropTypes

``` JavaScript
var HelloWorld = React.createClass({
  render: function () {
    return (
      <div>Hello {this.props.name}</div>
    )
  }
})
ReactDOM.render(<HelloWorld name='NAME' />, document.getElementById('app'))
```
To

``` JavaScript
function HelloWorld (props) {
  return (
    <div>Hello {props.name}</div>
  )
}
ReactDOM.render(<HelloWorld name='Tyler' />, document.getElementById('app'))
```

### PropTypes
* Allows for type checking properties passed to components

``` JavaScript
var React = require('react')
var PropTypes = React.PropTypes
var Icon = React.createClass({
  propTypes: {
    name: PropTypes.string.isRequired,
    size: PropTypes.number.isRequired,
    color: PropTypes.string.isRequired,
    style: PropTypes.object
  },
  render: ...
});
```

### Containers
* Deals with functional work
* Components deal with presentational work

### Link
* Use when in another component and want to link to a defined route
* Import `ReactRouter.Link`
* `<Link to="/route-name-here">text</Link>


### State
* e.g. you have a form which has a field with the username that you want to save
* We first initialise all states with a `getInitialState` function that initialise all fields
  * e.g. `return { username: '' }`

``` JavaScript
 <input
   className="form-control"
   placeholder="Github Username"
   onChange={this.onUpdateUser}
   value={this.state.username}
   type="text" />
```

* onChange is fired when the field is changed
* Define the `onUpdateUser` function to use `this.setState` to change the state of the username
  * Take in arg `e` and get the value using `e.target.value`

### Context
* Use to switch routes
* Avoid needing to pass through props
* Take `router` from `contextTypes`
* Use `this.context.router.push` to change route

## Life Cycle Events and Conditional Rendering

* Render method needs to be a pure function - receive state and props, render UI
* Where to put state, Ajax requests, etc.?
* Lifecycle methods allow us to hook into views when specific conditions happen e.g first render
* 2 main categories
 * Component un/mounted from/to DOM
 * Component receives new data

Life cycle events

* `getDefaultProps()`
* `getInitialState()`
* `componentWillMount()`
* `render()`
* `componentDidMount()`

Events called when component receives new data from parent

* `componentWillReceiveProps` execute code when component receives new props
* `shouldComponentUpdate` implement to return a bool whether or not to update component

![react lifecycle][lifecycle]


### Mounting/Unmounting

* Component initialised and added to DOM (mounting)
* Component removed from DOM (unmounting)
* Invoked once during life of component

#### Establish default props in component
* Prop has a default value
* `getDefaultProps`
* e.g. loading component that took in text, have a default value if none provided

``` JavaScript
var Loading = React.createClass({
  getDefaultProps: function () {
    return {
      text: 'Loading'
    }
  },
  render: function () {
    ...
  }
})
```

#### Set initial state in component

* `getInitialState`
* Set initial state of component when first added to DOM
* Update state using `this.setState` and pass in object to overwite email/password properties

``` JavaScript
var Login = React.createClass({
  getInitialState: function () {
    return {
      email: '',
      password: ''
    }
  },
  render: function () {
    ...
  }
})
```

#### AJAX request to fetch data needed for component

* `componentDidMount`
* Called after mounted
* e.g. Axios fetches data tehn calls callback fn

``` JavaScript
var FriendsList = React.createClass({
  componentDidMount: function () {
    return Axios.get(this.props.url).then(this.props.callback)
  },
  render: function () {
    ...
  }
})
```

#### Setup listeners e.g. websockets or firebae

* `componentDidMount`

``` JavaScript
var FriendsList = React.createClass({
  componentDidMount: function () {
    ref.on('value', function (snapshot) {
      this.setState({
        friends: snapshot.val()
      })
    })
  },
  render: function () {
    ...
  }
})
```


#### Remove listeners upon unmounting

* Remove when component removed to prevent memory leaks
* `componentWillUnmount`

``` JavaScript
var FriendsList = React.createClass({
  componentWillUnmount: function () {
    ref.off()
  },
  render: function () {
    ...
  }
})
```

## Axios, Promises, and the Github API

### this

* Where was this function invoked?

#### Implicit binding

* Most common
* Left of the dot at call time
* e.g. `me.callName()`
* We can nest functions, will check if left of dot has property

#### Explicit binding

* call, apply, bind
* `var sayName = function(lang1, lang2, lang3)`
* `call`
 * e.g. `sayName.call(stacey, languages[0], languages[1], languages[2])`
 * Context to call function in
 * Args after the first are params
* `apply`
 * Similar to call, parses objects in an array for us
 * e.g. `sayName.apply(stacey, languages) //languages is an array of 3 elements`
* `bind`
 * Returns a new function instead of invoking one
 * e.g. `var newFn = sayName.bind(stacey, languages[0], languages[1], languages[2])`


#### new binding

* When `new` keyword used
* `this` is bound to a new object

#### window binding 

* `var sayAge = function() { console.log(this.age); }'`
* If `this` is not set through implicit or explicit binding, it uses `window`
* e.g. `sayAge()` will output undefined
* `window.age = 25;` then `sayAge()` will output `25`

### Axios

* Uses promises
* `axios.get` sends a GET request to the URL
* `axios.all` takes in an array of promises, waits for all to be resolved and then executes callback

## More Container vs Presentational Components

### Reduce

* Take a list of items and convert them into one new item
* e.g. sum an arary of integers
* `.reduce` takes a callback function and an initial value
* Callback function takes in 2 parameters
* Reducer uses the initial value with the first element for the first call of the callback
* Returned element acts as the accumulator for the next iteration

``` JavaScript
var scores = [89, 76, 47, 95]
var initialValue = 0
var reducer = function (accumulator, item) {
  return accumulator + item
}
var total = scores.reduce(reducer, initialValue)

var votes = [
  'tacos',
  'pizza',
  'pizza',
  'tacos',
  'fries',
  'ice cream',
  'ice cream',
  'pizza'
]
var initialValue = {}
var reducer = function(tally, vote) {
  if (!tally[vote]) {
    tally[vote] = 1;
  } else {
    tally[vote] = tally[vote] + 1;
  }
  return tally;
}
var result = votes.reduce(reducer, initialValue) // {tacos: 2, pizza: 3, fries: 1, ice cream: 2}
```

## Private Functional Stateless Components

### Private Components

* Similar to a private function
* Ideal for modularity
* Have a stateless functional component call another stateless functional component

``` JavaScript
var React = require('react');
function FriendItem (props) {
  return <li>{props.friend}</li>
}
function FriendsList (props) {
  return (
    <h1>Friends:</h1>
    <ul>
      {props.friends.map((friend, index) => <FriendItem friend={friend} key={friend} />)}
    </ul>
  )
}
module.exports = FriendsList
```

## Building a Highly Reusable React Component


## React Router Transition Animation and Webpack's CSS Loader


[lifecycle]: http://i.imgur.com/peYbIzH.png
