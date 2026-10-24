# 日志

- 更新时间:2026-10-22 10:58:41

> 日志-log





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116225237653567&bvid=BV1Qmwsz5Eqq&cid=36684169437&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

日志组件：显示日志信息


![](./img/1033925169795800.png)

## 一、常用属性


### padding - 内边距

> 设置内边距


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <log w="max" h="max" padding="50" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/1034016914246900.png)

### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <log bg="#FF0000" />
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
    <log bgImg="res/t01.png" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、常用函数


### setTextSize(size)

> 设置日志显示文字的字号大小，单位 sp。

- 参数 : size {Float} 字体大小，单位 sp
- 版本 : 1.7.3


```javascript
//先用一段 XML 创建界面，里面放一个占满全屏的日志面板
var ui = $ui.layout('<ui><statusbar/><log id="mLog" w="max" h="max"/></ui>');
ui.show(); //把界面显示出来
var log = ui.id("mLog"); //根据 id 拿到这个日志面板
log.setTextSize(12); //把日志字号设成 12sp
```


### setBgColor(color)

> 设置日志面板的背景颜色（用安卓颜色整数表示）。
> 
> 通常配合 $color 预置颜色使用，例如 $color.BLACK。

- 参数 : color {int} 安卓颜色整数，常用 $color.BLACK 等预置颜色
- 版本 : 1.7.3


```javascript
//先用一段 XML 创建界面，里面放一个日志面板
var ui = $ui.layout('<ui><statusbar/><log id="mLog" w="max" h="max"/></ui>');
ui.show(); //把界面显示出来
var log = ui.id("mLog"); //根据 id 拿到这个日志面板
log.setBgColor($color.BLACK); //把背景涂成黑色
```


### setBgColor(color)

> 设置日志面板的背景颜色（用颜色字符串表示）。

- 参数 : color {String} 颜色字符串，例如 "#FF0000"
- 版本 : 1.7.3


```javascript
//先用一段 XML 创建界面，里面放一个日志面板
var ui = $ui.layout('<ui><statusbar/><log id="mLog" w="max" h="max"/></ui>');
ui.show(); //把界面显示出来
var log = ui.id("mLog"); //根据 id 拿到这个日志面板
log.setBgColor("#111111"); //把背景涂成深灰
```


### getContent()

> 把日志面板里目前显示的全部文字读出来。

- 返回 : {String} 面板里目前的全部日志文字
- 版本 : 1.7.3


```javascript
//先用一段 XML 创建界面，里面放一个日志面板
var ui = $ui.layout('<ui><statusbar/><log id="mLog" w="max" h="max"/></ui>');
ui.show(); //把界面显示出来
var log = ui.id("mLog"); //根据 id 拿到这个日志面板
var all = log.getContent(); //读出全部日志文字
log(all); //用日志功能再打印一遍
```


### scrollBottom()

> 让日志面板自动滚动到最底部（看最新一条日志）。

- 版本 : 1.7.3


```javascript
//先用一段 XML 创建界面，里面放一个日志面板
var ui = $ui.layout('<ui><statusbar/><log id="mLog" w="max" h="max"/></ui>');
ui.show(); //把界面显示出来
var log = ui.id("mLog"); //根据 id 拿到这个日志面板
//打印很多条日志后，自动滚到底部看最新的
log.scrollBottom();
```


### clear()

> 把这个日志面板里已经显示的内容全部清空。

- 版本 : 1.7.3


```javascript
//先用一段 XML 创建界面，里面放一个日志面板
var ui = $ui.layout('<ui><statusbar/><log id="mLog" w="max" h="max"/></ui>');
ui.show(); //把界面显示出来
var log = ui.id("mLog"); //根据 id 拿到这个日志面板
//清空这个面板上的内容
log.clear();
//如果想连悬浮窗日志也一起清空，更简单的做法是：
//$log.delete();
```


