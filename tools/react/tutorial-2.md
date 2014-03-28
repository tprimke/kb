# React Tutorial, part 2

## The first step towards dynamic content

So far, our application is not very impressive. In fact, we had to do much more in order to obtain the same results with React, that we could easily achieve with the old, plain HTML.

Now, let's try to do something more interesting. The application should show a list of items to do, and we're simply showing a list with one, static item. Let's define a list of items, and let's prepare a shadow DOM representation for all of them:

```js
/** @jsx React.DOM */

var App = React.createClass({

  render: function() {

    var items = [
      { title: 'Water the flowers', desc: '' },
      { title: 'Call James', desc: '' },
      { title: 'Cook the dinner', desc: '' }
    ];

    var lis = items.map( function(item) {
      return <li>{item.title}</li>;
    });

    return (
      <div>
        <input type="text" />
        <textarea />
        <button>Save</button>
        <button>Delete</button>
        <ol>
          {lis}
        </ol>
        <button>Add new</button>
      </div>
    );
  }

});

React.renderComponent(<App />, document.getElementById('app'));
```

Now, the `render` function starts with a definition of the list of items.

Then, the list is processed, and a list of `li` items is prepared. Each `li` element should diplay the title of its item.

Finally, the prepared list of `li` items is rendered as a fragment of our application (shadow) DOM representation.

## Properties

Of course, defining the list of items in a render function is not a good idea. Such a list should be *passed* to our component. In React, we can pass **any** JavaScript object to a component, as a property:

```js
/** @jsx React.DOM */

var App = React.createClass({

  render: function() {

    var items = this.props.items;

    var lis = items.map( function(item) {
      return <li>{item.title}</li>;
    });

    return (
      <div>
        <input type="text" />
        <textarea />
        <button>Save</button>
        <button>Delete</button>
        <ol>
          {lis}
        </ol>
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

Now, we define our items as a global object, and then simply pass it to the application as a property.

Well, it's still not as good, as it should be: items should be kept in a separate module. Here, we sacrifice the application's structure design for keeping everything in one file.

