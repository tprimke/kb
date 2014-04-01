# React Tutorial, part 1

## The first React - the static component

Now that we know the static HTML document, we can create its React counterpart.

First, we'll modify our HTML document:

```HTML
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>To do</title>
  <script type="text/javascript" src="http://cdnjs.cloudflare.com/ajax/libs/react/0.9.0/react.min.js"></script>
</head>

<body id="app">
  <script type="text/javascript" src="app.js"></script>
</body>

</html>
```

What has been changed:

* the script with React library was added in the head section,
* the body element was given an identifier,
* the script with our application was added at the end of the body section,
* thw whole static, HTML part of the document body has been removed.

Now it's time to write the application. We'll start with using JSX syntax:

```js
/** @jsx React.DOM */

var App = React.createClass({

  render: function() {
    return (
      <div>
        <input type="text" />
        <textarea />
        <button>Save</button>
        <button>Delete</button>
        <ol>
          <li>Item title</li>
        </ol>
        <button>Add new</button>
      </div>
    );
  }

});

React.renderComponent(<App />, document.getElementById('app'));
```

Each component is an *object*, created with the `React.createClass` function. Each component should have the `render` function, which returns the representation of the component.

Let's start from the end: we told React to find the "app" element, and to mount the `<App />` component at this element (DOM node).

The `<App />` component is simply our application. So far, its content is static, and it's very similar to out first, static document. There are some differencies, though:

* The component resides in a `div` element. All React components have to return a single DOM node. The node can be composed of many other nodes, but it has to be a single node.
* The `textarea` element has been denoted in a self-closing XML style. It's one of few differencies between React and HTML.

