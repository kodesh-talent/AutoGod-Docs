# SelectFloaty - 选择悬浮窗

- 更新时间:2026-10-22 10:55:49

> 区域选择悬浮窗。
> 
> 它会铺满整个屏幕，让你用手指在屏幕上拖出一个矩形框，框住想要的那一块区域；
> 松手后系统会把你框出的区域（Rect 矩形对象）通过创建时传的回调告诉你。
> 通常用 $floaty.newSelect(回调函数) 创建并立即开始选择。



```javascript
var selector = $floaty.newSelect(function(region) {
    //松手后回调，region 就是你框出来的矩形区域
    log("选的区域：" + region.left + "," + region.top + "," + region.right + "," + region.bottom);
});
```




### const {WindowManager.LayoutParams} params;

> 这个悬浮窗在系统里的窗口参数（WindowManager.LayoutParams）。
> 
> 记录悬浮窗的位置、宽高等底层信息，是公开字段。普通用户一般不需要直接动它。

- 版本 : 1.8.3


```javascript
var selector = $floaty.newSelect(function(region) {});  //创建区域选择悬浮窗
log(selector.params);                                   //打印它的窗口参数（高级用户才改）
```


### const {WindowManager} manager;

> 系统的悬浮窗管理器（WindowManager）。
> 
> 负责把这个悬浮窗加到屏幕上或移除。普通用户一般不需要直接碰它。

- 版本 : 1.8.3


```javascript
var selector = $floaty.newSelect(function(region) {});  //创建区域选择悬浮窗
log(selector.manager);                                  //打印系统悬浮窗管理器
```


### 关闭()

> 手动关闭这个区域选择悬浮窗（中文写法）。
> 
> 和 close 完全一样，只是方法名是中文。

- 版本 : 1.8.3


```javascript
var selector = $floaty.newSelect(function(region) {
    log("选的区域：" + region);
});
sleep(5000);          //给用户 5 秒时间框选
selector.关闭();      //超时后强制关闭
```


