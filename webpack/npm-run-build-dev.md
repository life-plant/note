#从头开始npm run build 和 npm run dev的构建

##构建后目录
pro-\---app-\---dist
    |       |   \---src
    |       |       \---assets
    |       \---src
    |           +---assets
    |           +---css
    |           \---js
    \---wbpack.config.js
    |
    \---package.js
    ...


##npm run build

###package.js 
```
  "scripts": {
    "build": "webpack --mode production --config webpack.config.js",
  },
```

###webpack.config.js  配置entry入口文件
```
    entry: ["babel-polyfill", "./app/index"], 
    //这里先打包babel-polyfill,然后再从index.js入口文件开始打包，其中入口文件路径是“入口文件" 相对于 "webpack.config.js" 的路径
```

###webpack.config.js 配置output打包后要放的位置
```
    output: {
        path: path.resolve(__dirname,"app/dist"), //webpack会将npm run build构建的文件打包到这里
        publicPath: "", 
        //在将打包的js以'<script>'的方式插入html中时，会在文件路径前添加这个路径，
        //如：localhost:9000/{publicPath}/{filename}
        filename: 'bundle.js'
        //打包后输出的js文件名
    },
```


###加入打包css、js
```
// webpack.config.js

    module: {
      rules: [
        { 
            test: /\.js$/,
            exclude: /node_modules/,
            use: ["babel-loader", "eslint-loader"]},
        { 
            test: /\.css$/,
            exclude: /node_modules/,
            use: ["style-loader", "css-loader"] 
        }
      ]
    }
```

###加入打包html
```
    //webpack.config.js

    plugins:[
        new HtmlWebpackPlugin({
            template: path.resolve(__dirname, './app/index.html'),//html入口文件
            filename:'index.html',//打包后的文件相对路径
        })
    ]
```


###加入打包图片
```
    //webpack.config.js
    module: {
      rules: [
        {
            test: /\.(html)$/,
                use: {
                loader: 'html-withimg-loader',//用于将html里的属性抽出来形成一个路径并用require引进来
            }
        },
        {
            test: /\.(png|jpg)$/,
            loader: 'url-loader',
            options: {
                limit: 100, //小于100bytes的图片无法打包显示，而且data-url并不兼容所有浏览器
                mimetype: 'image/png',
                name: 'src/assets/[name].[ext]'//打包的图片放在这个路径
            }
　　　　}
      ]
    },

    plugins:[
        new HtmlWebpackPlugin({
            template: 'html-withimg-loader!' + path.resolve(__dirname, './app/index.html'),
            //html入口文件
            filename:'index.html',//打包后的文件相对路径
        })
    ]


    //html
    <div><img src='./src/assets/wxshare.jpg'></div>
        //这里src和data-src是相对html的图片的路径
```
###抽离css
注意 extract-text-webpack-plugin 3还不能支持webpack4.0.0以上的版本，需要升级
npm install --save-dev extract-text-webpack-plugin@next 
1.将处理css的loader改成这样，他会将其打包进对应的html中
```
    module: {
      rules: [
        { 
            test: /\.css$/,
            exclude: /node_modules/,
            use: ExtractTextPlugin.extract({
              fallback: "style-loader",
              use: "css-loader"
            }),
        }
    }
```

```
plugins:[
        new ExtractTextPlugin("[name].css"),
```

##npm run dev

###package.js 
```
    "dev": "webpack-dev-server --inline"
```
###devServer配置
```
    devServer: {
        contentBase: path.join(__dirname, 'app'), //应填index.html的入口位置
        compress: true,
        port: 9000
    },
```

###结果：
```
Project is running at http://localhost:9000/
webpack output is served from /
            // 由output.publicPath决定
Content not from webpack is served from D:\document\pratice-project\webpack-learn\app 
            // 由contentBase决定
```


##注意：
contentBase的路径跟publicPath的路径很重要，否则会有各种图片不正确的问题
