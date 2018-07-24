#关于写video的注意事项

##日常用的video

```
<video 
controls="controls" 
width="690" height="385" 
src="//qimg.mama.cn/act/cms/2018/06/dc42fa59fe08fd8df0a2c841ab2eef.mp4" 
poster='{%gen_url("$static/asset/img/video-bg.png")%}' 
allowfullscreen 
webkit-playsinline playsinline x5-playsinline x-webkit-airplay="allow">
</video>

```

###属性解释
- controls：是否启用对视频的控制（暂停、播放、进度等）
- width、height： 宽、高
- src：视频的路径
- poster： 视频背景图设置
- allowfullscreen：是否允许全屏显示
- webkit-playsinline playsinline x5-playsinline x-webkit-airplay="allow" ：不让弹出窗播放。


##微信中的video属性设置

```
<video id="videoID" src="video.mp4" poster="loadbg.jpg" preload="auto" x-webkit-airplay="true" x5-video-player-type="h5" x5-video-player-fullscreen="true" webkit-playsinline="true" playsinline="true"></video> 

<video
 id="videoID"
 src="video.mp4"
 poster="loadbg.jpg"　视频封面
 preload="auto"
 x-webkit-airplay="allow"
 x5-video-player-type="h5"　启用H5播放器,是wechat安卓版特性
 x5-video-player-fullscreen="true"　全屏设置，设置为 true 是防止横屏
 x5-video-orientation="portraint"　播放器支付的方向，landscape横屏，portraint竖屏，默认值为竖屏
 webkit-playsinline="true"　这个属性是ios 10中设置可以让视频在小窗内播放，也就是不是全屏播放
 playsinline="true"　IOS微信浏览器支持小窗内播放
 style="object-fit:fill">
</video>
```




###video属性解释：
preload="auto" ：属性规定在页面加载后载入视频。如果设置了 autoplay 属性，则忽略该属性。
一般参数可能的值：
· auto - 当页面加载后载入整个视频
· meta - 当页面加载后只载入元数据
· none - 当页面加载后不载入视频

muted：当设置该属性后，它规定视频的音频输出应该被静音 
JQ操作的用法：
$('#videoID')[0].muted = true;
$('#videoID')[0].muted = false;

controls="controls" ：属性规定浏览器应该为视频提供播放控件。

autoplay="autoplay"： 视频自动播放设置，但是有经验的人都应该知道，autoplay标签在手机上不兼容，APP中设置问题导致无法自动播放，无论安卓或IOS。需要模拟自动播放只能通过一些事件触发。

webkit-playsinline="true"：视频播放时局域播放，不脱离文档流 。但是这个属性比较特别， 需要嵌入网页的APP比如WeChat中UIwebview 的allowsInlineMediaPlayback = YES webview.allowsInlineMediaPlayback = YES，才能生效。换句话说，如果APP不设置，你页面中加了这标签也无效，这也就是为什么安卓手机WeChat 播放视频总是全屏，因为APP不支持playsinline，而ISO的WeChat却支持。
这里就要补充下，如果是想做全屏直播或者全屏H5体验的用户，ISO需要设置删除 webkit-playsinline 标签，因为你设置 false 是不支持的 ，安卓则不需要，因为默认全屏。但这时候全屏是有播放控件的，无论你有没有设置control。 做直播的可能用得着播放控件，但是全屏H5是不需要的，那么去除全屏播放时候的控件，需要以下设置：同层播放。

x5-video-player-type="h5"：启用同层H5播放器，就是在视频全屏的时候，div可以呈现在视频层上，也是WeChat安卓版特有的属性。同层播放别名也叫做沉浸式播放，播放的时候看似全屏，但是已经除去了control和微信的导航栏，只留下"X"和"<"两键。目前的同层播放器只在Android（包括微信）上生效，暂时不支持iOS。笔者想过为什么同层播放只对安卓开放，因为安卓不能像ISO一样局域播放，默认的全屏会使得一些界面操作被阻拦，如果是全屏H5还好，但是做直播的话，诸如弹幕那样的功能就无法实现了，所以这时候同层播放的概念就解决了这个问题。不过笔者在测试的过程中发现，不同版本的ISO和安卓效果略有不同。

x5-video-orientation：声明播放器支持的方向，可选值landscape 横屏,portraint竖屏。默认值portraint。无论是直播还是全屏H5一般都是竖屏播放，但是这个属性需要x5-video-player-type开启H5模式

x5-video-player-fullscreen="true"：全屏设置。ture和false的设置会导致布局上的不一样