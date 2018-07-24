#flex兼容

Q:大佬们解决过手机flex兼容性问题吗？有没有比较好的写法?
A:用autoprefixer插件，配置属性 browsers: ['> 1%', 'last 5 versions', 'Firefox >= 20', 'iOS >=7', 'android >=4', 'safari>=5'] ，如下：
```
var autoprefixer = require('autoprefixer');
autoprefixer({
    browsers: ['> 1%', 'last 5 versions', 'Firefox >= 20', 'iOS >=7', 'android >=4', 'safari>=5']
})

```

然后 flex-box 的子元素尽量别用 默认display为 inline 的元素的应该就没什么坑了
用且只用 display: flex flex: 1 justify-content align-items