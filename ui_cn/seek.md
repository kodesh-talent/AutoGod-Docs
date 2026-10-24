# 拖动条

- 更新时间:2026-10-22 10:58:42

> 拖动条-seek
> 
> 该组件比slider更加小巧，属于安卓原生组件。
> 
> 原生类型:{android.widget.SeekBar}




## 一、常用属性


### from - 开始值

> 设置开始值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <seek from=\"0\" />\n" +
    "</ui>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### to - 结束值

> 设置结束值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <tab to=\"100\" />\n" +
    "</ui>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### value - 当前值

> 设置当前值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <tab value=\"30\" />\n" +
    "</ui>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### padding - 内边距

> 设置内边距


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <!--padding顺序是:左,上,右,下-->\n" +
    "    <!--padding只设置一个值：则设置所有方向的内边距-->\n" +
    "    <!--padding只设置两个值：则设置左右和上下方向的内边距-->\n" +
    "    <tab seek=\"20\" />\n" +
    "</ui>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <tab seek=\"#1E1F22\" />\n" +
    "</ui>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bgImg - 背景图片

> 设置背景图片


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <tab seek=\"./img.png\" />\n" +
    "</ui>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、常用函数


### 监听变化(回调)

> “监听变化”是 onChange 的中文名字：用户拖动时回调，并告诉你当前数值。

- 参数 : 回调 {function} 变化回调，参数是当前数值；传 null 取消监听
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.监听变化(function(value) {
    log("当前值:" + value);
});
```


### 监听触摸开始(回调)

> “监听触摸开始”是 onTouchStart 的中文名字：用户刚按住拖动条时回调。

- 参数 : 回调 {function} 手指按下时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.监听触摸开始(function() {
    log("开始拖了");
});
```


### 监听触摸结束(回调)

> “监听触摸结束”是 onTouchStop 的中文名字：用户松手时回调。

- 参数 : 回调 {function} 手指松开时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.监听触摸结束(function() {
    log("松手了");
});
```


### 获取最小值()

> “获取最小值”是 getMin 的中文名字：读出拖动条最左边允许到几。

- 返回 : {number} 最小值
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
var minVal = seek.获取最小值();
log("最小是" + minVal);
```


### 获取最大值()

> “获取最大值”是 getMax 的中文名字：读出拖动条最右边允许到几。

- 返回 : {number} 最大值
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
var maxVal = seek.获取最大值();
log("最大是" + maxVal);
```


### 设置值(数值)

> “设置值”是 setValue 的中文名字：代码里直接把滑块跳到某个数值。

- 参数 : 数值 {Number} 要设的数值
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.设置值(50); //滑块跳到 50
```


### 获取值()

> “获取值”是 getValue 的中文名字：读出滑块当前停在多少。

- 返回 : {number} 当前数值
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.setValue(50);
var value = seek.获取值();
log("当前是" + value);
```


### 设置开始值(开始值)

> “设置开始值”是 setFrom 的中文名字：代码里设拖动条最左边允许到几。安卓 8.0 及以上生效。

- 参数 : 开始值 {Number} 最小值，会转成整数
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.设置开始值(10); //最左边变成 10
```


### 设置结束值(结束值)

> “设置结束值”是 setTo 的中文名字：代码里设拖动条最右边允许到几。

- 参数 : 结束值 {Number} 最大值，会转成整数
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.设置结束值(200); //最右边变成 200
```


