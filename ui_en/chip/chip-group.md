# 小片组

- 更新时间:2026-10-22 10:58:40

> 小片组-chip-group
> 
> 是布局父类的(XLayout)的子类
> 
> 原生类型:{com.google.android.material.chip.ChipGroup}




## 一、常用属性


### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <chip-group bg="#FF0000" />
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
    <chip-group bgImg="res/t01.png" />
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
    <chip-group padding="0,0,0,0" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


### check(text)

> 按“文字内容”选中小片组里的某个小片。
> 
> 在 XML 里 chip-group 下面会放好几个 chip。这个方法传一段文字，
> 就会把组里“文字正好等于这段文字”的那个小片选中；如果有多个小片文字相同，会全部选中。
> 前提是这些小片本身是可选中的（checkable="true"）。

- 参数 : text {String} 要选中的小片上显示的文字


```javascript
//先用一段 XML 创建界面：一个小片组里放三个可选中的小片
var ui = $ui.layout('<ui><statusbar/><chip-group id="g1"><chip text="选项1" checkable="true"/><chip text="选项2" checkable="true"/></chip-group></ui>');
ui.show(); //把界面显示出来
var g = ui.id("g1"); //根据 id 拿到这个小片组
g.check("选项1"); //自动把文字是“选项1”的那个小片勾上
```


### inverse(text)

> 按文字选中匹配的小片，并取消其他小片的选中状态。
> 
> 虽然方法名叫“反选”，实际行为不是把所有小片的选中状态逐个取反。
> 输入 CharSequence 文本，脚本通常传字符串；使用完整文字匹配，不是只匹配其中一部分。
> 传 null 时会记录提示并直接结束。请先把小片设置为可选中，否则无法正常演示选中效果。
> 返回类型为 void，没有返回值。操作在界面线程中执行，最终状态也受小片组的选择规则限制。

- 参数 : text {CharSequence} 需要匹配的小片完整文字；传 null 时不修改状态。


```javascript
// 创建两个可以选中的小片，并给小片组取一个查找用的名字。
var ui = $ui.layout("<ui><statusbar /><chip-group id=\"options\"><chip text=\"Option 1\" checkable=\"true\" /><chip text=\"Option 2\" checkable=\"true\" /></chip-group></ui>");
var group = ui.id("options");
// 选中第二项，同时取消其他项的选中状态。
group.inverse("Option 2");
ui.show();
```


### check(index)

> 按“下标位置”选中小片组里的某个小片。
> 
> 下标从 0 开始数：第 1 个小片是 0，第 2 个是 1，依次类推。

- 参数 : index {Number} 下标，从 0 开始


```javascript
//先用一段 XML 创建界面：一个小片组里放两个可选中的小片
var ui = $ui.layout('<ui><statusbar/><chip-group id="g1"><chip text="选项1" checkable="true"/><chip text="选项2" checkable="true"/></chip-group></ui>');
ui.show(); //把界面显示出来
var g = ui.id("g1"); //根据 id 拿到这个小片组
g.check(0); //选中小片组里第 1 个小片（下标 0）
```


### childCount()

> 数一下这个小片组里一共有多少个小片。
> 
> 返回一个整数。

- 返回 : {int} 小片组里小片的个数


```javascript
//先用一段 XML 创建界面：一个小片组里放两个小片
var ui = $ui.layout('<ui><statusbar/><chip-group id="g1"><chip text="A"/><chip text="B"/></chip-group></ui>');
ui.show(); //把界面显示出来
var g = ui.id("g1"); //根据 id 拿到这个小片组
var count = g.childCount(); //数一下有几个
ui.toast("一共 " + count + " 个小片"); //弹出 2
```


### getChild(index)

> 按下标拿到组里某个小片的“安卓原生 Chip 对象”。
> 
> 下标从 0 开始。注意：返回的是安卓原生的 Chip 对象，不是本应用封装的 XChip；
> 对它做修改时要放在界面线程里，一般小白用不到，了解即可。
> 下标超出范围时返回 null。

- 参数 : index {Number} 下标，从 0 开始
- 返回 : {Chip} 对应的安卓原生小片对象；越界时返回 null


```javascript
//先用一段 XML 创建界面：一个小片组里放两个小片
var ui = $ui.layout('<ui><statusbar/><chip-group id="g1"><chip text="A"/><chip text="B"/></chip-group></ui>');
ui.show(); //把界面显示出来
var g = ui.id("g1"); //根据 id 拿到这个小片组
var chip = g.getChild(0); //拿到第 1 个小片的原生对象
if (chip != null) { //判断一下是否拿到
    ui.toast("第1个小片的文字是：" + chip.getText());
}
```


