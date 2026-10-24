# 布局父类

- 更新时间:2026-10-22 10:58:43

> 布局父类-XLayout
> 
> 布局父类{XLayout}是属于{XView}的子控件，因此{XView}中的所有方法，布局父类都可以调用。
> 
> 所有布局控件都继承{XLayout}类，一因此可以调用{XLayout}中的方法。
> 
> 为了清晰的了解本软件的UI界面框架结构，我给你画个图:XView->XLayout->XScroll、XLinear、XCard等等
> 
> 这是什么意思呢？例如:XScroll是<scroll>标签、XLinear是<linear>标签、XCard是<card>标签等等我就不一一例举了，这些标签都是XLayout布局类的子类，也就是说这些对象都可以调用XLayout中的方法，而XLayout又是XView的子类，因此也可以调用XView中的所有方法。




### addView(xView)

> 添加子视图

- 参数 : xView {XView} 控件


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//创建一个新的文本控件
var textView = $ui.create("text").setText("新添加的文本");
//添加到布局中
layout.addView(textView);
```


### addView(view)

> 添加子视图

- 参数 : view {View} 控件


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//创建一个新的原生文本控件
var textView = new TextView(activity);
textView.setText("原生文本");
//添加到布局中
layout.addView(textView);
```


### removeView(xView)

> 移除子视图

- 参数 : xView {XView} 要移除的控件


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//获取要移除的控件
var childView = ui.id("childView");
//从布局中移除
layout.removeView(childView);
```


### removeView(view)

> 移除子视图

- 参数 : view {View} 要移除的原生控件


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//获取要移除的原生控件
var nativeView = findViewById(R.id.native_view);
//从布局中移除
layout.removeView(nativeView);
```


### removeView(index)

> 根据索引移除子视图

- 参数 : index {Integer} 子视图索引


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//移除第一个子视图
layout.removeView(0);
```


### removeView(from, to)

> 批量移除子视图

- 参数 : from {Integer} 起始索引
- 参数 : to {Integer} 结束索引


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//移除从索引1开始的3个子视图
layout.removeView(1, 3);
```


### removeAll()

> 移除所有子视图


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取布局控件
var layout = ui.id("myLayout");
//清空所有子视图
layout.removeAll();
```


