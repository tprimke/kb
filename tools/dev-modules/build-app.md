# Building Apps

For building applications (processing various JS dialects, compilation of JS and CSS files, etc.), we use [gulp](http://gulpjs.com/).

Before gulp can be used, it should be installed **globally**:

    $ npm install -g gulp

For each project, a bunch of modules should be installed **locally**:

    $ npm install —save-dev gulp gulp-concat gulp-clean gulp-react run-sequence

For now, the following gulpfile.js is used:

```js
var gulp   = require('gulp'),
    clean  = require('gulp-clean'),
    concat = require('gulp-concat'),
    react  = require('gulp-react'),
    seq    = require('run-sequence');

gulp.task('clean', function() {
  return gulp.src('build', {read: false})
             .pipe(clean());
});

gulp.task('compile-jsx', function() {
  return gulp.src('src/**/*.jsx')
             .pipe(react())
             .pipe(gulp.dest('build'));
});

gulp.task('build-components', function() {
  return gulp.src('build/components/**/*.js')
             .pipe(concat('components.js'))
             .pipe(gulp.dest('build'));
});

gulp.task('build-js', function() {
  return gulp.src('src/**/*.js')
             .pipe(concat('libs.js'))
             .pipe(gulp.dest('build'));
});

gulp.task('build-app', function() {
  return gulp.src(['build/libs.js', 'build/components.js', 'build/app.js'])
             .pipe(concat('app.js'))
             .pipe(gulp.dest('.'));
});

gulp.task('build-css', function() {
  return gulp.src('src/**/*.css')
             .pipe(concat('app.css'))
             .pipe(gulp.dest('.'));
});

gulp.task('build', function() {
  seq('clean',
      'compile-jsx',
      ['build-components', 'build-js'],
      ['build-app', 'build-css']);
});
```

The application can be built with the command:

    $ gulp build
