# UI - 界面对象

- 更新时间:2026-10-22 10:58:43

> 界面对象




### getView()

> 获取解析后的最大布局

- 返回 : {View} 返回最大布局
- 版本 : 1.1.2


```javascript
//解析布局
var ui = $ui.layout("/main.xml");
//获取解析的最大视图
var view = ui.getView();
```


### id(id)

> 通过id获取控件

- 参数 : id {string} 控件id 
- 返回 : {XView} 返回控件
- 版本 : 1.1.2


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//获取组件
var mButton = ui.id("mButton");
```


### run(runnable)

> ui线程

- 参数 : runnable {function() {}} ui线程
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
//在ui线程中执行
ui.run(function() {
    //在ui线程中执行的代码
});
```


### toast(text)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : text {string} 文本
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
//悬浮土司
ui.toast("文本");
```


### toast(text, gravity)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : text {string} 文本
- 参数 : gravity {string} 重力
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
//悬浮土司
ui.toast("文本","center");
```


### show()

> 显示界面

- 返回 : 当前界面对象，可继续链式调用
- 版本 : 1.1.2


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//显示界面
ui.show();
```


### finish()

> 结束界面

- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.id("button").click(function() {
    //关闭界面
    ui.finish();
});
```


### activity()

> 等待获得activity对象
> 
> 注意:如果没有解析界面,那么就直接返回null
> 如果没有显示界面,也会直接返回null
> 如果解析成功并且成功显示,那么就会进入循环中,不断的等待判断activity是否获取成功,如果获取成功,则直接返回activity

- 返回 : {AppCompatActivity} activity
- 版本 : 1.1.2


```javascript
//解析界面
var ui = $ui.layout("main.xml");
//显示界面
ui.show();
//显示完界面之后即可等待获取到activity对象
var avt = ui.activity();
```


### onStart(runnable)

> 界面初始时执行

- 参数 : runnable {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onStart(function(activity) {
    //界面初始时执行
});
```


### onResume(runnable)

> 重返界面时执行

- 参数 : runnable {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onResume(function(activity) {
    //重返界面时执行
});
```


### onPause(runnable)

> 界面暂停时执行

- 参数 : runnable {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onPause(function(activity) {
    //界面暂停时执行
});
```


### onStop(runnable)

> 界面停止时执行

- 参数 : runnable {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onStop(function(activity) {
    //界面停止时执行
});
```


### onDestroy(runnable)

> 界面销毁时执行

- 参数 : runnable {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onDestroy(function(activity) {
    //界面销毁时执行(一般用来释放资源)
});
```


### onRestart(runnable)

> 重新刷新界面时执行

- 参数 : runnable {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onRestart(function(activity) {
    //重新刷新界面时执行
});
```


### onActivityResult(runnable)

> 活动结果事件

- 参数 : runnable {function(requestCode,resultCode,intent,activity) {}} 活动结果事件
- 版本 : 1.4.9


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onActivityResult(function(requestCode,resultCode,intent,activity) {
    //活动结果事件(一般用来申请权限时作为结果回调)
    //回调参数类型:
    //int requestCode
    //int resultCode
    //Intent intent
    //AppCompatActivity activity
});
```


### onCreateContextMenu(runnable)

> 上下文菜单创建事件

- 参数 : runnable {function(menu,view,menuInfo,activity) {}} 上下文菜单创建事件
- 版本 : 1.4.9


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onCreateContextMenu(function(menu,view,menuInfo,activity) {
    //上下文菜单创建事件
    //回调函数参数类：
    //ContextMenu menu (其API涉及安卓API，请自行参考安卓文档)
    //View view
    //ContextMenu.ContextMenuInfo menuInfo (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### onCreateOptionsMenu(runnable)

> 选项菜单创建事件

- 参数 : runnable {function(menu,activity) {}} 选项菜单创建事件
- 版本 : 1.4.9


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onCreateOptionsMenu(function(menu,activity) {
    //选项菜单创建事件
    //回调函数参数类：
    //Menu menu (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### onCreatePanelMenu(runnable)

> 选项菜单面板创建事件

- 参数 : runnable {function(featureId,menu,activity) {}} 选项菜单面板创建事件
- 版本 : 1.4.9


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onCreatePanelMenu(function(featureId,menu,activity) {
    //选项菜单创建事件
    //回调函数参数类：
    //int featureId
    //Menu menu (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### onOptionsItemSelected(runnable)

> 选项菜单点击事件

- 参数 : runnable {function(item,activity) {}} 选项菜单点击事件
- 版本 : 1.4.9


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onOptionsItemSelected(function(item,activity) {
    //选项菜单创建事件
    //回调函数参数类：
    //MenuItem item (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### onKeyDown(callback)

> 按键按下事件

- 参数 : callback {function(keyCode,event,activity) {return false;}} 按键按下事件
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onKeyDown(function(keyCode,event,activity) {
    //按键按下回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### onKeyUp(callback)

> 按键抬起事件

- 参数 : callback {function(keyCode,event,activity) {return false;}}  按键抬起事件
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onKeyUp(function(keyCode,event,activity) {
    //按键抬起回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### onKeyLongPress(callback)

> 长按事件

- 参数 : callback {function(keyCode,event,activity) {return false;}}  长按事件
- 版本 : 1.1.2


```javascript
var ui = $ui.layout("main.xml");
ui.show();
//周期函数
ui.onKeyLongPress(function(keyCode,event,activity) {
    //按键长按回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### setDir(dir)

> 设置界面显示方向
> 
> 可选值：h(横向)、v(竖向)、auto(自动)、null(默认)

- 参数 : dir {String} 界面显示方向
- 版本 : 1.8.7


```javascript
//首先获取ui对象
var ui = $ui.layout("main.xml");
//设置界面显示方向
ui.setDir("h");
//当界面显示的时候就会转为横屏
ui.show();
//参数说明：（以下效果也会因使用户手机系统设置而改变）
//h、横向：进入界面后界面强制横屏
//v、竖向：进入界面后界面强制竖屏
//auto、自动：进入界面后界面随用户手机感应自动切换横竖屏
//null、默认：无任何效果
```


### setTheme(style)

> 设置主题
> 
> 设置主题后，需要重启才会生效。
> 
> "blue.light"、"blue.dark"、"green.light"、"green.dark"、"pink.light"、"pink.dark"、"orange.light"、"orange.dark"、"yellow.light"、"yellow.dark"、"purple.light"、"purple.dark"。

- 参数 : style {String} 主题名称
- 版本 : 1.9.7


```javascript
//解析布局
var ui = $ui.layout("main.xml");
//显示界面
ui.show();
//绑定一个按钮切换主题
ui.id("mBut").click(function() {
    ui.setTheme("pink.light");
});
```


