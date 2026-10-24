# UiSelector - UI选择器

- 更新时间:2026-10-22 10:55:44

> 界面选择器（用来在当前屏幕上“按条件找控件”）。
> 
> 一个手机界面上有成百上千个小控件（按钮、文字、图片……），你不可能一个个去点。
> 选择器就是一张“寻人启事”：你先告诉它你要找什么样的控件（文字是什么、id是什么、能不能点、在屏幕哪个区域……），
> 它再帮你把符合条件的节点找出来。
> 
> 使用分两步：
> (1) 筛选元素：一串 .text("xx").cls("xx") 这样的方法连在一起，把条件越收越窄；
> (2) 选中元素：最后调用 findFirst / findAll / waitFirst 等方法，真正把节点取出来。
> 注意：每个加条件的方法都会“返回它自己”，所以可以像搭积木一样一直点下去（这叫链式调用）。



```javascript
//第一步：创建一个选择器
var selector = $act.selector();
//第二步：连续加条件——只要文字是“登录”、并且是按钮的节点
selector = selector.text("登录").cls("android.widget.Button");
//第三步：在当前屏幕上找到符合条件的第一个节点
var node = selector.findFirst();
//上面三步其实可以一口气写完：
var node = $act.selector().text("登录").cls("android.widget.Button").findFirst();
if (node != null) {
    node.click(); //找到了就点它
}
```




