gulp-ejs-precompiler
====================

A plugin for gulp that precompiles ejs templates


```js
var ejsPrecompiler = require('gulp-ejs-precompiler');
var concat = require('gulp-concat');
var insert = require('gulp-insert');

// Sample of task config
var config = {
    src: '/path/to/ejs/templates/*.ejs', // The ejs source files
    dist: '/path/to/compiled/ejs/', // Path where the compiled file will be stored
    filename: 'templates.js', // Name of the complied file
    templateVarName: 'templates',
};

gulp.task('ejs', function() {
    return gulp.src(config.src)
        .pipe(
            ejsPrecompiler({
                templateVarName: config.templateVarName,
                compileDebug: true,
                client: true,
            }).on('error', function(err) {
                console.log('EJS Precompiler error', err);
                this.emit('end');
            })
        )
        .pipe(concat(config.filename))
        .pipe(insert.prepend('window.' + config.templateVarName + ' = {};'+"\n"))
        .pipe(gulp.dest(config.dist));
});
```

## Options

- templateVarName (String): the javascript variable name. _Default: templates_
- fileExtension (String): the template source file extension. _Default: .ejs_

_Others options are directly given to gulp ejs for compilation. See [gulp-ejs](https://www.npmjs.com/package/gulp-ejs) for more information._
