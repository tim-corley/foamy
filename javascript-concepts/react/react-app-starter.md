## How to Get Started with a Fresh React App

### create-react-app 

https://github.com/facebook/create-react-app

```bash
npx create-react-app my-new-app
```

### nano-react-app

a stripped-down, bare-bones version of create-react-app 

https://github.com/nano-react-app/nano-react-app

```bash
npx nano-react-app my-new-app
```

### custom

step-by-step installs

 - __tools:__
 - webpack - a build process / bundler (similar to gulp)
 - babel - converts code (i.e. ES6) into something browsers understand (i.e. older versions)

https://www.freecodecamp.org/news/part-1-react-app-from-scratch-using-webpack-4-562b1d231e75/

#### project structure 

1) create project directory
```bash
➜  React git:(master) ✗ mkdir scratch-starter-app && cd $_
```
2) create package.json (autocomplete questions)
```bash
➜  scratch-starter-app git:(master) ✗ npm init -y
```
3) install webpack & webpack-cli 
```bash 
➜  scratch-starter-app git:(master) ✗ npm i webpack webpack-cli -D
```
4) create a __src__ folder with `index.js` file in it
```bash
➜  scratch-starter-app git:(master) ✗ mkdir src && cd $_ && touch index.js
```
5) add some content to the `index.js` file
```bash
➜  src git:(master) ✗ nano index.js
➜  src git:(master) ✗ cat index.js 
console.log('Hello There!');
```
6) add start & build script to __package.json__
```json
...
"scripts": {
    "start": "webpack --mode development",
    "build": "webpack --mode production"
  
},...
```
7) execute the `start` script (this will create a dist folder with main.js file inside - containing your src code)
```bash
npm run start
```

should now have a project structure like:
```
├── dist
│   └── main.js
├── node_modules
├── package.json
├── package-lock.json
└── src
    └── index.js
```

running: `npm run build` will minify the code in `dist/main.js`

#### react & babel setup

8) install react & react-dom   
```bash
➜  scratch-starter-app git:(master) ✗ npm i react react-dom -S
```
9) install babel
```bash
➜  scratch-starter-app git:(master) ✗ npm i babel-core babel-loader@^7 babel-preset-env babel-preset-react -D
``` 
 - __babel-core:__ Transforms your ES6 code into ES5
 - __babel-loader:__ Webpack helper to transform your JavaScript dependencies (for example, when you import your components into other components) with Babel
 - __babel-preset-env:__ Determines which transformations/plugins to use and polyfills (provide modern functionality on older browsers that do not natively support it) based on the browser matrix you want to support
- __babel-preset-react:__ Babel preset for all React plugins, for example turning JSX into functions
10) at root, create a __webpack.config.js__ file to state the rules for our babel-loader
```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
```
11) at root, create a file called __.babelrc__ to provide the options for babel-loader. when it is stated that project is using babel-loader in the webpack config, it will look for this file. 
```
{
  "presets": ["env", "react"]
}
```
12) update __index.js__ so that it renders a react component
```javascript
import React from "react";
import ReactDOM from "react-dom";

const Index = () => {
  return <div>Hello React!</div>;
};

ReactDOM.render(<Index />, document.getElementById("index"));
```
13) in __src/__, create an __index.html__ file
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>React and Webpack4</title>
</head>
<body>
  <section id="index"></section>
</body>
</html>
```
14) install __html-webpack-plugin__ as a dev dependency (used in webpack config file to generate an HTML file with `<script>` injected, write this to dist/index.html, and minify the file)
```bash
npm i html-webpack-plugin -D
```
15) update the __webpack.config.js__ file
```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");

const htmlPlugin = new HtmlWebPackPlugin({
  template: "./src/index.html",
  filename: "./index.html"
});

module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  },
  plugins: [htmlPlugin]
};
```
16) execute `npm run start` to see an __index.html__ file create in the __dist/__ dir
 - _if error, make sure versions (webpack & babel) align - see: https://stackoverflow.com/questions/49182862/preset-files-are-not-allowed-to-export-objects_

17) open, in the browser, the __dist/index.html__ file 
```bash
➜  scratch-starter-app git:(master) ✗ google-chrome dist/index.html
```

#### webpack-dev-server setup 

have webpack “watch” for changes and thus refresh whenever changes are made to any components

18) install 
```bash
npm i webpack-dev-server -D
```
19) update the start script in __package.json__
```json
  ...
  "scripts": {
    "start": "webpack-dev-server --mode development --open",
    "build": "webpack --mode production"
  },...
```
#### css setup

20) install dependencies
```bash
npm i css-loader style-loader -D
``` 
21) update __webpack.config.js__
```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");

const htmlWebpackPlugin = new HtmlWebPackPlugin({
  template: "./src/index.html",
  filename: "./index.html"
});

module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  plugins: [htmlWebpackPlugin]
};
```
22) make css modular by providing some options to css-loader. this means class name will be scoped locally and specific to only the component in question.
`webpack.config.js`
```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");

const htmlWebpackPlugin = new HtmlWebPackPlugin({
  template: "./src/index.html",
  filename: "./index.html"
});

module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            modules: true,
            importLoaders: 1,
            localIdentName: "[name]_[local]_[hash:base64]",
            sourceMap: true,
            minimize: true
          }
        }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  plugins: [htmlWebpackPlugin]
};
```

the localIdentName allows you to configure the generated identification.

 - __name__ - will take the name of your component
 - __local__ - is the name of your class/id
 - __hash:base64__ - is the randomly generated hash which will be unique in every component’s CSS. For example, say there is a component named Form and a button with a CSS class primaryButton. also another component called Search and a button in it with a CSS class primaryButton. However, both of these classes have different CSS:
```css
Form button.primaryButton {
  background-color: green;
}
Search button.primaryButton {
  background-color: blue;
}
```

NOTE: at this point, running: `npm run start` produces an error 
```
Using removed Babel 5 option: base.modules - Use the corresponding module transform plugin in the `plugins` option.
```

to be in a good position moving forward, i want to configure my default starter app with the latest version of Webpack (4) and Babel (7). additionally, when it comes to incorporating styling I want to use tailwind css and styled components since i have used that combo in the past. 

going to use a new guide to get Webpack4 & Babel7 configured and will remove styling pieces added above. 

https://blog.logrocket.com/webpack-from-scratch-for-tailwind-css-with-react/

```bash
➜  scratch-starter-app git:(master) ✗ npm uninstall css-loader style-loader -D
➜  scratch-starter-app git:(master) ✗ npm uninstall babel-plugin-add-module-exports --save-dev
➜  scratch-starter-app git:(master) ✗ npm i babel-loader @babel/core @babel/preset-env @babel/preset-react @babel/cli -D
```

#### tailwind css setup

```bash
➜  scratch-starter-app git:(master) ✗ npm i tailwindcss autoprefixer postcss-cli mini-css-extract-plugin postcss-loader --save-dev
```

A) generate a Tailwind config file
```bash
➜  scratch-starter-app git:(master) ✗ ./node_modules/.bin/tailwind init tailwind.config.js
```

B) (at root) create a file called __postcss.config.js__ and add:
```javascript
const tailwindcss = require('tailwindcss');
module.exports = {
    plugins: [
        tailwindcss('./tailwind.config.js'),
        require('autoprefixer'),
    ],
};
```

C) inside of __src/__, create a __styles.css__ and add:
```css
@tailwind preflight;

@tailwind components;

@tailwind utilities;

/* Custom css */
```

D) enable import of css files into react components 
```bash
npm i css-loader style-loader -D
```
and update the __webpack.config.js__ file 
```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
       {
        test: /\.css$/,
        use: [
          MiniCssExtractPlugin.loader,
          "css-loader", "postcss-loader",
          ],
      },
    ]
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: "styles.css",
      chunkFilename: "styles.css"
    }),
    new HtmlWebPackPlugin({
    template: "./src/index.html",
    filename: "./index.html"
  }),
]
};
```





more resources:
 - https://blog.logrocket.com/webpack-from-scratch-for-tailwind-css-with-react/
 - https://hashinteractive.com/blog/webpack-configuration-for-react-and-tailwindcss/
 - https://www.freecodecamp.org/news/how-to-combine-webpack-4-and-babel-7-to-create-a-fantastic-react-app-845797e036ff/
 - https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658
 - https://www.valentinog.com/blog/babel/
 - https://webpack.js.org/
 - https://www.youtube.com/watch?v=nfmvexyoHXE
 - https://babeljs.io/
 - https://www.youtube.com/watch?v=ahh65GQz74g