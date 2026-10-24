# 状态栏

- 更新时间:2026-10-22 10:58:42

> 状态栏-statusbar
> 
> 本质上就是一个{MaterialTextView},只不过高度为状态条的高度,此控主要用来占位置,避免手机状态条挡住主要的布局
> 
> 原生类型:{com.google.android.material.textview.MaterialTextView}





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116230690182616&bvid=BV1hLwKzWEMX&cid=36706716488&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

状态栏：一般手机界面的最上方的部分就是状态栏。


![](./img/statusbar_example.png)

## 一、常用属性


### color - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" dir="v" gravity="center" h="max">
        <statusbar color="#518855" />
        <statusbar color="#B44A4A" />
        <statusbar color="#3574F0" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/822704913786800.png)

### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar bg="#518855" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/823019796005800.png)

### bgImg - 背景图片

> 设置背景图片


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
// 若布局引用图片、视频或其他资源，请先准备文件并改成实际可用的路径。
var layoutXml = `
<ui>
    <statusbar />
    <statusbar bgImg="./img.png"/>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/822979123418600.png)

## 二、常用函数


### setColor(color)

> 设置颜色

- 参数 : color {string} 状态条颜色


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var bar = ui.id("mBar");
//设置颜色
bar.setColor("#1E1F22");
```


