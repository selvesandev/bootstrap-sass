# Bootstrap Sass Template

`npm install bootstrap@4.0.0-beta.2 --save`  
`npm install --save jquery`  
`npm install --save-dev css-loader node-sass extract-text-webpack-plugin sass-loader style-loader webpack`

[free photos](https://www.pexels.com/)

### Directory Structure.
```
//Main File.
/src/sass/app.scss
/src/js/main.js

```

### Live Server
`npm install -g live-server` go to your folder and write `live-server --port=8000` to browser the project. Will automatically reload the browser.



### Generate SourceMap

```
var webpack = require('webpack');
var path = require('path');
var ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
    entry: ['./src/js/app.js', './src/sass/app.scss'],
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js'
    },
    devtool: "source-map",
    module: {
        rules: [
            { // regular css files
                test: /\.css$/,
                use: ['style-loader', 'css-loader']
            },
            { // sass / scss loader for webpack
                test: /\.(sass|scss)$/,
                use: ExtractTextPlugin.extract({
                    use: [{
                        loader: "css-loader", options: {
                            sourceMap: true
                        }
                    }, {
                        loader: "sass-loader", options: {
                            sourceMap: true
                        }
                    }],
                    fallback: 'style-loader'
                })
            }
        ]
    },
    plugins: [
        new ExtractTextPlugin('style.css')
    ]
};
```



### Using font-awesome.
`npm install --save font-awesome`  
`npm install --save-dev file-loader`
**main.scss**
```
$fa-font-path: "~font-awesome/fonts";
@import "~font-awesome/scss/font-awesome";
```

**webpack.config.js**
```
{
    test: /.(ttf|otf|eot|svg|woff(2)?)(\?[a-z0-9]+)?$/,
        use: [{
            loader: 'file-loader',
            options: {
                name: '[name].[ext]',
                outputPath: 'fonts/',    // where the fonts will go
                publicPath: './'       // override the default path
            }
        }]
    }
```
