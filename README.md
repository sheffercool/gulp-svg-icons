gulp-svg-icons [![Build Status](https://travis-ci.org/coma/gulp-svg-icons.png?branch=master)](https://travis-ci.org/coma/gulp-svg-icons)
==============

Inserting SVG icons was never so easy.

Install
-------

```
npm install gulp-svg-icons
```

Usage
-----

In your HTML sources just add icons like:

```html
<icon-trophy class="red">
```

and it will be replaced by:

```html
<svg class="icon red" viewBox="0 0 30 32"><use xlink:href="#icon-trophy"></use></svg>
```

where "trophy" is the name of the icon's file (path/to/the/icons/trophy.svg); and use the placeholder where you want the definitions (in the index.html for example, in case that you are building a SPA):

```html
<!-- icons -->
```

and then invoke it through gulp:

```javascript
var gulp  = require('gulp');
var Icons = require('gulp-svg-icons');

var icons = new Icons('src/icons');

gulp.task('replace', function() {

	var htmls = path.join(fixtures, 'html', '**', '*.html');

	return gulp
	        .src('src/html/*.html')
	        .pipe(icons.replace())
	        .pipe(gulp.dest('web'));
});

gulp.task('default', ['replace'], function() {

	return gulp
	        .src('web/index.html')
	        .pipe(icons.inject())
	        .pipe(gulp.dest('web'));
});
```

Options
-------

### prefix

An string to use on every icon id (concatenated using "-") or a falsy value (false, null...) to avoid prefixes.

### placeholder

An string to be replaced with the icons definitions. The default is ```<!-- icons -->```.

### style

A function which will receive every icon name and should return the desired CSS class name. The default will return just ```icon```.

### external

A function which will receive every icon name and should return the desired path to the icons defs, useful to keep those in an external file (and share them between documents, [see this](http://css-tricks.com/svg-use-external-source/)). The default will return just an empty string, meaning that the icons are supposed to be defined in the same document.
