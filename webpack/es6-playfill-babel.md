#配置es6、es7环境

##作用
    用于配置配置es6或es7环境,对于IE8或者其他的一些浏览器进行es6->es5的转化
###依赖：
```    "devDependencies": {
        "babel-cli": "^6.26.0",
        "babel-core": "^6.26.3",
        "babel-loader": "^7.1.4",
        "babel-preset-env": "^1.7.0",
    }```

##babel配置环境
###.babelrc
```    {
      "presets": ["env"]
    }```
###preset解释
babel-preset-env behaves exactly the same as babel-preset-latest (or babel-preset-es2015, babel-preset-es2016, and babel-preset-es2017 together).
babel-preset-env 可以将最新一版的es转化成可执行的js文件。

##webpack-config.js对babel的配置
```    module: {
      rules: [
        { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
      ]
    }```

##加入babel-ployfill
在前面的基础上加入。
###package.js
```    "dependencies": {
        "babel-polyfill": "^6.26.0",
    }```

###webpack-config.js(上面的过程不会自动引入）
```    entry: ["babel-polyfill", "./app/index"],//或者在入口import "babel-polyfill"
```

##在eslint中配置es6环境
```
{
    "parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true
        }
    },
}
```

