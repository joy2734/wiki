# Webpack + React + Meterial UI + Bootstrap  초기세팅

<br>
<br>

## init Project
   
 - exec  
   `npm init`

<br>
<br>

## React Install

 * `react` - React 라이브러리
 * `react-dom` - React Dom이 rendering 할 수 있게 도와준다.
 
 <br>
 
 - exec  
   `yarn add react react-dom`

<br>
<br>

## Babel Install

 * `@babel/core` - 리액트는 ES6를 사용하므로 크로스브라우징이 가능하도록 ES5 문법으로 바꿔줌
 * `@babel/preset-react` - jsx를 javascript로 변환해준다.
 * `@babel/preset-env`
   - ES6를 ES5로 변환해준다.
   - ES6만이 아니라 브라우저에 따라서 컴파일해준다.
 * `babel-loader`
   - 자바스크립트 파일을 babel preset/plugin 과 webpack을 사용하여 ES5로 컴파일 해주는 플러그인.
   - jsx를 javascript로 변환해준다.
   - html webpack plugin
<br>

 - exec  
   `npm install --save-dev @babel/core babel-loader @babel/preset-react @babel/preset-env `

<br>
<br>

## Webpack Install

 * `webpack` - 모든 리액트 파일을 컴파일된 `하나의 자바스크립트 파일`(index.js)에 번들링 함.
 * `webpack-dev-server` - 개발시 소스변경시 `live reload` 해주는 기능
 * `webpack-cli` - build 스크립트를 통하여 webpack 커맨드를 사용한다.
 * `html-webpack-plugin` - webpack.config.js 에서 사용되는 플러그인.

 `--save-dev` : 개발 환경에서만 사용되는 라이브러리에 옵션 사용.
<br>

 - exec  
  `npm install --save-dev webpack webpack-dev-server webpack-cli html-webpack-plugin`

## Hot Module Reload

개발시 소스가 저장될때 마다 자동으로 Reload해주는 기능
<br>

 - React Hot Loader 사용
  1. .babelrc에 해당 소스 추가
```
  {
    "plugins": ["react-hot-loader/babel"]
  }
```
  2. 루트 컴포넌트에 `react-hot-loader` 임포트.
```
  import { hot } from 'react-hot-loader/root';
  
  const App = () => <div>Hello World!</div>;
  export default hot(App);
```
  3. webpack.config.js 에 entry에 `react-hot-loader/patch` 추가
```
  module.exports = {
    entry: ['react-hot-loader/patch', '메인entry.js'],
  };
```
  ※ 리로딩 설정옵션 - 해당소스추가시 reload를 on/off할 수 있다.(미동작하는 것 같음)
  ```
  import { setConfig } from 'react-hot-loader';
  
  setConfig({
    reloadHooks: false,
  });
  ```

 - wepack Hmr사용시 - dev옵션에 hot 설정을 true 로변경
```
  module.exports = {
    devServer: {
      hot: true
    }
  }
```


<br>
<br>
<br>

## 웹팩, 바벨, package.json 초기설정

- package.json
```javascript
{
  "name": "react-meterial-web",
  "version": "1.0.0",
  "description": "meterial web example",
  "main": "index.js",
  "scripts": {
    "start": "webpack serve",
    "build": "webpack build",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/joy2734/react-meterial-web.git"
  },
  "author": "hjjoo",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/joy2734/react-meterial-web/issues"
  },
  "homepage": "https://github.com/joy2734/react-meterial-web#readme",
  "dependencies": {
    "@hot-loader/react-dom": "^17.0.1",
    "babel-cli": "^6.26.0",
    "babel-core": "^6.26.3",
    "babel-loader": "^7.0.0",
    "babel-polyfill": "^6.26.0",
    "babel-preset-env": "^1.7.0",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-react": "^6.24.1",
    "babel-preset-react-hmre": "^1.1.1",
    "babel-preset-stage-0": "^6.24.1",
    "css-loader": "^5.0.1",
    "expose-loader": "^2.0.0",
    "express": "^4.17.1",
    "file-loader": "^6.2.0",
    "html-webpack-plugin": "^4.4.0",
    "json-server": "^0.16.3",
    "node-sass": "^5.0.0",
    "react": "^17.0.1",
    "react-dom": "^17.0.1",
    "react-hot-loader": "^4.13.0",
    "sass-loader": "^10.1.1",
    "style-loader": "^2.0.0",
    "url-loader": "^4.1.1",
    "webpack-dev-middleware": "^4.1.0",
    "webpack-dev-server": "^3.11.0",
    "webpack-hot-middleware": "^2.25.0"
  },
  "devDependencies": {
    "@material-ui/core": "^4.11.3",
    "@material-ui/icons": "^4.11.2",
    "babel-register": "^6.26.0",
    "bootstrap": "^4.6.0",
    "chokidar": "^3.5.1",
    "react-bootstrap": "^1.4.3",
    "react-percent-bar": "^0.0.2",
    "react-redux": "^7.2.2",
    "react-router-dom": "^5.2.0",
    "redux": "^4.0.5",
    "redux-actions": "^2.6.5",
    "semantic-ui-css": "^2.4.1",
    "semantic-ui-react": "^2.0.3",
    "ts-loader": "^9.1.1",
    "underscore": "^1.12.1",
    "webpack": "^4.46.0",
    "webpack-cli": "^4.6.0",
    "webpack-node-externals": "^3.0.0"
  }
}
```
- webpack.config.js

```
var webpack = require('webpack');
var path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  mode: 'development',
  resolve:{
    alias:{
      'react-dom': '@hot-loader/react-dom'
    }
  },
  entry: [
    'react-hot-loader/patch',
    './src/index.js'
  ],
  output: {
    path: __dirname + '/dist',
    filename: 'main.js'
  },
  devServer: {
    hot: true,
    inline: true,
    port: 3000,
    publicPath: '/'
    //contentBase: __dirname + '/dist/'
  },
  module: {
        rules: [
        {
          test: /\.js$|\.jsx?$/,
          loaders: ['babel-loader'],
          include: path.join(__dirname, 'src')
        },
        {
          test: /\.less$/,
          loader: 'style-loader!css-loader!less-loader'  // use ! to chain loaders
        },
        {
          test: /\.css$/,
          loader: 'style-loader!css-loader'
        },
        {
          test: /\.scss$/,
          loader: 'style-loader!css-loader!sass-loader'
        },
        {
          test: /\.(png|jpg)$/,
          loader: 'url-loader?limit=8192' // inline base64 URLs for <=8k images, direct URLs for the rest
        },
        {
          test: /\.(ttf|eot|svg|woff|woff2)(\?v=[0-9]\.[0-9]\.[0-9])?$/,          
          loader: 'file-loader'
        },
        {
          test: require.resolve("underscore"),
          loader: "expose-loader",
          options: {
            exposes: {
              globalName: "_.filter",
              moduleLocalName: "filter",
            },
          },
        }
      ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      inject: 'body',
      template: path.resolve(__dirname, './src/index.html'),
      filename: path.resolve(__dirname, './dist/index.html')
    }),
    new webpack.HotModuleReplacementPlugin()
  ]
}
```
- .babelrc
```
{
    "presets":["env","react","es2015", "stage-0"],
    "env":{
       "development":{
          "presets":["react-hmre"]
       }
    },
    "plugins": ["react-hot-loader/babel"]
 }
```