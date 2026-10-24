# 应用条布局

- 更新时间:2026-10-22 10:58:39

> 应用条布局-appbar-layout
> 
> 是布局父类的(XLayout)的子类
> 
> 原生类型:{com.google.android.material.appbar.AppBarLayout}




## 一、常用属性


### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <appbar-layout bg="#FF0000">
    </appbar-layout>
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
    <appbar-layout bgImg="/res/t01.png">
    </appbar-layout>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### liftOnScroll - 是否启用滚动阴影

> 是否启用滚动阴影


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <appbar-layout liftOnScroll="false">
    </appbar-layout>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### padding - 内边距

> 设置内边距
> 
> 参数顺序:左,上,右,下(单位:dp)


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <appbar-layout padding="0,0,0,0">
    </appbar-layout>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### gravity - 重力

> 设置重力


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <appbar-layout gravity="center">
    </appbar-layout>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、常用函数


### setBg(color)

> 设置背景颜色

- 参数 : color {int} 颜色值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获得控件
var abl = ui.get("mAppBarLayout");
//设置背景颜色
abl.setBg($color.RED);
```


### setBg(color)

> 设置背景颜色

- 参数 : color {string} 颜色值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获得控件
var abl = ui.get("mAppBarLayout");
//设置背景颜色
abl.setBg("#000000");
```


## 子控件属性表

被应用条布局包裹的子控件可以使用如下属性:

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 滑动标识   | scrollFlags     | 设置视图的滑动行为标识，可取的值请参考下表 |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 权重       | weight          | 设置视图的权重，通过浮点值指定，用于分配剩余空间               |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过parseGravity获取对应的重力值           |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

## 滑动标识属性取值表

| 英文名 | 中文名 | 描述 |
| ------ | ------ | ----------------------- |
| scroll | 滑动 | 设置视图将随滚动事件一起滚动（基础滑动行为）。 |
| enterAlways | 进入时总是可见 | 设置向下滚动时视图立即显示（无论滚动位置如何）。 |
| snap | 滑动时总是可见 | 设置视图在滚动结束时自动吸附到最近的完全显示或完全隐藏状态。 |
| exitUntilCollapsed | 退出时总是可见 | 设置向上滚动时视图一直滚动直到折叠（通常配合最小高度使用）。 |
| enterAlwaysCollapsed | 折叠后进入时总是可见 | 设置向下滚动时，仅当视图折叠后才立即开始显示。 |


:::tip 注意
在代码中可以使用英文或中文作为值，且多个值可以通过 '|' 符号连接，例如：'scroll|enterAlways' 或 '滑动|进入时总是可见'。
:::


