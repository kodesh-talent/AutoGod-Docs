# 绝对布局

- 更新时间:2026-10-22 10:58:38

> 绝对布局-absolute
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.AbsoluteLayout}




## 一、常用属性


### bg - 背景颜色

> 设置背景颜色


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <absolute bg="#57965C" />
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
    <absolute bgImg="res/t01.png" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### padding - 内边距

> 设置内边距
> 
> 参数顺序:左,上,右,下(单位:dp)


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <absolute padding="0,0,0,0" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### gravity - 重力

> 设置重力
> 
> 绝对布局只能设置前景重力，并且要求安卓6.0+。


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <absolute gravity="center" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 子控件属性表

被绝对布局包裹的子控件可以使用如下属性：

| 中文名   | 英文名    | 描述                                                         |
|----------|-----------|--------------------------------------------------------------|
| 横轴     | x         | 设置视图在AbsoluteLayout中的横轴（X轴）位置                   |
| 纵轴     | y         | 设置视图在AbsoluteLayout中的纵轴（Y轴）位置                   |
| 解决方向 | resolveDir | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽       | w         | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高       | h         | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |


