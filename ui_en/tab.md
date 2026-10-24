# 标签布局

- 更新时间:2026-10-22 10:58:42

> 标签布局-tab
> 
> 原生类型:{com.google.android.material.tabs.TabLayout}




## 一、常用属性


### item - 选项标签

> 选项标签
> 
> icon/图标：用于指定图标，可以填写图标库的名称，也可以填写图标的相对路径或者绝对路径


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <tab w="max">
        <item text="选项1" icon="ag_logo" iconTint="#FF0000" />
        <item text="选项2" icon="ag_logo" iconTint="#00FF00" />
    </tab>
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
    <!--padding顺序是:左,上,右,下-->
    <!--padding只设置一个值：则设置所有方向的内边距-->
    <!--padding只设置两个值：则设置左右和上下方向的内边距-->
    <tab padding="20" />
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
    <tab bg="#1E1F22" />
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
    <tab bgImg="./img.png" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


