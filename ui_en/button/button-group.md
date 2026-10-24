# 按钮组

- 更新时间:2026-10-22 10:58:39

> 按钮组-button-group
> 
> 是布局父类的(XLayout)的子类
> 
> 原生类型:{com.google.android.material.button.MaterialButtonToggleGroup}




## 一、常用属性


### dir - 布局方向

> 设置布局方向
> 
> 可选参数:v(纵向),h(横向)


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <button-group dir="h">
        <button text="按钮1"/>
        <button text="按钮2"/>
    </button-group>
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
    <button-group bg="#FF0000">
        <button text="按钮1"/>
        <button text="按钮2"/>
    </button-group>
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
    <button-group bgImg="/res/t01.png">
        <button text="按钮1"/>
        <button text="按钮2"/>
    </button-group>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### singleSelect - 是否是单选模式

> 是否是单选模式


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <button-group singleSelect="false">
        <button text="按钮1"/>
        <button text="按钮2"/>
    </button-group>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### selectRequire - 是否至少选一个

> 是否至少选一个
> 
> 只在单选模式下有效


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <button-group selectRequire="false">
        <button text="按钮1"/>
        <button text="按钮2"/>
    </button-group>
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
    <button-group padding="0,0,0,0"/>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### gravity - 重力

> 设置重力
> 
> 可选值参考重力参数表


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <button-group gravity="center">
        <button text="按钮1"/>
        <button text="按钮2"/>
    </button-group>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### check(index)

> 选中按钮

- 参数 : index {int} 按钮下标


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获得控件
var bg = ui.get("mButtonGroup");
//选中按钮
bg.check(0);
```


### onCheck(callback)

> 监听选中按钮的下标

- 参数 : callback (function(index) {}) 回调


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获得控件
var bg = ui.id("mButtonGroup");
//监听选中按钮的下标
bg.onCheck(function(index) {
    $ui.toast(index);
});
```


