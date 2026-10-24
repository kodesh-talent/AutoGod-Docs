# $ui - 界面交互

- 更新时间:2026-10-22 10:58:44

> UI交互界面




### run(runnable)

> ui线程

- 参数 : runnable {function(){}} ui线程 
- 版本 : 1.1.2


```javascript
//在ui线程中执行
$ui.run(function(){
    //在ui线程中执行的代码
});
```


### layout(xmlOrPath)

> 解析全屏布局
> 
> 创建一个ui对象,并且解析布局,最终返回这个ui对象

- 参数 : xmlOrPath {string} xml内容或者路径 
- 返回 : {UI}
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("./res/main.xml");
```


### sheet(activity)

> 显示底部弹窗

- 参数 : activity {activity} 需要显示底部弹窗的活动对象
- 返回 : {Sheet} 弹窗对象
- 版本 : 1.5.5


```javascript
//假如已经显示了一个ui了
var ui = $ui.layout("main.xml");
ui.show();
//当ui显示之后就可以获取对应界面的activity活动对象了
var sheet = $ui.sheet(ui.activity());//创建目标活动的底部弹窗对象
sheet.layout("sheet.xml"); //解析sheet布局
sheet.id("mButton"); //绑定sheet中的组件事件
sheet.show(); //显示底部弹窗
```


### toast(text)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : text {string} 文本 
- 版本 : 1.1.2


```javascript
$ui.toast("文本");
```


### toast(text, gravity)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : text {string} 文本 
- 参数 : gravity {string} 位置 
- 版本 : 1.1.2


```javascript
$ui.toast("文本","center");
```


### toPx(dp)

> dp转px

- 参数 : dp {float} dp(虚拟长度单位)
- 返回 : {float} 转换后的px(像素值)
- 版本 : 1.8.2


```javascript
//获取10dp的真实像素单位
var px = $ui.toPx(10);
```


### toDp(px)

> px转dp

- 参数 : px {float} 要转换的px(像素值)
- 返回 : {float} 转换后的(dp)虚拟像素单位
- 版本 : 1.8.2


```javascript
//获取10像素的(dp)虚拟单位值
var dp = $ui.toDp(10);
```


