## Gulp
- Automates repetitive tasks.
- Tasks are just functions that take a callback as an argument, which will be invoked after the task has finished.
- If the callback is called with an argument, that will rise an error.
- series(…tasks) executes each task one after the other. If one fails the process will stop.
- parallel(…tasks)executes all tasks in parallel.
- src(glob: string): locates and reads all the files in the workspace matching the [glob pattern](Gulp globs) passed and returns a stream with their content.
- dest(directory: string): will write the content of the stream into the given folder.
- Gulp also offers a way to watch files, running a task automatically when it detects they’re modified.
- Plugins help you transform all the files in the pipeline.
```
// A task
function task (cb) {
  // ...task logic
  cb();
}
```
```
// File handling
function() {
  return src('src/*.js')
    .pipe(dest('output/'));
}
```
```
// Watch files
var { src, watch, series } = require('gulp');
var gulpMocha = require('gulp-mocha');

function mocha() {
  return src(['src/**.spec.js'], { read: false })
    .pipe(gulpMocha())
    .on('error', log.error);
}

function watchMocha() {
  return watch(['src/**.js'], series(mocha));
}
```
``` 
// Plugins
function() {
  return src('src/*.js')
    .pipe(babel())
    .pipe(dest('output/'));
}
```

## Webpack
- Is a static module bundler for JavaScript.
- Is extensible to other languages and assets.
- Everything starts from the “entry point”. It’s the file where Webpack is going to start crawling from. And the output is the location Webpack writes the bundle to.
- A loader is a processor that can be attached to webpack’s bundling process in order to parse specific files.
- Plugins contain some logic that can be append to the bundling process. They’re meant to do a wide range of tasks with many possibilities.

``` 
// Entry and output
const webpack = require('webpack');
const path = require('path');

const config = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
};

module.exports = config;
```

``` 
// Loader
const config = {
  module: {
    rules: [
      {
        test: /\.txt$/,
        use: 'raw-loader'
      }
    ]
  }
};
```

``` 
// Plugins
const config = {
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```