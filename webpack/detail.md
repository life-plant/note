##注意细节
- entry js入口文件不执行除了import、require的js语句

- loader执行顺序
```
    module: {
      rules: [
        { test: /\.js$/, exclude: /node_modules/, use: ["babel-loader", "eslint-loader"]},//先执行eslint-loader
      ]
    }
```
