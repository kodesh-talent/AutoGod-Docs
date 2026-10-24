# 折叠布局

- 更新时间:2026-10-22 10:58:39

> 可展开或收起子内容的布局。常用作折叠面板；可用 open、close 和 change 控制展开状态。




## 一、常用属性


### dir - 折叠方向

> 设置折叠方向


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand dir="v" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### dur - 折叠动画时长

> 设置折叠动画时长


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand dur="500" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### exp - 默认展开状态

> 设置默认展开状态


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand exp="true" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### minW - 最小宽度

> 设置最小宽度


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand minW="100" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### minH - 最小高度

> 设置最小高度


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand minH="100" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bg - 背景颜色

> 设置背景颜色


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand bg="red" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bgImg - 背景图片

> 设置背景图片


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 示例引用的图片或子布局文件需要先放到项目中，并按实际位置修改路径。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <expand bgImg="res/bg.png" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、常用函数


### setDur(dur)

> 设置动画时长

- 参数 : dur {Number} 动画时长


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//找到折叠布局
var exp = ui.id("mExp");
//设置动画时长
exp.setDur(500);
```


### setDir(dir)

> 设置折叠方向
> 
> 默认是竖向折叠

- 参数 : dir {String} 折叠方向(可选:h、v)


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//找到折叠布局
var exp = ui.id("mExp");
//设置折叠方向
exp.setDir("h");
```


### setBg(color)

> 设置背景颜色

- 参数 : color {String} 背景颜色


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//找到折叠布局
var exp = ui.id("mExp");
//设置背景颜色
exp.setBg("#549159");
```


### open()

> 打开折叠面板


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//找到折叠布局
var exp = ui.id("mExp");
//打开折叠面板
exp.open();
```


### close()

> 关闭折叠面板


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//找到折叠布局
var exp = ui.id("mExp");
//关闭折叠面板
exp.close();
```


### change()

> 切换折叠面板状态
> 
> 如果面板处于关闭状态，那么调用此函数就会打开，反之：如果面板处于打开状态，那么调用此函数就会关闭面板。


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//找到折叠布局
var exp = ui.id("mExp");
//切换折叠面板状态
exp.change();
```


## 子控件属性表

被折叠布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |


