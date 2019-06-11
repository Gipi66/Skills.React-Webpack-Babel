### Init project
- yarn init
- conifg npm project:
	```
	npm config list

	npm set init.author.name "<Your Name>"
	npm set init.author.email "you@example.com"
	npm set init.author.url "example.com"
	npm set init.license "MIT"
	```
- add webpack deps:
	`npm install --save-dev webpack webpack-dev-server webpack-cli`

- add scripts to project config:
	```
	  "scripts": {
	  	"start": "webpack-dev-server --config ./webpack.config.js --mode development"
	  }
  ```

- add webpack config to `touch webpack.config.js`:
	```
	module.exports = {
	  entry: './src/index.js',
	  output: {
	    path: __dirname + '/dist',
	    publicPath: '/',
	    filename: 'bundle.js'
	  },
	  devServer: {
	    contentBase: './dist'
	  }
	};
	```
- create file `src/index.js`:
	```
	console.log('My Minimal React Webpack Babel Setup');
	```

### Babel setup
- deps: `npm install --save-dev @babel/core @babel/preset-env babel-loader @babel/preset-react`
- add babel presets to `package.json`:
    ```
    "babel": {
      "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
      ]
    },
    ```
- update `webpack.config.js`:
    ```
    module: {
        rules: [
          {
            test: /\.(js|jsx)$/,Webpack
            exclude: /node_modules/,
            use: ['babel-loader']
          }
        ]
        },
        resolve: {
            extensions: ['*', '.js', '.jsx']
    },
    ```
- add babel config `.babelrc`:
    ```
    {
      "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
      ]
    }
    ```

### Include React part
* install react `npm install --save react react-dom`
* update `src/index.js`
    ```
    import React from 'react';
    import ReactDOM from 'react-dom';
    
    const title = 'My Minimal React Webpack Babel Setup';
    
    ReactDOM.render(
      <div>{title}</div>,
      document.getElementById('app')
    );
    ```
* hot module replacement 
    - `npm install --save-dev react-hot-loader`:
    -  put into the `webpack.config.js`:
        ```
        const webpack = require('webpack');
        
        module.exports = {
          entry: './src/index.js',
          module: {
            rules: [
              {
                test: /\.(js|jsx)$/,
                exclude: /node_modules/,
                use: ['babel-loader']
              }
            ]
          },
          resolve: {
            extensions: ['*', '.js', '.jsx']
          },
          output: {
            path: __dirname + '/dist',
            publicPath: '/',
            filename: 'bundle.js'
          },
          plugins: [
            new webpack.HotModuleReplacementPlugin()
          ],
          devServer: {
            contentBase: './dist',
            hot: true
          }
        };
        ```
    - add to end of the `src/index.js`:
        ```
        module.hot.accept();
        ```


### How to run:
- `npm start`
