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


### onChange(callback)

> 监听用户拖动拖动条：手指一动就回调，并告诉你当前数值。
> 
> 注意：只监听用户手动拖出来的变化，代码里 setValue 不会触发。传 null 可取消监听。

- 参数 : callback {function} 变化回调，参数是当前数值；传 null 取消监听


```javascript
//先用一段 XML 创建界面：一个拖动条，范围 0 到 100
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
//监听拖动
seek.onChange(function(value) {
    log("当前值:" + value);
});
```


### onTouchStart(callback)

> 监听用户“刚用手指按住拖动条”这一刻，立刻回调你传进来的函数（没有参数）。
> 
> 传 null 可取消监听。

- 参数 : callback {function} 手指按下时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.onTouchStart(function() {
    log("开始拖了");
});
```


### onTouchStop(callback)

> 监听用户“手指离开拖动条”这一刻，立刻回调你传进来的函数（没有参数）。
> 
> 传 null 可取消监听。

- 参数 : callback {function} 手指松开时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.onTouchStop(function() {
    log("松手了");
});
```


### getMin()

> 读出拖动条允许的最小值（最左边是几）。
> 
> 安卓 8.0 以上才返回真正的最小值；旧系统返回当前进度。

- 返回 : {number} 最小值


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
var minVal = seek.getMin(); //读最小值
log("最小是" + minVal);
```


### getMax()

> 读出拖动条允许的最大值（最右边是几）。

- 返回 : {number} 最大值


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
var maxVal = seek.getMax(); //读最大值
log("最大是" + maxVal);
```


### setValue(value)

> 代码里直接把滑块跳到某个数值。
> 
> 数值必须在最小和最大值之间，否则不生效。

- 参数 : value {Number} 要设的数值


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.setValue(50); //滑块跳到 50
```


### getValue()

> 读出滑块当前停在多少。

- 返回 : {number} 当前数值


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.setValue(50);
var value = seek.getValue(); //读出来
log("当前是" + value);
```


### setFrom(value)

> 代码里设置拖动条允许的最小值（最左边是几）。安卓 8.0 及以上才生效。

- 参数 : value {Number} 最小值，会转成整数
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.setFrom(10); //最左边变成 10
```


### setTo(value)

> 代码里设置拖动条允许的最大值（最右边是几）。

- 参数 : value {Number} 最大值，会转成整数
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><seek id="mSeek" w="max" from="0" to="100"/></ui>');
ui.show(); //把界面显示出来
var seek = ui.id("mSeek"); //根据 id 拿到这个拖动条
seek.setTo(200); //最右边变成 200
```


