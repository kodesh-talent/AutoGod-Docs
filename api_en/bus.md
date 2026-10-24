# $bus - 消息总线

- 更新时间:2026-10-22 10:55:46

> 消息总线（也叫事件总线）对象，脚本里叫 $bus。
> 
> 它像一个"广播站"：一个地方用 post 发布一条带名字的消息，另一个地方用 event 提前监听同名消息，
> 就能在收到消息时自动执行回调。常用于同一段脚本内部各部分之间互相传递消息、解耦代码。
> 



```javascript
$bus.event("taskDone", function(data) { log(data); });
$bus.post("taskDone", { ok: true });
```




### ls()

> 列出全部事件监听器

- 返回 : {String[]} 当前所有已注册监听器的名字列表（字符串数组形式）；一个都没有时返回空列表
- 版本 : 1.0.0


```javascript
//获得所有监听器列表
var monis = $bus.ls();
log(monis);//[我的监听器1号]
```


### post(name, object)

> 发布消息

- 参数 : name {String} 要发布的消息名字，必须和监听时用的名字一模一样才能收到
- 参数 : object {Object} 要随消息一起带给监听者的数据，可以是任意类型（字符串、数字、对象等）
- 版本 : 1.0.0


```javascript
$bus.post("我的监听器1号","我是数据");
```


### event(name, listener)

> 添加事件监听器。
> 
> 提前登记一个"名字 + 回调函数"：以后只要有人用 post 发了同名消息，这个回调就会自动被调用，
> 收到发来的数据 data。同名重复监听会覆盖之前的。

- 参数 : name {string} 要监听的消息名字，发布时名字一致才会触发
- 参数 : listener {function} 收到消息时要执行的回调函数，参数 data 就是发布时带过来的数据
- 版本 : 1.0.0


```javascript
$bus.event("我的监听器1号", function(data) {
    log("获得数据:" + data);
    toast(data);
});
```


### close(name)

> 移除事件监听器

- 参数 : name {string} 要关闭的监听器名字（监听时登记的那个名字）
- 版本 : 1.0.0


```javascript
//指定关闭监听器
$bus.close("我的监听器1号");
```


### clear()

> 移除全部事件监听器

- 版本 : 1.0.0


```javascript
$bus.clear();//关闭所有监听器
```


### stopAll()

> 停止并移除全部事件监听器。
> 
> 把当前登记的所有监听一次性全部清空，之后它们都不会再收到消息。效果和 clear() 完全一样。

- 版本 : 1.0.0


```javascript
$bus.stopAll();//关闭所有监听器效果和clear()一样
```


