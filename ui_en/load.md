# 加载

- 更新时间:2026-10-22 10:58:41

> 加载器-load





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116225036262735&bvid=BV1erwszEE1r&cid=36683251823&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

加载器一般配合帧布局使用，显示在其他组件的上方。


![](./img/load_desc.png)

## 一、基础使用

需要手动的显示和隐藏，例如我下面的操作，点击按钮后：会显示正在加载中，完成加载任务后，手动隐藏这个控件。


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear gravity="center" w="max">
        <!--
        最开始的时候先隐藏这个加载器
        当点击按钮的时候再显示这个加载器
        -->
        <load id="mLoad" show="false" />
        <!--点击按钮时显示加载器-->
        <button id="mButton" text="开始加载" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```

```javascript
var ui = $ui.layout("main.xml");
//获取控件
var mLoad = ui.id("mLoad");
var mButton = ui.id("mButton");
//绑定点击事件
mButton.click(function() {
    //显示加载器
    mLoad.show();
    //加载中
    sleep(3000);
    //加载完毕：隐藏加载器
    mLoad.hide();
    toast("加载完毕");
});
```


## 二、常用属性


### color - 主题颜色

> 设置主题颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear dir="h" w="max">
        <load color="#57965C" marginEnd="15" />
        <load color="#3574F0" marginEnd="15" />
        <load color="#C94F4F" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/load_color.png)

### colors - 主题颜色组

> 设置主题颜色组


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <load colors="#57965C,#3574F0,#C94F4F,#FFC31F,#F501F5" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/load_colors.png)

### size - 尺寸

> 设置尺寸


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear dir="h" w="max">
        <load marginEnd="15" size="20" />
        <load marginEnd="15" size="25" />
        <load size="30" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/load_size.png)

### show - 显示状态

> 设置显示状态


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear dir="h" w="max">
        <load color="#57965C" marginEnd="15" show="true" />
        <!--第二个加载器被隐藏了，所以实际上只能看到两个加载器-->
        <load color="#3574F0" marginEnd="15" show="false" />
        <load color="#C94F4F" />
    </linear>
    <text gravity="center" h="50" selectable="true"
        text="第二个(蓝色的)加载器被隐藏了，所以实际上只能看到两个加载器" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/load_show.png)

## 三、常用函数


### setColor(color)

> 设置那个转圈小圆圈的颜色（用颜色字符串表示）。

- 参数 : color {String} 颜色字符串，例如 "#FF0000"


```javascript
//先用一段 XML 创建界面，里面放一个带 id 的加载圈
var ui = $ui.layout('<ui><statusbar/><load id="mLoad"/></ui>');
ui.show(); //把界面显示出来
var load = ui.id("mLoad"); //根据 id 拿到这个加载圈
load.setColor("#C94F4F"); //把转圈涂成红色
```


### setSize(size)

> 设置转圈小圆圈的大小，单位 dp。

- 参数 : size {Number} 圆圈大小，单位 dp


```javascript
//先用一段 XML 创建界面，里面放一个带 id 的加载圈
var ui = $ui.layout('<ui><statusbar/><load id="mLoad"/></ui>');
ui.show(); //把界面显示出来
var load = ui.id("mLoad"); //根据 id 拿到这个加载圈
load.setSize(40); //放大到 40dp
```


### show()

> 让转圈加载圈显示出来（开始转圈动画）。


```javascript
//先用一段 XML 创建界面：一个加载圈（默认先藏起来）加一个按钮
var ui = $ui.layout('<ui><statusbar/><load id="mLoad" show="false"/><button id="btn" text="开始加载"/></ui>');
ui.show(); //把界面显示出来
var load = ui.id("mLoad"); //根据 id 拿到这个加载圈
ui.id("btn").click(function() {
    load.show(); //点按钮后显示转圈
    sleep(2000); //假装加载两秒
    load.hide(); //加载完隐藏
});
```


### hide()

> 把转圈加载圈隐藏掉（它就不占位置了）。


```javascript
//先用一段 XML 创建界面：一个加载圈加一个按钮
var ui = $ui.layout('<ui><statusbar/><load id="mLoad"/><button id="btn" text="加载完"/></ui>');
ui.show(); //把界面显示出来
var load = ui.id("mLoad"); //根据 id 拿到这个加载圈
ui.id("btn").click(function() {
    load.hide(); //点按钮后把转圈藏掉
});
```


