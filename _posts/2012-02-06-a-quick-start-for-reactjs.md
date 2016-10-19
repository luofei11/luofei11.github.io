---
layout: post
title: A quick start for ReactJS
---

------

ReactJS has been a very popular web front-end framework that many companies are using to develop their applications. This article introduces how to create a user interface with React.
<!-- more -->
Compared with other frameworks, React provided only a few APIs.
Before using React, we need to know some basic terminologies in order to understand the framework.

## Basic Terminology
| Terminology        | Explanation
| --------   | -----:  |
| React Elements    | JavaScript objects that represent HTML elements |  
| Components        |   Contains one or more React Elements. Used for creating reusable UI modules   |  
| JSX        |    Extensions of JavaScript defined by React(Optional)    |
| Virtual DOM       |    React uses Virtual DOM to render UI and monitors data on the DOM    |

## Demo Preparation
Downloadn Starter Kit at [React download page](http://facebook.github.io/react/downloads.html) and decompress it.

Go to the `build` directory and create `index.html`. Import `react.js` and `JSXTransformer.js` as follows.

```html
<html>
  <head>
    <meta charset="utf-8" >
    <title>demo</title>
  </head>

  <body>

    <script src="react.js"></script>
    <script src="JSXTransformer.js"></script>
    <script type="text/jsx" src="app.js"></script>
  </body>
</html>
```

## First React Element
Call `React.createElement` to create an `Element` and pass the information of the element.
```js
var div = React.createElement('div', null, "Hello React");
// Use JSX
var div = <div>Hello React</div>
```
After that, we can call `React.render` to render the page.
```js
React.render(div, document.body);
```

## First React Component
React Component extracts the structure and logic of the same UI components. Call `React.createClass` to create a Component and pass an object parameter with `render` function.

```js
var HelloMessage = React.createClass({
  render: function () {
    return <div>Hello {this.props.name}</div>;
  }
});

React.render(<HelloMessage name="iissnan" />, document.body);
```
As we see, `React.createClass` receives an object and return the function to `HelloMessage`. Finally, render the component by calling `React.render`. Actually, we can expand the component by adding some structures or functions.

## Props
In the example below, we noticed that there was a special thing: `this.props.name`. It's known as `Props`. We can imagine it as attribute in HTML.
```js
React.render(<HelloMessage name="foo" />, document.body);
```
We use the Props in the Component by `this.props.name`.

## Stateful Component
State indicates the state of the Component. When state changes, React rerenders the UI page. We can access the state by `this.state`.
```js
var Greeting = React.createClass({
  getInitialState: function () {
    return { greeted: false };
  },
  greet: function () {
    this.setState({
      greeted: true
    });
  },
  render: function () {
    var response = this.state.greeted ? 'Hi' : '';

    return (
      <div>
        <div>Hello {this.props.name}</div>
        <span>{response}</span>
        <button onClick={this.greet}>Hi</button>
      </div>
    );
  }
});

React.render(<Greeting name="foo" />, document.body);
```
Here we have more functions. `getInitialState` is called when Component is initialized and returns the state. We set `greeted ` as `false`. `greet` is called to change the state to `true`.
After state has been changed, React renders component on the Virtual DOM and compares it with the old version. At this time, DOM is updated. In this example, `greeted` is changed after the button click event.

## Combination
With combination of Props and State, we can create a complete application using Component.
```js
var Greeting = React.createClass({
  getInitialState: function () {
    return { greeted: false };
  },
  greet: function () {
    this.setState({
      greeted: true
    });
  },
  render: function () {
    var response = this.state.greeted ? 'Hi' : '';

    return (
      <div>
        <div>Hello {this.props.name}</div>
        <span>{response}</span>
        <button onClick={this.greet}>Hi</button>
      </div>
    );
  }
});

var users = ["foo", "bar", "baz"];

var GreetingApp = React.createClass({
  render: function () {
    var greetings = this.props.users.map(function (user) {
      return <Greeting name={user} />;
    });

    return <div>{greetings}</div>;
  }
});

React.render(<GreetingApp users={users} />, document.body);

```
