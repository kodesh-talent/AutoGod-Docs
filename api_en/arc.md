# $arc - 悬浮球

- 更新时间:2026-10-22 10:55:45

> 悬浮球（扇形悬浮菜单）对象，脚本里叫 $arc。
> 
> 一个"容器"负责显示和关闭一组按钮，按钮用 item 创建后装进容器。
> 



```javascript
var item = $arc.item("logo_ag");
$arc.body("工具菜单").add(item).show();
```




![](./img/407372540692722.gif)

### item(iconName)

> 创建悬浮菜单项
> 
> 先创建一个小按钮（菜单项），指定它显示什么图标。
> 
> 一个容器可以保存并显示多个菜单项。
> 
> 每个菜单项都可以使用自己的样式，样式直接在菜单项上配置。

- 参数 : iconName {string} 图标：可填内置图标资源名，或本地自定义图片的相对路径
- 返回 : {MenuItem} 创建好的菜单项（小按钮）对象，之后用容器的 add 方法把它装进去
- 版本 : 1.0.0


```javascript
//创建悬浮小按钮,可以被容器添加进去
var menu1 = $arc.item("logo_ag");//内置图标资源名称或者本地自定义图片相对路径
//之后可以创建容器并且显示，例如：
$arc.body("悬浮球1号").add(menu1).show();
//如果有多个悬浮小按钮：
var menu01 = $arc.item("logo_ag");
var menu02 = $arc.item("ic_color");
$arc.body("悬浮球2号").add(menu01).add(menu02).show();
```


### body(name)

> 创建菜单容器
> 
> 容器负责显示和关闭菜单，也可以保存并显示多个菜单项。
> 
> 已有同名悬浮菜单显示时，不能再次显示第二个同名菜单。

- 参数 : name {string} 这个悬浮菜单容器的名字，用来区分和关闭，不能与已显示的同名菜单重复
- 返回 : {MenuBody} 创建好的菜单容器对象，之后用 add 装按钮、show 显示
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器,用于存放多个小按钮，并且显示
var mBody01 = $arc.body("悬浮球1号");//指定一个名称，方便后面根据名称关闭
//添加一个按钮并且显示，例如：
var item = $arc.item("logo_ag"); //先建一个按钮
mBody01.add(item).show();        //装进容器并显示
```


### has(name)

> 检查悬浮菜单是否存在

- 参数 : name {string} 要检查的悬浮菜单容器名字
- 返回 : {boolean} 该名字的悬浮菜单当前正在显示就返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
if($arc.has("悬浮球1号")){
    toast("悬浮球1号存在");
}
```


### close(name)

> 关闭当前资源。
> 
> 按名称关闭菜单容器

- 参数 : name {string} 要关闭的悬浮菜单容器名字
- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
if ($arc.has("tools")) $arc.close("tools");
log("悬浮球已关闭");
}</pre>


```javascript
$arc.close("悬浮球1号");
```


### closeAll()

> 关闭全部菜单容器
> 
> 关闭全部已创建的悬浮菜单。

- 版本 : 1.0.0


```javascript
//关闭全部悬浮球(容器)
$arc.closeAll();
```


