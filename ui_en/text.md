# 文本

- 更新时间:2026-10-22 10:58:42

> 文本-text
> 
> 原生类型:{com.google.android.material.textview.MaterialTextView}




## 一、常用属性


### size - 文本尺寸

> 设置文本尺寸
> 
> 单位:dp


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text size="100" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### textSize - 文本尺寸

> 设置文本尺寸
> 
> 单位:dp


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text textSize="100" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### typeface - 文本字体

> 设置文本字体
> 
> 可选值:sans,serif,mono,default,bold,italic,boldItalic


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text typeface="bold" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### color - 文本颜色

> 设置文本颜色


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text color="#FF0000" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### textColor - 文本颜色

> 设置文本颜色


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text textColor="#FF0000" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### selectable - 是否可选则文本

> 设置是否可选则文本


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text selectable="true" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### singleLine - 是否单行显示

> 是否单行显示


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text singleLine="true" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### maxLines - 最大行数

> 设置最大行数


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text maxLines="3" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### minW - 最小宽度

> 设置最小宽度


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text minW="100" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### minH - 最小高度

> 设置最小高度


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text minH="100" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### padding - 内边距

> 设置内边距


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><!--padding顺序是:左,上,右,下-->
<!--padding只设置一个值：则设置所有方向的内边距-->
<!--padding只设置两个值：则设置左右和上下方向的内边距-->
<text padding="20" text="内边距" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### gravity - 重力

> 设置重力


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text gravity="start" h="100" margin="20" text="重力:start" w="max" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### bg - 背景颜色

> 设置背景颜色


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text bg="#1E1F22" text="背景颜色" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


### bgImg - 背景图片

> 设置背景图片


```html
// 用字符串保存布局；其中的属性就是本节演示的设置。
var layoutXml = `
<ui><statusbar/><text bgImg="./img.png" text="背景图片" /></ui>
`;
var ui = $ui.layout(layoutXml); // 解析布局并创建控件。
ui.show(); // 显示界面，观察属性效果。
```


## 二、常用函数


### setText(text)

> 设置文本

- 参数 : text {string} 文本内容


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//设置文本
text.setText("新的内容");
```


### setColor(color)

> 设置文本颜色

- 参数 : color {int} 文本颜色


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//设置文本颜色
text.setColor($color.RED);
```


### setColor(color)

> 设置文本颜色

- 参数 : color {string} 文本颜色


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//设置文本颜色
text.setColor("#1E1F22");
```


### setBg(color)

> 设置背景颜色

- 参数 : color {int} 颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//设置背景颜色
text.setBg($color.RED);
```


### setBg(color)

> 设置背景颜色

- 参数 : color {string} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//设置背景颜色
text.setBg("#1E1F22");
```


### setSize(size)

> 设置文本尺寸

- 参数 : size {float} 尺寸


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//设置文本尺寸
text.setSize(18);
```


### getText()

> 获取文本内容

- 返回 : {string} 文本内容


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var text = ui.id("mText");
//获取文本内容
var t = text.getText();
```


