# UI - 界面对象

- 更新时间:2026-10-22 10:58:43

> 界面对象




### 获得视图()

> 获取解析后的最大布局

- 返回 : {View} 返回最大布局
- 版本 : 1.5.8


```javascript
//解析布局
var 界面 = $ui.解析布局("主界面.xml");
//获取最大视图
var 最大视图 = 界面.获得视图();
```


### 找控件(标识)

> 通过标识找到组件

- 参数 : 标识 {字符串} 组件标识 
- 返回 : {XView} 控件


```javascript
var 界面 = $ui.解析布局("主界面.xml");
//获取组件
var 按钮 = 界面.找控件("按钮");
```


### 界面线程(回调函数)

> 在ui线程中执行

- 参数 : 回调函数 {function() {}} ui线程回调函数


```javascript
var 界面 = $ui.解析布局("主界面.xml");
//在ui线程中执行
界面.界面线程(function() {
    //在ui线程中执行的代码
});
```


### 吐司(文本)

> 悬浮吐司
> 
> 悬浮吐司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : 文本 {字符串} 文本
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
//悬浮吐司
界面.吐司("文本");
```


### 吐司(文本, 重力)

> 悬浮吐司
> 
> 悬浮吐司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : 文本 {字符串} 文本
- 参数 : 重力 {字符串} 重力
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
//悬浮吐司
界面.吐司("文本","中间");
```


### 显示()

> 显示界面

- 返回 : {UI} 界面
- 版本 : 1.12


```javascript
var 界面 = $ui.解析布局("主界面.xml");
//显示界面
界面.显示();
```


### 结束()

> 结束界面


```javascript
var 界面 = $ui.解析布局("主界面.xml");
//显示界面
界面.显示();
//找一个按钮控件来关闭界面
界面.找控件("关闭按钮").点击事件(function(){
    //关闭界面
    界面.结束();
});
```


### 获得活动对象()

> 等待获得activity对象
> 
> 注意:如果没有解析界面,那么就直接返回null
> 如果没有显示界面,也会直接返回null
> 如果解析成功并且成功显示,那么就会进入循环中,不断的等待判断activity是否获取成功,如果获取成功,则直接返回activity

- 返回 : {AppCompatActivity} activity
- 版本 : 1.1.2


```javascript
//解析界面
var 界面 = $ui.解析布局("主界面.xml");
//显示界面
界面.显示();
//显示完界面之后即可等待获取到activity对象
var 活动对象 = 界面.获得活动对象();
```


### 当活动开始(回调)

> 界面初始时执行

- 参数 : 回调 {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动开始(function(activity) {
    //界面初始时执行
});
```


### 当活动恢复(回调)

> 重返界面时执行

- 参数 : 回调 {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动恢复(function(activity) {
    //重返界面时执行
});
```


### 当活动暂停(回调)

> 界面暂停时执行

- 参数 : 回调 {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动暂停(function(activity) {
    //界面暂停时执行
});
```


### 当活动停止(回调)

> 界面停止时执行

- 参数 : 回调 {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动停止(function(activity) {
    //界面停止时执行
});
```


### 当活动销毁(回调)

> 界面销毁时执行

- 参数 : 回调 {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动销毁(function(activity) {
    //界面销毁时执行(一般用来释放资源)
});
```


### 当活动重启(回调)

> 重新刷新界面时执行

- 参数 : 回调 {function(activity) {}} 生命周期回调
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动重启(function(activity) {
    //重新刷新界面时执行
});
```


### 当活动结果(回调)

> 活动结果事件

- 参数 : 回调 {function(requestCode,resultCode,intent,activity) {}} 活动结果事件
- 版本 : 1.4.9


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动结果(function(requestCode,resultCode,intent,activity) {
    //活动结果事件(一般用来申请权限时作为结果回调)
    //回调参数类型:
    //int requestCode
    //int resultCode
    //Intent intent
    //AppCompatActivity activity
});
```


### 当上下文菜单创建(回调)

> 上下文菜单创建事件

- 参数 : 回调 {function(menu,view,menuInfo,activity) {}} 上下文菜单创建事件
- 版本 : 1.4.9


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当上下文菜单创建(function(menu,view,menuInfo,activity) {
    //上下文菜单创建事件
    //回调函数参数类：
    //ContextMenu menu (其API涉及安卓API，请自行参考安卓文档)
    //View view
    //ContextMenu.ContextMenuInfo menuInfo (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当选项菜单创建(回调)

> 选项菜单创建事件

- 参数 : 回调 {function(menu,activity) {}} 选项菜单创建事件
- 版本 : 1.4.9


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当选项菜单创建(function(menu,activity) {
    //选项菜单创建事件
    //回调函数参数类：
    //Menu menu (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当选项菜单面板创建(回调)

> 选项菜单面板创建事件

- 参数 : 回调 {function(featureId,menu,activity) {}} 选项菜单面板创建事件
- 版本 : 1.4.9


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当选项菜单面板创建(function(featureId,menu,activity) {
    //选项菜单创建事件
    //回调函数参数类：
    //int featureId
    //Menu menu (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当选项菜单选中(回调)

> 选项菜单点击事件

- 参数 : 回调 {function(item,activity) {}} 选项菜单点击事件
- 版本 : 1.4.9


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当选项菜单选中(function(item,activity) {
    //选项菜单创建事件
    //回调函数参数类：
    //MenuItem item (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当按键按下(回调)

> 按键按下事件

- 参数 : 回调 {function(keyCode,event,activity) {return false;}}  按键抬起事件
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当按键按下(function(keyCode,event,activity) {
    //当按键按下回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### 当按键抬起(回调)

> 按键抬起事件

- 参数 : 回调 {function(keyCode,event,activity) {return false;}}  按键抬起事件
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当按键抬起(function(keyCode,event,activity) {
    //按键抬起回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### 当按键长按(回调)

> 长按事件

- 参数 : 回调 {function(keyCode,event,activity) {return false;}}  长按事件
- 版本 : 1.1.2


```javascript
var 界面 = $ui.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当按键长按(function(keyCode,event,activity) {
    //按键长按回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### 设置方向(方向)

> 设置界面显示方向
> 
> 可选值：h(横向)、v(竖向)、auto(自动)、null(默认)

- 参数 : 方向 {字符串} 界面显示方向
- 版本 : 1.8.7


```javascript
//首先获取ui对象
var 界面 = $ui.解析布局("主界面.xml");
//设置界面显示方向
界面.设置方向("横向");
//当界面显示的时候就会转为横屏
界面.显示();
//参数说明：（以下效果也会因使用户手机系统设置而改变）
//h、横向：进入界面后界面强制横屏
//v、竖向：进入界面后界面强制竖屏
//auto、自动：进入界面后界面随用户手机感应自动切换横竖屏
//null、默认：无任何效果
```


### 设置主题(主题名称)

> 设置主题
> 
> 设置主题后，需要重启才会生效。
> 
> "blue.light"、"blue.dark"、"green.light"、"green.dark"、"pink.light"、"pink.dark"、"orange.light"、"orange.dark"、"yellow.light"、"yellow.dark"、"purple.light"、"purple.dark"。

- 参数 : 主题名称 {字符串} 主题名称
- 版本 : 1.9.7


```javascript
//解析布局
var 界面 = $ui.解析布局("main.xml");
//显示界面
界面.显示();
//绑定一个按钮切换主题
界面.找控件("我的按钮").点击事件(function() {
    界面.设置主题("pink.light");
});
```


