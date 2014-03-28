# React Tutorial, part 1

## A TODO application

Every time you have to do something with React, start with a deep understanding of the problem.

A TODO application is a simple, single-page application (SPA), that is supposed to:

* allow end-user to enter a new todo item,
* allow end-user to view a list of all todo items,
* allow end-user to delete any of the todo items in the list,
* allow end-user to modify any of the todo items in the list.

This application can be composed of a form, used to edit a todo item data, and a simple, (probably ordered) list of items.

## The model

But what is this TODO item?

Well, it can be everything we want it to be, but let's assume that a TODO item can be represented with a JavaScript object (so called "plain old JavaScript object", POJO) of two properties: a title, and some description:

```js
var todo_item = {
  title: 'A title',
  desc: 'Some description.'
};
```

We can store such items in an array:

```js
var items = [];
```

(Yeap. The list is empty. It should be populated by the application.)

## The HTML document

Let's design a (dead) simple HTML document for our application:

```HTML
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>To do</title>
</head>

<body>
  <input type="text" />
  <textarea></textarea>
  <button>Save</button>
  <button>Delete</button>
  <ol>
    <li>Item title</li>
  </ol>
  <button>Add new</button>
</body>

</html>
```

The `input` element is for the item's title. The description can be written with the `textarea`.

The items are presented in a simple, ordered list. Each item's title is a `li` element.

When an item is clicked, it should be somehow highlighted; the values of the `input` and `textarea` elements should be properly set, and the buttons Save and Delete should be enabled.

After the "Add new" button is pressed, a new item should be added to the list.

## The first React - the static component

Now, let's create (almost) the same app using React.

First, we'll modify out HTML document:

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
* the script with our application was added at the end of the body section.

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

