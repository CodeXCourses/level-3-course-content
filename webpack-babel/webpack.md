# Webpack

### Default Settings

These are default Webpack settings that DO NOT need to be in `webpack.config.json` and `webpack.config.js`:

Webpack resolves JavaScripts files, so it's unnecessary to include `.js` when importing from a JavaScript file:
```json
"resolve": {
  "extensions": ['.js', '.json', '.wasm']
}
```

Webpack starts with `index.js` in the `src` folder:
```json
"entry": "./src/index.js"
```

Webpack outputs `main.js` to the `dist` folder: 
```json
"output": {
  "filename": "main.js",
  "path": "./dist"
}
```

### Default Webpack Folder Structure

```
├── dist
│   ├── main.js
├── src
│   ├── index.js
└── index.html
```

### No Config

With no config file and the default folder structure:
- Webpack allows the use of node modules in HTML/JavaScript/CSS projects (no React).
- The `index.html` file should import `./dist/main.js`

### Minimal React Config

This config will run a Hello World React application and other simple projects:

NOTE: All JavaScript files, including React components, should end with `.js`
```json
{
  "modules": {
    "rules": [
      {
        "use": "babel-loader"
      }
    ]
  }
}
```
webpack.config.json

### Practical Minimal React Config

This config will run a Hello World React application and other simple projects, but also:
- Watch for changes and re-bundle
- Enable the debugger
- Enable the debugger with original source code

NOTE: All JavaScript files, including React components, should end with `.js`
```json
{
  "modules": {
    "rules": [
      {
        "use": "babel-loader"
      }
    ]
  },
  "watch": true,
  "mode": "development",
  "devtool": "source-map"
}
```
webpack.config.json

### Build Errors

As more node modules are added to the project, build errors may occur as web servers (like Live Server) prematurely render pages before Webpack finishes bundling. To fix, add a delay to the server, or add a delay to Webpack:

NOTE: Increase the delay by 1-second increments if build errors occur.
```json
"watchOptions": {
  "aggregateTimeout": 1000
}
```
webpack.config.json

### Level 3 Config File

This config file includes features to cover level 3 topics:
- JSX files
- Style imports
- Asset imports

```javascript
export default {
  //MODULES ARE FILES THAT ARE IMPORTED
  module: {
    //RULES ARE A LIST OF WAYS TO PROCESS THE MODULES
    rules: [
      {
        exclude: /\.(json)/, //NOT .json FILES
        test: /\.(js|jsx)/, //JAVASCRIPT AND REACT FILES
        use: "babel-loader", //USE THIS LOADER TO PROCESS THE MODULES ABOVE
      },
      {
        test: /\.(scss|css)/, //STYLE MODULES
        use: ["style-loader", "css-loader", "sass-loader"], //USE THESE LOADERS TO PROCESS MODULES ABOVE
      },
      {
        test: /\.(jpg|png|mp4)/, //ASSET FILES
        type: "asset/resource", //THIS BUILT-IN FEATURE PROCESSES ASSETS.
      },
    ],
  },
  watch: true, //WATCH FOR CODE CHANGES. PRESS CTRL+C TO CANCEL
  watchOptions: { aggregateTimeout: 2000 }, //USE A DELAY TO AVOID BUILD ERRORS
  mode: "development", //ENABLES THE DEBUGGER
  devtool: "source-map", //ENABLES DEBUGGER CODE TO MATCH ACTUAL CODE
};
```
webpack.config.js
