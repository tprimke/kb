# Frontend Application Structure

This document is based on ["Best Practice Recommendations for Angular App Structure"](https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/pub).

## The main directory

In the main directory, only three files are present:

    our-app/
      index.html
      app.js
      app.css
      components/
      js/

The `index.html` file is the HTML document for our application. This document can load other JS/CSS files, including the files described below.

`app.js` is the JavaScript file for the application. It should be a single file, and it should contain **everything** needed by the app (third-party files might be loaded from other sources).

`app.css` is the CSS file for the application, and it should be loaded as the last CSS file.

The `app.js` and `app.css` files should be created by the app's build script.

The `components` directory is for JSX files and will be discused in detail later.

The `js` directory is for all the JavaScript files, which don't need processing by the React tools. This directory might contain JavaScript modules.

## The React components

All the components should live in the `components` directory:

    our-app/
      index.html
      app.js
      app.css
      components/
        app.jsx
        app.css
        Component1/
          component1.jsx
          component1.css
        Component2/
          component2.jsx
          component2.css
        Component3/
          component3.jsx
          component3.css
          Subcomponent1/
            subcomponent.jsx
            subcomponent.css        
      js/

There are the `app.jsx` and `app.css` files in the `components` directory. The files are for the main application component.

All the other components have their own subdirectories.

