# React Theory

## The direction of data flow

Let's take a look at the last example from the third tutorial:

```js
/** @jsx React.DOM */

var Form = React.createClass({

  render: function() {
    return (
      <div>
        <input type="text" />
        <textarea />
        <button>Save</button>
        <button>Delete</button>
      </div>
    );
  }

});

var ItemsList = React.createClass({

  render: function() {

    var items = this.props.items;

    var lis = items.map( function(item) {
      return <li>{item.title}</li>;
    });

    return (
      <ol>
        {lis}
      </ol>
    );
  }

});

var App = React.createClass({

  render: function() {

    var items = this.props.items;

    var lis = items.map( function(item) {
      return <li>{item.title}</li>;
    });

    return (
      <div>
        <Form />
        <ItemsList items={this.props.items} />
        <button>Add new</button>
      </div>
    );
  }

});

var items = [
  { title: 'Water the flowers', desc: '' },
  { title: 'Call James', desc: '' },
  { title: 'Cook the dinner', desc: '' }
];

React.renderComponent(<App items={items} />, document.getElementById('app'));
```

The `items` are declared as a global variable. Then, they're passed to the main application component, `App`. And from the `App`, they are passed to the list of items, which is a separate component.

This direction of data flow is essential for React, and essential for the React's simplicity. The data always flows in **one direction**: from the parent, to the children. **It's impossible to pass data from a child component to some ancestor.**

At first, it might seem a very limiting solution: how the data from our `Form` could be passed to the list of items? It will be explained in the following tutorials. For now, let's focus on another aspect of this feature: since the data is passed always in the same direction, it's much easier to reason about components, to control them, to design them and to maintain them. And that's why React is so easy to use.

