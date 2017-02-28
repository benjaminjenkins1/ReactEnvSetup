# React Environment Setup

Guide for setting up a minimal react development environment.

In the root directory:

    $ npm init
    $ npm i react react-dom babel-core babel-loader babelify babel-preset-react babel-preset-es2017
    $ npm i webpack webpack-dev-server babel-cli -g
    
- Make index.html in root

- Make build and src directories in root

- Make webpack.config.js in root

- Make main.js in src

index.html:

    <!doctype html>
    <html>
      <head>
        <meta charset="utf-8" />
        <title>React App!</title>
      </head>
      <body>
        <div id="app"></div>
        <script src="build/bundle.js"></script>
      </body>
    </html>
    
main.js:

    import React from 'react';
    import ReactDOM from 'react-dom';
     
    ReactDOM.render(
      <h1>Hello World!</h1>,
      document.getElementById('app')
    );

webpack.config.js:

    module.exports = {
      // entry file
      entry: './src/main.js',
      output: {
        path: __dirname + '/build',
        publicPath: '/build/',
        filename: 'bundle.js'
      },
      // we will use webpack-dev-server
      devServer: {
        inline: true, // reload on the fly (auto refresh)
        port: 4567 // which port to run the server on
      },
      module: {
        // loaders are transformers basically
        loaders: [
          {
            // All files that end with `.js`
            test: /\.js$/,
            // Do not consider node_modules for webpack bundling
            exclude: /node_modules/,
            // use babel as the loader (transformer)
            loader: 'babel',
            // Passing queries/arguments to the loader
            query: {
              presets: ['es2015', 'react']
            }
          }
        ]
      }
    }

To build:

    $ webpack
    
To run dev server:

    $ wepack-dev-server
