# $floaty - 悬浮窗

- 更新时间:2026-10-22 10:55:48

> $floaty：悬浮窗工具，用来在屏幕上盖自己的小窗口。
> 
> 支持三种悬浮窗：应用级（隐蔽、只盖本 App）、系统级（全屏覆盖但易被检测）、
> 可调节（可拖动调整大小），还有一个框选区域的范围选择器。用之前必须先拿到悬浮窗权限。



```javascript
// 先检查悬浮窗权限
var allowed = $floaty.hasPermit();
```




### 获取权限()

> 获取悬浮窗权限：阻塞等待直到授权成功。
> 
> 这是 $floaty.getPermit 的中文叫法。

- 返回 : {布尔值} true 表示已授权
- 版本 : 1.7.0


```javascript
var 获取成功 = $floaty.获取权限();
if (获取成功) {
    log("拿到悬浮窗权限");
}
```


### 有权限()

> 是否有悬浮窗权限：只检查不弹窗。
> 
> 这是 $floaty.hasPermit 的中文叫法。

- 返回 : {布尔值} true 表示已有权限
- 版本 : 1.7.0


```javascript
var 有权限 = $floaty.有权限();
if (有权限) {
    log("有悬浮窗权限");
}
```


### 新建可调节(xml内容或者路径)

> 新建可调节悬浮窗：可拖动、可调大小。
> 
> 这是 $floaty.newAdj 的中文叫法，返回 AdjFloaty 对象。

- 参数 : xml内容或者路径 {string} 布局 xml 路径或内容
- 返回 : {AdjFloaty} 可调节悬浮窗对象
- 版本 : 1.7.0


```javascript
$floaty.获取权限();
var 可调节 = $floaty.新建可调节("./res/layout/floaty_adj.xml");
```


### 新建应用级(xml内容或者路径)

> 新建应用级悬浮窗：只盖在本 App 上，隐蔽。
> 
> 这是 $floaty.newApp 的中文叫法，返回 AppFloaty 对象。

- 参数 : xml内容或者路径 {string} 布局 xml 路径或内容
- 返回 : {AppFloaty} 应用级悬浮窗对象
- 版本 : 1.7.0


```javascript
$floaty.获取权限();
var 应用悬浮窗 = $floaty.新建应用级("./res/layout/floaty_app.xml");
```


### 新建应用级(xml内容或者路径, 可触摸)

> 新建应用级悬浮窗（可指定是否触摸）。
> 
> 这是带触摸开关版 $floaty.newApp 的中文叫法。

- 参数 : xml内容或者路径 {string} 布局 xml 路径或内容
- 参数 : 可触摸 {布尔值} true 可触摸，false 穿透
- 返回 : {AppFloaty} 应用级悬浮窗对象
- 版本 : 1.8.3


```javascript
$floaty.获取权限();
var 应用悬浮窗 = $floaty.新建应用级("./res/layout/floaty_app.xml", false);
```


### 新建系统级(xml内容或者路径)

> 新建系统级悬浮窗：可全屏覆盖，但易被检测。
> 
> 这是 $floaty.newSys 的中文叫法，返回 SysFloaty 对象。

- 参数 : xml内容或者路径 {string} 布局 xml 路径或内容
- 返回 : {SysFloaty} 系统级悬浮窗对象
- 版本 : 1.7.0


```javascript
$floaty.获取权限();
var 系统悬浮窗 = $floaty.新建系统级("./res/layout/floaty_sys.xml");
```


### 新建系统级(xml内容或者路径, 可触摸)

> 新建系统级悬浮窗（可指定是否触摸）。
> 
> 这是带触摸开关版 $floaty.newSys 的中文叫法。

- 参数 : xml内容或者路径 {string} 布局 xml 路径或内容
- 参数 : 可触摸 {布尔值} true 可触摸，false 穿透
- 返回 : {SysFloaty} 系统级悬浮窗对象
- 版本 : 1.8.3


```javascript
$floaty.获取权限();
var 系统悬浮窗 = $floaty.新建系统级("./res/layout/floaty_sys.xml", false);
```


### 新建范围选择(回调)

> 新建范围选择悬浮窗：让用户框选一块区域。
> 
> 这是 $floaty.newSelect 的中文叫法。

- 参数 : 回调 {function(rect){}} 选完回调，参数是区域数据
- 返回 : {SelectFloaty} 范围选择悬浮窗对象
- 版本 : 1.8.3


```javascript
$floaty.获取权限();
var 选择器 = $floaty.新建范围选择(function(范围) {
    log("用户选择范围：" + 范围);
});
```


![](./img/floaty_newSelect.png)

### 关闭所有()

> 关闭所有悬浮窗。
> 
> 这是 $floaty.closeAll 的中文叫法。

- 版本 : 1.7.0


```javascript
$floaty.关闭所有();
```


