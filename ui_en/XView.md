# 控件父类-XView

- 更新时间:2026-10-22 10:58:43

> 控件父类-XView
> 
> 在应用中所有的控件或者布局都是这个类{XView}的子类，因此，这个类中的所有方法，所有的子类都能调用，故称为：公共方法。
> 
> 在代码示例中，多数情况下，我都是使用{XButton}按钮控件来进行演示的，其实任何控件都可以。




### getView()

> 获得安卓原生视图
> 
> 我们可以通过控件的getView()方法获得原生控件,从而进行原生操作
> 
> 对于[button]标签,对应的原生类就是[MaterialButton]
> 
> 对于[text]标签,对应的原生类就是[MaterialTextView]
> 
> 其余的请参考原生对照表
> 
> ::: tip 特殊示例
> 这里的 getView 是所有组件都有的一个方法(因为所有组件都继承XView类，换句话说:所有组件都是XView类型的)，在代码中的体现就是 ui.id("任何").getView() 都能拿到原生视图，
> 
> 需要注意：在本应用中有很多组件都是组合组件，例如：input(输入框)组件，其实是由{TextInputLayout}包裹了一个{TextInputEditText}
> 
> 我们需要注意：getView 是返回最大的组件视图，像上面所说的input(输入框)组件，返回的就是{TextInputLayout}类，如果我们想要获取{TextInputEditText}则需要参考input(输入框)的文档：通过getEditText方法获取{TextInputEditText}对象(参考input文档)。
> :::

- 返回 : {View} 安卓原生View


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件:{XButton}类型
var mButton = ui.id("mButton");//{XButton}属于{XView}的子类
//获得原生控件
var view = mButton.getView();//{MaterialButton}对象
//需要注意：在后续操作安卓原生对象的时候需要放在ui线程中进行
$ui.run(function() {
    view.setText("我是新的按钮");
});
//如果不操作原生控件，我们已经封装过ui线程这一步了，可以直接在其他线程中操作
mButton.setText("我是新的按钮");
```


### parseColor(color)

> 解析颜色
> 
> 可以通过这个函数获得主题颜色值或者一些常用颜色值

- 参数 : color {String} 颜色名称
- 返回 : {int} 颜色值


```javascript
var ui = $ui.layout("/ui.xml");
var myButton = ui.id("myButton");
//获取颜色值(返回int类型的颜色值)
var color = myButton.parseColor("white");
var color = myButton.parseColor("black");
var color = myButton.parseColor("null");
var color = myButton.parseColor("none");
var color = myButton.parseColor("green");
var color = myButton.parseColor("red");
var color = myButton.parseColor("blue");
var color = myButton.parseColor("yellow");
//主题颜色值(返回int类型的颜色值)
var color = myButton.parseColor("colorPrimary");//(常用)一般是主题最明显的颜色
var color = myButton.parseColor("colorSurface");//(常用)一般是背景颜色：亮色主题一般呈现白色，暗色主题一般呈现黑色
var color = myButton.parseColor("colorOnSurface");//(常用)一般是文字颜色：亮色主题一般呈现黑色，暗色主题一般呈现白色
var color = myButton.parseColor("colorOnPrimary");
var color = myButton.parseColor("colorPrimaryContainer");
var color = myButton.parseColor("colorOnPrimaryContainer");
var color = myButton.parseColor("colorSecondary");
var color = myButton.parseColor("colorOnSecondary");
var color = myButton.parseColor("colorSecondaryContainer");
var color = myButton.parseColor("colorOnSecondaryContainer");
var color = myButton.parseColor("colorTertiary");
var color = myButton.parseColor("colorOnTertiary");
var color = myButton.parseColor("colorTertiaryContainer");
var color = myButton.parseColor("colorOnTertiaryContainer");
var color = myButton.parseColor("colorError");
var color = myButton.parseColor("colorErrorContainer");
var color = myButton.parseColor("colorOnErrorContainer");
var color = myButton.parseColor("colorOnBackground");
var color = myButton.parseColor("colorSurfaceVariant");
var color = myButton.parseColor("colorOnSurfaceVariant");
var color = myButton.parseColor("colorOutline");
var color = myButton.parseColor("colorOutlineVariant");
var color = myButton.parseColor("colorPrimaryInverse");
```


### dp(dp)

> 将dp转换成对应的px（像素）。
> 
> dp 是一种与屏幕密度无关的尺寸单位：同样写 16dp，在不同手机上看起来大小差不多；
> 而 px 是屏幕上真实的像素数。这个方法会根据当前手机的屏幕密度，把 dp 自动换算成真实像素。
> 拿到任意控件后都可以调用，常用来设置间距、宽高等尺寸。

- 参数 : dp {float} 要换算的 dp 长度
- 返回 : {float} 换算后的 px（像素）长度


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//把 16dp 换算成当前手机上的真实像素
var px = ui.dp(16);
log("16dp 等于 " + px + " 像素");
```


### bgImg(path)

> 设置背景图片

- 参数 : path {String} 图片路径


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置背景图片
mButton.bgImg("./res/bg.png");
```


### snack(msg)

> 显示 Snackbar

- 参数 : msg {String} 信息 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//显示信息条
mButton.snack("我是信息");
```


### snack(msg, title, callback)

> 显示 Snackbar

- 参数 : msg {String} 信息 
- 参数 : title {String} action标题 
- 参数 : callback {function(view) {}} 点击事件回调 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//显示信息条
mButton.snack("我是信息","确定",function(view) {
    //点击确定触发的事件
    toast("点击了确定");
});
```


### click(callback)

> 设置点击事件

- 参数 : callback {function(view) {}} 点击事件 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置点击事件
mButton.click(function(view) {
    //点击事件
    toast("我被点击了");
});
```


### longClick(callback)

> 设置长按事件

- 参数 : callback {function(view) {}} 点击事件 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置长按事件
mButton.longClick(function(view) {
    //点击事件
    toast("我被长按了");
});
```


### popup(titles, callback)

> 显示选项菜单

- 参数 : titles {String[]} 选项 
- 参数 : callback {function(title) {}} 回调 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//显示选项菜单
mButton.popup(["选项1","选项2","选项3"],function(title) {
    toast("点击了选项:"+title);
});
```


### popup(titles, gravity, callback)

> 显示选项菜单

- 参数 : titles {String[]} 选项 
- 参数 : gravity {String} 重力,例如:"center|start"(默认值) 
- 参数 : callback {function(title) {}} 回调 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//显示选项菜单
mButton.popup(["选项1","选项2","选项3"],"start|center",function(title) {
    toast("点击了选项:"+title);
});
```


### setEnabled(enabled)

> 是否启用控件

- 参数 : enabled {boolean} true:启用,false:禁用 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//禁用
mButton.setEnabled(false);
```


### isEnabled()

> 判断可用

- 返回 : {boolean} true:启用,false:禁用 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//是否可用
var is = mButton.isEnabled();
if(is){
    toast("可用");
}
```


### setVisibility(visibility)

> 设置可见性

- 参数 : visibility (使用$ui中的常量,例如:ui.INVISIBLE) 


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置成不可见
mButton.setVisibility($ui.GONE);
//设置成可见
//mButton.setVisibility($ui.VISIBLE);
```


### isVisibility()

> 获得可见性

- 返回 : {int} (使用$ui中的常量,例如:ui.INVISIBLE)


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//获得可见性的值
var vis = mButton.isVisibility();
if(vis==$ui.VISIBLE){
    toast("可见");
}
```


### setFocusable(focusable)

> 设置可聚焦

- 参数 : focusable {boolean} true:控件可获得焦点,false:控件不可获得焦点


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置控件是否可聚焦
mButton.setFocusable(true);
```


### setClickable(clickable)

> 设置可点击

- 参数 : clickable {boolean} true:控件可被点击,false:控件不可被点击


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置控件是否可点击
mButton.setClickable(true);
```


### setAlpha(alpha)

> 设置透明度

- 参数 : alpha {float} 0.5:控件半透明,1:控件不透明


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置透明度
mButton.setAlpha(0.5);
```


### getAlpha()

> 获得透明度

- 返回 : {float} 控件透明度值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//获得透明度
var alpha = mButton.getAlpha();
```


### setElevation(elevation)

> 设置立体值
> 
> 可以让控件看起来更加立体

- 参数 : elevation {int} 立体值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置立体值
mButton.setElevation(10);
```


### getX()

> 获取x值
> 获取相对于父控件的x值

- 返回 : {float} x值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//获取x值
var x = mButton.getX();
```


### setX(x)

> 设置x值
> 设置在父控件中x的值

- 参数 : x {float} x值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置x值
mButton.setX(10);
```


### getY()

> 获取y值
> 获取相对于父控件的x值

- 返回 : {float} y值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//获取y值
var y = mButton.getY();
```


### setY(y)

> 设置y值
> 设置在父控件中y的值

- 参数 : y {float} y值


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//设置y值
mButton.setY(10);
```


### getW()

> 获得控件宽度

- 返回 : 当前控件宽度（像素）；控件尚未布局时通常为 0


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//获得控件宽度
mButton.getW();
```


### getH()

> 获得控件高度

- 返回 : {int} 当前控件高度（像素）；控件尚未布局时通常为 0


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//获得控件高度
mButton.getH();
```


### onTouch(callback)

> 获得控件高度

- 参数 : callback {function(motionEvent,view) {return false;}} 触摸回调


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./myUi.xml");
//拿到控件
var mButton = ui.id("mButton");
//处理触摸事件
mButton.onTouch(function(event,view) {
    //处理触摸事件
    return true;
});
```


### getName()

> 获取组件的节点名称

- 返回 : {String} 组件节点名称
- 版本 : 1.5.5


```}
var ui = $ui.layout("main.xml");
var button = ui.id("submit");
var typeName = button.getName();
```


