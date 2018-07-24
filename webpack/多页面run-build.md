
#多页面的npm run build的配置

这个配置基于
./npm-run-build-dev文件里的配置
##项目目录
app:.
|   index.html
|   index.js
|   index2.html
|   index2.js
|   tree.txt
|   vendor.js
|   
+---dist
|   |   index.html
|   |   index2.html
|   |   page1.css
|   |   page2.css
|   |   
|   +---js
|   |   +---page1
|   |   |       51fb00c9.bundle.js
|   |   |       
|   |   \---page2
|   |           0584ec63.bundle.js
|   |           
|   \---src
|       \---assets
|               pic-frame.png
|               wxshare.jpg
|               
\---src
    +---assets
    |       pic-frame.png
    |       wxshare.jpg
    |       
    +---css
    |       page1.css
    |       page2.css
    |       
    \---js
            page1.js
            page2.js
            

##entry 配置变化
```
    entry: {
        page1:["babel-polyfill", "./app/index"],
        page2:["babel-polyfill", "./app/index2"],
    },
```
这里entry里面page1和page2就是定义的chunks


##output配置变化
```
    output: {
        path: path.resolve(__dirname,"app/dist"),
        publicPath: "",
        filename: 'js/[name]/[chunkhash:8].bundle.js', 
            //这里[name][chunkhash]是对应变量，[name]指page1和page2，
    },
```

##HtmlWebpackPlugin的变化
```
    plugins:[
        new HtmlWebpackPlugin({
            template: path.resolve(__dirname, './app/index.html'),
            filename:'index.html',
            chunks:['page1']
        }),
        new HtmlWebpackPlugin({
            template: path.resolve(__dirname, './app/index2.html'),
            filename:'index2.html',
            chunks:['page2']
        })
    ]
```
