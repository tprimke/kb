# Unit testing

## Why mocha?

Because **I** like much more, than anything else (including Jasmine and QUnit).

Besides, AFAIK, the (probably more popular) tools like Jasmine and QUnit are unable to test JS code on the server side, and my idea is to use the same tool on the server side and in the browser.

## Unit testing on the server side

TODO

(Although the topic is quite easy.)

## Unit testing in the browser

Here is the template for the HTML test runner:

```HTML
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>Tests</title>
  <link rel="stylesheet" href="css/mocha.css" />
  <script src="js/should.js"></script>
  <script src="js/mocha.js"></script>
  <script>mocha.setup('bdd')</script>
  <!-- additional libraries -->
  <script src="js/lodash.min.js"></script>

  <!-- The tested sources -->
  <script type="text/javascript" src="..."></script>

  <!-- The tests -->
  <script type="text/javascript" src="..."></script>

  <!-- The runner -->
  <script>
    onload = function() {
      mocha.run();
    };
  </script>
</head>

<body>
  <div id="mocha"></div>
</body>
</html>
```

The things to note:

* The mocha and should js/css files should be downloaded from the local directory (I haven't found them on any CDN).
* After mocha JS file is loaded, the BDD tests style should be set (yes, it's a matter of my personal preference).
* A single div of id set to "mocha" should be added to the document body.

The gulp test building task should be responsible for preparing the JS files and specs for the browser. (Be careful - in browser, no `require` will work, so the spec files shouldn't contain any `require` calls.)

