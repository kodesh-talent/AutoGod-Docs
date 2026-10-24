# 视频

- 更新时间:2026-10-22 10:58:42

> 视频-video





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116242518253236&bvid=BV1y8wQzrEsi&cid=36756915385&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

用来展示视频的控件


## 一、常用属性


### path - 视频路径

> 设置视频路径


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
// 若布局引用图片、视频或其他资源，请先准备文件并改成实际可用的路径。
var layoutXml = `
<ui>
    <statusbar />
    <video path="res/video.mp4" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### url - 视频链接

> 设置视频链接


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <video url="http://www.a.a/video.mp4" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### loop - 是否循环播放视频

> 是否循环播放视频


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <video loop="true" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### autoStart - 是否自动播放视频

> 是否自动播放视频


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <video autoStart="true" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### padding - 内边距

> 设置内边距


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <video padding="0,0,0,0" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <video bg="red" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bgImg - 背景图片

> 设置背景图片


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
// 若布局引用图片、视频或其他资源，请先准备文件并改成实际可用的路径。
var layoutXml = `
<ui>
    <statusbar />
    <video bgImg="res/bg.png" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、常用函数


### onComplete(callback)

> 监听视频“整个播完”这一刻，回调你传进来的函数。

- 参数 : callback {function} 播完回调，参数是内部播放器对象


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.onComplete(function(mp) {
    log("视频播完了");
});
```


### onPrepare(callback)

> 监听视频“加载好、可以开始播”这一刻，回调你传进来的函数。

- 参数 : callback {function} 准备好回调，参数是内部播放器对象


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.onPrepare(function(mp) {
    log("视频准备好了，可以开始");
});
```


### onError(callback)

> 监听视频播放出错（比如文件损坏、网络视频加载失败），回调告诉你出错了。

- 参数 : callback {function} 错误回调，参数是播放器对象、错误类型码、额外码；返回 true 表示已处理


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" url="https://example.com/v.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.onError(function(mp, what, extra) {
    log("播放出错了,错误码:" + what);
    return true; //表示错误已处理
});
```


### onInfo(callback)

> 监听视频播放过程中的提示信息（比如开始缓冲、缓冲结束）。

- 参数 : callback {function} 信息回调，参数是播放器对象、事件码、额外码；返回 true 表示已处理


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" url="https://example.com/v.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.onInfo(function(mp, what, extra) {
    log("播放提示,类型:" + what);
    return false;
});
```


### path(path)

> 代码里指定要播放哪个本地视频文件（手机上的绝对路径，或项目里可读的资源路径）。

- 参数 : path {String} 本地视频文件路径或项目资源路径


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.path("res/video.mp4"); //换成这个视频文件
```


### uri(uri)

> 代码里指定要播放哪个视频地址（可以是网络网址，也可以是本地文件地址）。

- 参数 : uri {String} 视频地址，可以是网络网址或本地文件地址


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.uri("https://example.com/video.mp4"); //播放这个网络视频
```


### start()

> 开始播放视频（或从暂停处继续播）。


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.start(); //开始播放
```


### pause()

> 暂停播放视频（再调 start 会从暂停处接着播）。


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.start(); //先开始
video.pause(); //再暂停
```


### stop()

> 停止播放并释放播放器资源。注意：停掉后要再播，必须重新 path 或 uri 指定视频源。


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.stop(); //停止并释放
```


### resume()

> 恢复被挂起（suspend）的播放器资源。普通暂停后继续播用 start 即可。


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.resume(); //恢复播放器
```


### suspend()

> 挂起播放器并释放媒体资源，省内存。要再用就调 resume 恢复。


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.suspend(); //挂起
```


### keepScreen(keep)

> 播放时保持屏幕常亮，不让它自动锁屏变暗。true 常亮，false 恢复正常。

- 参数 : keep {boolean} true 保持屏幕常亮，false 恢复


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.keepScreen(true); //看视频时屏幕不灭
```


### seekTo(ms)

> 把播放进度跳到指定的时间点（单位是毫秒，30000 就是第 30 秒）。

- 参数 : ms {number} 要跳到的位置，单位毫秒


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
video.seekTo(30000); //跳到第 30 秒
```


### isPlaying()

> 读出视频现在是不是正在播放。返回 true 表示正在播。

- 返回 : {boolean} true 表示正在播放


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
if (video.isPlaying()) {
    log("正在播放");
}
```


### getDur()

> 读出这个视频一共有多长（总时长，单位毫秒）。还没加载好时可能返回 -1。

- 返回 : {number} 视频总时长（毫秒）；未知时返回 -1


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
var dur = video.getDur(); //读总时长
log("总时长毫秒:" + dur);
```


### getCur()

> 读出现在播到第几毫秒了（当前播放位置）。

- 返回 : {number} 当前播放位置（毫秒）


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
var pos = video.getCur(); //读当前位置
log("当前播到:" + pos + "毫秒");
```


### canPause()

> 读出这个视频现在能不能暂停。

- 返回 : {boolean} true 表示可以暂停


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
if (video.canPause()) {
    log("可以暂停");
}
```


### canSeekBackward()

> 读出这个视频能不能往回退（往前倒带）。

- 返回 : {boolean} true 表示可以往回退


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
if (video.canSeekBackward()) {
    log("可以往回退");
}
```


### canSeekForward()

> 读出这个视频能不能往前快进。

- 返回 : {boolean} true 表示可以往前快进


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" path="res/video.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
if (video.canSeekForward()) {
    log("可以往前快进");
}
```


### getBufferPercentage()

> 读出网络视频已经缓冲（提前下载好）了百分之几，0 到 100。

- 返回 : {number} 已缓冲百分比，0 到 100


```javascript
var ui = $ui.layout('<ui><statusbar/><video id="mVideo" w="max" url="https://example.com/v.mp4"/></ui>');
ui.show(); //把界面显示出来
var video = ui.id("mVideo"); //根据 id 拿到这个视频控件
var p = video.getBufferPercentage(); //读缓冲百分比
log("已缓冲:" + p + "%");
```


