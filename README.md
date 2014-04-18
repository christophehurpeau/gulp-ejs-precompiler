gulp-ejs-precompiler
====================

A plugin for gulp that precompiles ejs templates


```js
var ejs = require('gulp-ejs-precompiler');
var concat = require('gulp-concat');

gulp.task('ejs', function() {
    return gulp.src(paths.browser.templatesEJS)
        .pipe(plumber())
        .pipe(ejs({
            compileDebug: true,
            client: true
        }))
        .pipe(concat(pkg.name + /*'-' + pkg.version +*/ '.templates.js'))
        .pipe(insert.prepend('window.templates = {};'+"\n"))
        .pipe(gulp.dest(paths.dist));
});
