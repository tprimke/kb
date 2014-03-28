# React Tutorial, part 3

## The first step towards KISS

Properties are great, but handling values (and that's what properties are for) is not the only problem. Our application is quite simple, and it consists of many different elements: we have a form and a list, and the form consists of many fields, and the list consists of many items...

It might not seem as a problem *right now*, but in practice things get complicated very fast.

We should decompose our application into different components.

We'll start with the form, since it's static (so far):

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

var App = React.createClass({

  render: function() {

    var items = this.props.items;

    var lis = items.map( function(item) {
      return <li>{item.title}</li>;
    });

    return (
      <div>
        <Form />
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

The things to notice are:
* A new component has been introduced - the `Form`.
* Our application's code became more clear - now we can see it consists of a `Form` and... something else (the HTML code is much less clear).
* Since all the React components have to be mounted in a single DOM element, the `Form` components resides in a `div`. So, a new `div` has been introduced to the DOM.

## Passing properties to children

The form looks much better now (in the code, of course), so let's continue this decomposition. Now it's time to make the list of items a separate component.

This is a different component, though. The list needs the item's data to render - so we'll have to pass the items to this child component:

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

The things to notice:
* The list is represented as an `ol` element, so in this case the output will be the same, as previously. We don't need to introduce any new `div` elements.
* The application's code became even more clear. Now even a newbie can say, that our application consists of a form, and some list of items.

## How far we should go in decomposition?

That's an interesting question. I don't think there's a clear answer.

Let's try to answer a different question first: why we use React components?

We use them, since they allow us to develop apps faster. We don't have to think about all the details (like HTML elements, and JS code handling those elements) - we can use ready components. So, our goal should be to create many reusable components.

A component is reusable, when it can be used in many places. On the other hand, when a component is simply a single HTML element (without any simplified semantics, like properties and JS behaviour), there's no difference between using React components and pure HTML.

In our case, it would be pointless to decompose the list of items into single items. Thus we have a whole list as a single component.

The form, on the other hand, is composed of `input`s and `button`s, and those elements can have their own semantics. It's very likely, that in some future versions of our application, we would use other forms, composed of the same (or very similar) elements. So we can suppose, that the `Form` element could be decomposed further.

