# $res - 资源管理器

- 更新时间:2026-10-22 10:55:50

> 资源管理器（脚本里直接用 $res 或 $资源）。
> 
> 它像一个“小记事本”：你可以把一些数据（一段文字、一个数字、一个真假值）起个名字存进去，
> 下次再按名字取出来。这些数据会被持久化保存，脚本关掉再打开还在。
> 
> 使用步骤：先 create("名字") 得到一个资源本，再 set 存数据、get 取数据。
> 资源可以跨线程访问，但它不是外部文件系统，别把它当普通文件夹用。



```javascript
//创建一本名为“我的资源”的资源本
var res = $res.create("我的资源");
//存一条数据：名字叫“名字”，内容是“张三”
res.set("名字", "张三");
//再按名字取出来
log("取出的名字是：" + res.get("名字"));
```




### create(appName)

> 创建一本资源本（用一个名字区分不同的资源本）。
> 
> 同一个名字会对应同一份存储的数据。以后 set/get 都是在这本资源本里操作。

- 参数 : appName {String} 资源本的名字
- 返回 : {AgRes} 资源本对象，之后用它 set/get 存取数据
- 版本 : 1.0.0


```javascript
//创建一本资源本，名字叫“我的资源”
var res = $res.create("我的资源");
log("资源本创建好了");
```


### set(resName, resData)

> 往资源本里存一条数据。
> 
> 给数据起个名字（resName），再放进内容（resData，可以是文字、数字、真假、对象）。
> 下次用 get(同一个名字) 就能取出来。同名会被覆盖。

- 参数 : resName {String} 这条数据的名字（以后按它来取）
- 参数 : resData {Object} 要存的内容
- 版本 : 1.0.0


```javascript
var res = $res.create("我的资源");
res.set("名字", "张三");      //存文字
res.set("年龄", 18);          //存数字
res.set("是否男", true);       //存真假
log("数据已保存");
```


### get(resName)

> 按名字从资源本里取一条数据。
> 
> 取出来的内容会自动按它原来的类型返回（对象会被解析成脚本对象）。
> 如果这个名字不存在，会返回 null。

- 参数 : resName {String} 要取的数据的名字
- 返回 : {Object} 这条数据的内容；不存在时返回 null
- 版本 : 1.0.0


```javascript
var res = $res.create("我的资源");
res.set("名字", "张三");
var name = res.get("名字");   //取出内容
log("取出的名字是：" + name);
```


### get(resName, defaultValue)

> 按名字取一条文字数据，如果没有就返回你给的默认文字。
> 
> 例如 get("name", "无名氏")：存过就返回存的文字，没存过就返回 "无名氏"。

- 参数 : resName {String} 要取的数据的名字
- 参数 : defaultValue {String} 没有这条数据时返回的默认文字
- 返回 : {String} 取出的文字，或默认文字


```javascript
var res = $res.create("我的资源");
//从没存过“姓名”，这里会返回默认值“张三”
var name = res.get("姓名", "张三");
log("姓名是：" + name);
```


### get(resName, defaultValue)

> 按名字取一个小数数据，没有就返回你给的默认小数。
> 
> 如果存的内容不是数字，会返回 -1。

- 参数 : resName {String} 要取的数据的名字
- 参数 : defaultValue {float} 没有这条数据时返回的默认小数
- 返回 : {float} 取出的小数，或默认小数；内容不是数字时返回 -1


```javascript
var res = $res.create("我的资源");
res.set("PI", 3.14);
var pi = res.get("PI", 0.0);   //取出 3.14
log("圆周率：" + pi);
```


### get(resName, defaultValue)

> 按名字取一个整数数据，没有就返回你给的默认整数。
> 
> 如果存的内容不是数字，会返回 -1。

- 参数 : resName {String} 要取的数据的名字
- 参数 : defaultValue {int} 没有这条数据时返回的默认整数
- 返回 : {int} 取出的整数，或默认整数；内容不是数字时返回 -1


```javascript
var res = $res.create("我的资源");
res.set("age", 18);
var age = res.get("age", 0);   //取出 18
log("年龄是：" + age);
```


### get(resName, defaultValue)

> 按名字取一个真假值，没有就返回你给的默认真假值。
> 
> 用于存开关状态，例如“是否已开启”。

- 参数 : resName {String} 要取的数据的名字
- 参数 : defaultValue {boolean} 没有这条数据时返回的默认真假值
- 返回 : {boolean} 取出的真假值，或默认真假值


```javascript
var res = $res.create("我的资源");
res.set("已登录", true);
var isLogin = res.get("已登录", false);   //取出 true
if (isLogin) {
    log("已经登录了");
}
```


### load(path)

> 把一个本地资源文件拷贝加载到这本资源本的内部存储里。
> 
> 参数 path 是你准备好的资源文件路径，它会被复制进来，之后就能用 get 读取里面的数据了。
> 返回 true 表示加载成功，false 表示失败。

- 参数 : path {String} 要加载的资源文件路径
- 返回 : {boolean} true 表示成功，false 表示失败
- 版本 : 1.1.4


```javascript
var res = $res.create("我的资源");
var ok = res.load("res/backup.res");   //加载外部资源文件
if (ok) {
    log("加载成功，当前内容：" + res.cat());
}
```


### ls()

> 列出这本资源本里所有数据的名字。
> 
> 返回一个名字列表，可以遍历它看看都存了哪些条数据。

- 返回 : {List} 所有数据名字的列表
- 版本 : 1.0.0


```javascript
var res = $res.create("我的资源");
res.set("名字", "张三");
res.set("年龄", 18);
var names = res.ls();          //取出所有名字
for (var i = 0; i < names.size(); i++) {
    log("第" + i + "条数据叫：" + names.get(i));
}
```


### cat()

> 把这本资源本的全部内容以一段文字（JSON 形式）打印出来。
> 
> 用来查看现在里面都存了什么。没有任何数据时返回 "{}"。

- 返回 : {String} 资源本的全部内容文字
- 版本 : 1.0.0


```javascript
var res = $res.create("我的资源");
res.set("名字", "张三");
res.set("年龄", 18);
log("当前资源内容：" + res.cat());
```


### dump(path)

> 把这本资源本内部的数据导出（拷贝）到你指定的文件路径。
> 
> 本质是把内部存储的数据复制到外部路径，会自动补上 .res 后缀。
> 返回最终保存的文件路径。

- 参数 : path {String} 想保存到的文件路径
- 返回 : {String} 实际保存出来的文件路径
- 版本 : 1.0.0


```javascript
var res = $res.create("我的资源");
res.set("名字", "张三");
res.set("年龄", 18);
var out = res.dump("/sdcard/backup");   //导出到这个路径
log("已导出到：" + out);
```


