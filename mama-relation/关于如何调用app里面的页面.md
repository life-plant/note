# 调用app页面的内容
调用app里面的页面，主要是需要跟客户端做对接，前端只需要在a标签填入相对应的链接，即所谓的协议

#但在这里分几种情况
1. 从app外调用app的原生页面
2. 从app外调用app的非原生页面（wap用html写的，一般有《返回》两个字的页面都是）
3. 从app内调用app的原生页面
4. 从app内调用app的非原生页面

#从外部打开app
http://wiki.corp.mama.cn/pages/viewpage.action?pageId=73893454


http://wiki.corp.mama.cn/pages/viewpage.action?pageId=77435786


http://wiki.corp.mama.cn/pages/viewpage.action?pageId=78190965

#从内部打开
http://wiki.corp.mama.cn/pages/viewpage.action?pageId=66257111
http://wiki.corp.mama.cn/pages/viewpage.action?pageId=79004248
内部wap页面是用内部浏览器打开的，我们使用spy-debugger去调试，手机打开app的wap页面，console页面用location.href='href';将页面导航到你要调试的页面。
