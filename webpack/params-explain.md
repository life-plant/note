#参数配置说明

##mode
###作用：
    用于配置构建出来的代码的状态，是否是压缩过的等等。
###参数 
- development 开发环境
- production 生产 默认是这个
- none
###配置环境：
    "build": "webpack --mode development"

##loader
###babel-loader
####作用
    用于配置配置es6环境
####依赖：
    "devDependencies": {
        "babel-cli": "^6.26.0",
        "babel-core": "^6.26.3",
        "babel-loader": "^7.1.4",
        "babel-preset-env": "^1.7.0",
      }
####babel配置环境