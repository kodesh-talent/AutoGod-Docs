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




### screen(transCut, vertCut, index)

> 把屏幕切成网格，只在“指定的那一格范围内”找控件。
> 
> 当你知道目标控件大概在屏幕的某个角落、不想让它误找到别处时，用这个方法圈定一个搜索范围。
> 它的原理是：先把屏幕按 transCut 列、vertCut 行切成网格，再取第 index 格当作搜索区域。
> 这里的三个数字和 $screen.split(transCut, vertCut, index) 返回的那一块是同一回事，可以先用它画框调试。

- 参数 : transCut {int} 把屏幕横向（左右）切成几列
- 参数 : vertCut {int} 把屏幕纵向（上下）切成几行
- 参数 : index {int} 取第几格作为搜索范围，从 0 开始数
- 返回 : {UiSelector} 返回选择器自身，可以继续接着加条件
- 版本 : 1.0.0


```javascript
$draw.closeAll(); //先关掉旧的标记框
//把屏幕横竖都切成3份（共9格），取第8格（最下面那格）的范围，用来调试位置
var region = $screen.split(3, 3, 8);
$draw.rect(region); //把这一格画出来看看对不对
//位置确认好后，就让选择器只在这一格范围内找文字为“登录”的节点
var node = $act.selector().screen(3, 3, 8).text("登录").findFirst();
if (node != null) {
    node.click();
}
```


### clickable(able)

> 加条件：只要“能不能点”这个属性符合要求的节点。
> 
> able 填 true 就只找可点击的（按钮类）；填 false 只找不可点击的。

- 参数 : able {boolean} true 只要可点击的；false 只要不可点击的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要可点击的节点里，第一个
var node = $act.selector().clickable(true).findFirst();
if (node != null) {
    log("找到一个可点击节点");
}
```


### visible(able)

> 加条件：只要“现在看得见”这个属性符合要求的节点。
> 
> able 填 true 只找可见的；填 false 找看不见的。一般都用 true，因为看不见的节点点了也没用。

- 参数 : able {boolean} true 只要可见的；false 只要不可见的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.1


```javascript
//只要可见的节点里，第一个
var node = $act.selector().visible(true).findFirst();
if (node != null) {
    log("找到一个可见节点");
}
```


### longClickable(able)

> 加条件：只要“能不能长按”这个属性符合要求的节点。
> 
> able 填 true 只找可长按的；填 false 找不可长按的。

- 参数 : able {boolean} true 只要可长按的；false 只要不可长按的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要可长按的节点里，第一个
var node = $act.selector().longClickable(true).findFirst();
if (node != null) {
    log("找到一个可长按节点");
}
```


### enabled(able)

> 加条件：只要“现在是否可用”这个属性符合要求的节点。
> 
> able 填 true 只找可用的（没灰掉）；填 false 找灰掉不可用的。

- 参数 : able {boolean} true 只要可用的；false 只要不可用的（灰掉）
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要可用的节点里，第一个
var node = $act.selector().enabled(true).findFirst();
if (node != null) {
    log("找到一个可用节点");
}
```


### selected(able)

> 加条件：只要“当前是否被选中”这个属性符合要求的节点。
> 
> able 填 true 只找当前高亮/选中的；填 false 找未选中的。

- 参数 : able {boolean} true 只要已选中的；false 只要未选中的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要当前被选中的节点里，第一个
var node = $act.selector().selected(true).findFirst();
if (node != null) {
    log("找到一个被选中的节点");
}
```


### scrollable(able)

> 加条件：只要“能不能滚动”这个属性符合要求的节点。
> 
> able 填 true 只找可滚动的（列表类容器）；填 false 找不可滚动的。

- 参数 : able {boolean} true 只要可滚动的；false 只要不可滚动的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要可滚动的节点里，第一个（通常就是列表）
var node = $act.selector().scrollable(true).findFirst();
if (node != null) {
    log("找到一个可滚动列表");
}
```


### checkable(able)

> 加条件：只要“是不是可勾选控件”这个属性符合要求的节点。
> 
> able 填 true 只找复选框/开关这类控件；填 false 找不是的。注意这是“能不能勾”，当前勾没勾看 checked。

- 参数 : able {boolean} true 只要可勾选的；false 只要不可勾选的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要复选框/开关这类节点里，第一个
var node = $act.selector().checkable(true).findFirst();
if (node != null) {
    log("找到一个可勾选控件");
}
```


### checked(able)

> 加条件：只要“当前有没有被勾上”这个属性符合要求的节点。
> 
> able 填 true 只找已经勾上的；填 false 找没勾的。

- 参数 : able {boolean} true 只要已勾选的；false 只要未勾选的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要当前已经勾上的节点里，第一个
var node = $act.selector().checked(true).findFirst();
if (node != null) {
    log("找到一个已勾选的控件");
}
```


### region(x, y, w, h)

> 加条件：只找“所占区域和给定矩形完全一模一样”的节点。
> 
> 四个数字是 [左边, 上边, 宽度, 高度]，单位像素。要求节点的位置和大小都和你给的矩形完全相等才匹配，
> 条件很苛刻，一般很少用。想圈定搜索范围通常用 regionHas。

- 参数 : x {int} 矩形左边离屏幕左边的距离（像素）
- 参数 : y {int} 矩形上边离屏幕上边的距离（像素）
- 参数 : w {int} 矩形宽度（像素）
- 参数 : h {int} 矩形高度（像素）
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只找左上角在(0,0)、宽100高100的那个节点
var node = $act.selector().region(0, 0, 100, 100).findFirst();
if (node != null) {
    log("找到了");
}
```


### regionHas(x, y, w, h)

> 加条件：只找“完全落在你给的这块区域里”的节点。
> 
> 你给一个较大的矩形 [左边, 上边, 宽, 高]，只有整个节点都被这块大区域包住时才算匹配。
> 最常用：把搜索范围圈在屏幕某一块，避免点到别处。

- 参数 : x {int} 大范围左边离屏幕左边的距离（像素）
- 参数 : y {int} 大范围上边离屏幕上边的距离（像素）
- 参数 : w {int} 大范围宽度（像素）
- 参数 : h {int} 大范围高度（像素）
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只在屏幕上半部分（左上角0,0，宽540、高400的范围）里找“登录”
var node = $act.selector().regionHas(0, 0, 540, 400).text("登录").findFirst();
if (node != null) {
    node.click();
}
```


### regionInside(x, y, w, h)

> 加条件：只找“足够大、能把你给的这块小区域整个包住”的节点。
> 
> 和 regionHas 正好相反：你给一个较小的矩形，只有当节点本身大到能把这块小区域完全包含进去时才算匹配。
> 常用于找一个大容器，比如“哪个布局里包住了坐标(100,100)”。

- 参数 : x {int} 小范围左边离屏幕左边的距离（像素）
- 参数 : y {int} 小范围上边离屏幕上边的距离（像素）
- 参数 : w {int} 小范围宽度（像素）
- 参数 : h {int} 小范围高度（像素）
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找一个大容器，它必须能把左上角(0,0)宽100高100这块区域整个包进去
var node = $act.selector().regionInside(0, 0, 100, 100).findFirst();
if (node != null) {
    log("找到包住该区域的大容器");
}
```


### multiLine(able)

> 加条件：只要“是不是多行文本”这个属性符合要求的节点。
> 
> able 填 true 只找多行文字；填 false 找单行文字。

- 参数 : able {boolean} true 只要多行文本；false 只要单行
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要多行文本节点里，第一个
var node = $act.selector().multiLine(true).findFirst();
if (node != null) {
    log("找到一个多行文本");
}
```


### drawOrder(order)

> 加条件：只找“绘制顺序”正好等于指定数字的节点。
> 
> 绘制顺序数字越小越先画。一般用来在几个重叠节点里区分谁在上谁在下，平时很少用。

- 参数 : order {int} 要匹配的绘制顺序数字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只要绘制顺序为 1 的节点
var node = $act.selector().drawOrder(1).findFirst();
if (node != null) {
    log("找到了");
}
```


### desc(desc)

> 加条件：只要“内容描述”和给定文字完全一模一样的节点。
> 
> 内容描述（desc）是给图标、图片按钮写的说明文字，比如“返回箭头”。这里要求一字不差地相等。

- 参数 : desc {String} 要求完全相等的内容描述文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找内容描述正好是“登录按钮”的节点
var node = $act.selector().desc("登录按钮").findFirst();
if (node != null) {
    node.click();
}
```


### descNotNull(notNull)

> 加条件：只筛选“有没有内容描述”的节点。
> 
> notNull 填 true 时，只保留带内容描述的节点（描述不为空）；填 false 时只要没描述的。

- 参数 : notNull {boolean} true 只要有内容描述的；false 只要没有的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.6


```javascript
//只要带内容描述的节点里，第一个
var node = $act.selector().descNotNull(true).findFirst();
if (node != null) {
    log("它的描述是：" + node.desc);
}
```


### descHas(desc)

> 加条件：只要“内容描述里包含了某段文字”的节点。
> 
> 不要求完全相等，只要描述文字里出现了你给的这串字就算。比精确匹配更宽松。

- 参数 : desc {String} 内容描述里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找内容描述里含有“登录”两个字的节点
var node = $act.selector().descHas("登录").findFirst();
if (node != null) {
    log("找到了：" + node.desc);
}
```


### descStart(desc)

> 加条件：只要“内容描述是以某段文字开头”的节点。
> 
> 比如描述是“登录按钮”，用 descStart("登录") 就能匹配上。

- 参数 : desc {String} 内容描述开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找内容描述以“登录”开头的节点
var node = $act.selector().descStart("登录").findFirst();
if (node != null) {
    log("找到了：" + node.desc);
}
```


### descEnd(desc)

> 加条件：只要“内容描述是以某段文字结尾”的节点。
> 
> 比如描述是“返回箭头”，用 descEnd("箭头") 就能匹配上。

- 参数 : desc {String} 内容描述结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找内容描述以“按钮”结尾的节点
var node = $act.selector().descEnd("按钮").findFirst();
if (node != null) {
    log("找到了：" + node.desc);
}
```


### descMatch(regex)

> 加条件：只要“内容描述符合某个正则表达式”的节点。
> 
> 正则是一种更灵活的文字匹配规则，用符号表示“任意字、几个字”等。小白一般用不到；
> 比如 ".*登录.*" 表示描述里任意位置出现“登录”即可。

- 参数 : regex {String} 正则表达式，用来匹配内容描述
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.8


```javascript
//找内容描述里含有“登录”二字的节点（.* 表示前后任意字符）
var node = $act.selector().descMatch(".*登录.*").findFirst();
if (node != null) {
    log("找到了：" + node.desc);
}
```


### stateDesc(stateDesc)

> 加条件：只要“状态描述”和给定文字完全一模一样的节点（仅安卓 11+ 有效）。
> 
> 状态描述用来表示控件当前状态，比如开关是“开”还是“关”。这里要求一字不差地相等。

- 参数 : stateDesc {String} 要求完全相等的状态描述文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.9.5


```javascript
//找状态描述正好是“已开启”的节点
var node = $act.selector().stateDesc("已开启").findFirst();
if (node != null) {
    log("找到了");
}
```


### stateDescNotNull(notNull)

> 加条件：只筛选“有没有状态描述”的节点（仅安卓 11+ 有效）。
> 
> notNull 填 true 只保留带状态描述的；填 false 只保留没有状态描述的。

- 参数 : notNull {boolean} true 只要有状态描述的；false 只要没有的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.9.5


```javascript
//只要带状态描述的节点里，第一个
var node = $act.selector().stateDescNotNull(true).findFirst();
if (node != null) {
    log("状态描述：" + node.stateDesc);
}
```


### stateDescHas(desc)

> 加条件：只要“状态描述里包含了某段文字”的节点（仅安卓 11+ 有效）。

- 参数 : desc {String} 状态描述里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.9.5


```javascript
//找状态描述里含有“开启”二字的节点
var node = $act.selector().stateDescHas("开启").findFirst();
if (node != null) {
    log("找到了：" + node.stateDesc);
}
```


### stateDescStart(descStart)

> 加条件：只要“状态描述是以某段文字开头”的节点（仅安卓 11+ 有效）。

- 参数 : descStart {String} 状态描述开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.9.5


```javascript
//找状态描述以“已”开头的节点
var node = $act.selector().stateDescStart("已").findFirst();
if (node != null) {
    log("找到了：" + node.stateDesc);
}
```


### stateDescEnd(descEnd)

> 加条件：只要“状态描述是以某段文字结尾”的节点（仅安卓 11+ 有效）。

- 参数 : descEnd {String} 状态描述结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.9.5


```javascript
//找状态描述以“闭”结尾的节点
var node = $act.selector().stateDescEnd("闭").findFirst();
if (node != null) {
    log("找到了：" + node.stateDesc);
}
```


### stateDescMatch(regex)

> 加条件：只要“状态描述符合某个正则表达式”的节点（仅安卓 11+ 有效）。

- 参数 : regex {String} 正则表达式，用来匹配状态描述
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.9.5


```javascript
//找状态描述里含有“开启”二字的节点（.* 表示前后任意字符）
var node = $act.selector().stateDescMatch(".*开启.*").findFirst();
if (node != null) {
    log("找到了：" + node.stateDesc);
}
```


### windowId(id)

> 加条件：只找“属于指定窗口”的节点。
> 
> 屏幕上可能叠着多个窗口（主界面、弹窗），这里用窗口编号限定只在某个窗口里找。

- 参数 : id {int} 要限定的窗口编号
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只在窗口编号为 1 的窗口里找节点
var node = $act.selector().windowId(1).findFirst();
if (node != null) {
    log("找到了");
}
```


### id(id)

> 加条件：只要“资源 id”和给定文字完全一模一样的节点。
> 
> 资源 id 形如 com.example.app:id/btn_login，是开发者给控件起的固定编号，比靠文字找更稳。
> 这里要求完全相等。

- 参数 : id {String} 要求完全相等的资源 id
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找资源 id 正好是 com.example.app:id/btn_login 的节点
var node = $act.selector().id("com.example.app:id/btn_login").findFirst();
if (node != null) {
    node.click();
}
```


### idNotNull(notNull)

> 加条件：只筛选“有没有资源 id”的节点。
> 
> notNull 填 true 只保留带资源 id 的；填 false 只保留没有 id 的。

- 参数 : notNull {boolean} true 只要有资源 id 的；false 只要没有的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.6


```javascript
//只要带资源 id 的节点里，第一个
var node = $act.selector().idNotNull(true).findFirst();
if (node != null) {
    log("资源 id：" + node.id);
}
```


### idHas(id)

> 加条件：只要“资源 id 里包含了某段文字”的节点。
> 
> 不要求 id 完全相等，只要 id 里出现了你给的这串字就算，比如 id 里含 "btn_login"。

- 参数 : id {String} 资源 id 里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找资源 id 里含有 "btn_login" 的节点
var node = $act.selector().idHas("btn_login").findFirst();
if (node != null) {
    log("找到了：" + node.id);
}
```


### idStart(id)

> 加条件：只要“资源 id 是以某段文字开头”的节点。

- 参数 : id {String} 资源 id 开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找资源 id 以 "com.example.app:id/btn" 开头的节点
var node = $act.selector().idStart("com.example.app:id/btn").findFirst();
if (node != null) {
    log("找到了：" + node.id);
}
```


### idEnd(id)

> 加条件：只要“资源 id 是以某段文字结尾”的节点。

- 参数 : id {String} 资源 id 结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找资源 id 以 "_login" 结尾的节点
var node = $act.selector().idEnd("_login").findFirst();
if (node != null) {
    log("找到了：" + node.id);
}
```


### idMatch(regex)

> 加条件：只要“资源 id 符合某个正则表达式”的节点。

- 参数 : regex {String} 正则表达式，用来匹配资源 id
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.8


```javascript
//找资源 id 里含有 "login" 的节点（.* 表示前后任意字符）
var node = $act.selector().idMatch(".*login.*").findFirst();
if (node != null) {
    log("找到了：" + node.id);
}
```


### tip(tip)

> 加条件：只要“提示文字”和给定文字完全一模一样的节点。
> 
> 提示文字就是手指长按图标后弹出的那行小说明。这里要求完全相等。

- 参数 : tip {String} 要求完全相等的提示文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找提示文字正好是“删除”的节点
var node = $act.selector().tip("删除").findFirst();
if (node != null) {
    log("找到了");
}
```


### tipNotNull(notNull)

> 加条件：只筛选“有没有提示文字”的节点。
> 
> notNull 填 true 只保留带提示文字的；填 false 只保留没有的。

- 参数 : notNull {boolean} true 只要有提示文字的；false 只要没有的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.6


```javascript
//只要带提示文字的节点里，第一个
var node = $act.selector().tipNotNull(true).findFirst();
if (node != null) {
    log("提示：" + node.tip);
}
```


### tipHas(tip)

> 加条件：只要“提示文字里包含了某段文字”的节点。

- 参数 : tip {String} 提示文字里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找提示文字里含有“删除”的节点
var node = $act.selector().tipHas("删除").findFirst();
if (node != null) {
    log("找到了：" + node.tip);
}
```


### tipStart(tip)

> 加条件：只要“提示文字是以某段文字开头”的节点。

- 参数 : tip {String} 提示文字开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找提示文字以“删除”开头的节点
var node = $act.selector().tipStart("删除").findFirst();
if (node != null) {
    log("找到了：" + node.tip);
}
```


### tipEnd(tip)

> 加条件：只要“提示文字是以某段文字结尾”的节点。

- 参数 : tip {String} 提示文字结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找提示文字以“提示”结尾的节点
var node = $act.selector().tipEnd("提示").findFirst();
if (node != null) {
    log("找到了：" + node.tip);
}
```


### tipMatch(regex)

> 加条件：只要“提示文字符合某个正则表达式”的节点。

- 参数 : regex {String} 正则表达式，用来匹配提示文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.8


```javascript
//找提示文字里含有“删除”的节点（.* 表示前后任意字符）
var node = $act.selector().tipMatch(".*删除.*").findFirst();
if (node != null) {
    log("找到了：" + node.tip);
}
```


### pkg(packageName)

> 加条件：只找“属于指定 App 包名”的节点。
> 
> 包名是每个 App 的唯一身份，比如微信是 com.tencent.mm。限定包名后就只在这个 App 的界面里找，不会跑到别的 App 上去。
> 这里要求包名完全相等。

- 参数 : packageName {String} 要限定的 App 包名，要求完全相等
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只在微信界面里找“发现”两个字
var node = $act.selector().pkg("com.tencent.mm").text("发现").findFirst();
if (node != null) {
    node.click();
}
```


### pkgNotNull(notNull)

> 加条件：只筛选“有没有包名”的节点。
> 
> notNull 填 true 只保留带包名的；填 false 只保留没有的。

- 参数 : notNull {boolean} true 只要有包名的；false 只要没有的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.6


```javascript
//只要带包名的节点里，第一个
var node = $act.selector().pkgNotNull(true).findFirst();
if (node != null) {
    log("包名：" + node.pkg);
}
```


### pkgHas(packageName)

> 加条件：只要“包名里包含了某段文字”的节点。

- 参数 : packageName {String} 包名里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找包名里含有 "tencent" 的节点
var node = $act.selector().pkgHas("tencent").findFirst();
if (node != null) {
    log("包名：" + node.pkg);
}
```


### pkgStart(packageName)

> 加条件：只要“包名是以某段文字开头”的节点。

- 参数 : packageName {String} 包名开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找包名以 "com.tencent" 开头的节点
var node = $act.selector().pkgStart("com.tencent").findFirst();
if (node != null) {
    log("包名：" + node.pkg);
}
```


### pkgEnd(packageName)

> 加条件：只要“包名是以某段文字结尾”的节点。

- 参数 : packageName {String} 包名结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找包名以 ".mm" 结尾的节点
var node = $act.selector().pkgEnd(".mm").findFirst();
if (node != null) {
    log("包名：" + node.pkg);
}
```


### pkgMatch(regex)

> 加条件：只要“包名符合某个正则表达式”的节点。

- 参数 : regex {String} 正则表达式，用来匹配包名
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.8


```javascript
//找包名里含有 "tencent" 的节点（.* 表示前后任意字符）
var node = $act.selector().pkgMatch(".*tencent.*").findFirst();
if (node != null) {
    log("包名：" + node.pkg);
}
```


### cls(className)

> 加条件：只要“控件类名”和给定文字完全一模一样的节点。
> 
> 类名表示这是哪种控件，比如 android.widget.Button（按钮）、android.widget.EditText（输入框）。这里要求完全相等。

- 参数 : className {String} 要求完全相等的控件类名
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//只找按钮类控件
var node = $act.selector().cls("android.widget.Button").findFirst();
if (node != null) {
    node.click();
}
```


### clsNotNull(notNull)

> 加条件：只筛选“有没有类名”的节点。
> 
> notNull 填 true 只保留带类名的；填 false 只保留没有的。

- 参数 : notNull {boolean} true 只要有类名的；false 只要没有的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.6


```javascript
//只要带类名的节点里，第一个
var node = $act.selector().clsNotNull(true).findFirst();
if (node != null) {
    log("类名：" + node.cls);
}
```


### clsHas(className)

> 加条件：只要“类名里包含了某段文字”的节点。

- 参数 : className {String} 类名里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找类名里含有 "Button" 的节点
var node = $act.selector().clsHas("Button").findFirst();
if (node != null) {
    log("类名：" + node.cls);
}
```


### clsStart(className)

> 加条件：只要“类名是以某段文字开头”的节点。

- 参数 : className {String} 类名开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找类名以 "android.widget" 开头的节点
var node = $act.selector().clsStart("android.widget").findFirst();
if (node != null) {
    log("类名：" + node.cls);
}
```


### clsEnd(className)

> 加条件：只要“类名是以某段文字结尾”的节点。

- 参数 : className {String} 类名结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找类名以 "Button" 结尾的节点
var node = $act.selector().clsEnd("Button").findFirst();
if (node != null) {
    log("类名：" + node.cls);
}
```


### clsMatch(regex)

> 加条件：只要“类名符合某个正则表达式”的节点。

- 参数 : regex {String} 正则表达式，用来匹配类名
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.8


```javascript
//找类名里含有 "Button" 的节点（.* 表示前后任意字符）
var node = $act.selector().clsMatch(".*Button.*").findFirst();
if (node != null) {
    log("类名：" + node.cls);
}
```


### text(text)

> 加条件：只要“显示的文字”和给定文字完全一模一样的节点。
> 
> 这是最常用的查找方式：按钮写的字、标签写的字。这里要求一字不差地相等。

- 参数 : text {String} 要求完全相等的文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找文字正好是“登录”的节点
var node = $act.selector().text("登录").findFirst();
if (node != null) {
    node.click();
}
```


### textNotNull(notNull)

> 加条件：只筛选“有没有文字”的节点。
> 
> notNull 填 true 只保留带文字的；填 false 只保留没有文字的（比如纯图片按钮）。

- 参数 : notNull {boolean} true 只要有文字的；false 只要没有文字的
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.6


```javascript
//只要带文字的节点里，第一个
var node = $act.selector().textNotNull(true).findFirst();
if (node != null) {
    log("文字：" + node.text);
}
```


### textHas(text)

> 加条件：只要“显示的文字里包含了某段文字”的节点。
> 
> 不要求完全相等，只要文字里出现了你给的这串字就算，比精确匹配宽松。

- 参数 : text {String} 文字里需要包含的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找文字里含有“登录”的节点
var node = $act.selector().textHas("登录").findFirst();
if (node != null) {
    log("找到了：" + node.text);
}
```


### textStart(text)

> 加条件：只要“显示的文字是以某段文字开头”的节点。

- 参数 : text {String} 文字开头需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找文字以“登录”开头的节点
var node = $act.selector().textStart("登录").findFirst();
if (node != null) {
    log("找到了：" + node.text);
}
```


### textEnd(text)

> 加条件：只要“显示的文字是以某段文字结尾”的节点。

- 参数 : text {String} 文字结尾需要出现的那段文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//找文字以“登录”结尾的节点
var node = $act.selector().textEnd("登录").findFirst();
if (node != null) {
    log("找到了：" + node.text);
}
```


### textMatch(regex)

> 加条件：只要“显示的文字符合某个正则表达式”的节点。

- 参数 : regex {String} 正则表达式，用来匹配文字
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.6.8


```javascript
//找文字里含有“登录”二字的节点（.* 表示前后任意字符）
var node = $act.selector().textMatch(".*登录.*").findFirst();
if (node != null) {
    log("找到了：" + node.text);
}
```


### or()

> 开启一组新的“或”条件（OR）。
> 
> 平时连续加的条件都是“并且”的关系：既要文字是A，又要是按钮。调用 or() 之后，会另起一组条件，
> 两组之间是“或者”的关系——满足第一组，或者满足第二组，都算匹配。可以多次 or() 加更多组。
> 
> 典型用途：同一个按钮，不同手机上文字可能是“强制停止”或“强行停止”，两组文字条件就用 or() 连起来。

- 返回 : {UiSelector} 返回选择器自身，可继续链式加下一组条件
- 版本 : 1.7.8


```javascript
//找“文字是 登录” 或者 “文字是 登陆” 的任意一个节点
var node = $act.selector()
    .text("登录")   //第一组条件：文字必须是“登录”
    .or()           //开启第二组条件（两组之间是“或者”）
    .text("登陆")   //第二组条件：文字也可以是“登陆”
    .findFirst();
if (node != null) {
    node.click();
}
```


### findAll()

> 立刻在当前屏幕上找一次，把所有符合条件的节点全部取出。
> 
> 它只找一次、不等。拿到的是一个 Node 列表，可以用 for 循环遍历。一个都没有时是空列表。

- 返回 : {Node[]} 所有符合条件的节点列表；一个都没有时是空列表
- 版本 : 1.0.0


```javascript
//找出屏幕上所有文字是“条目”的节点
var list = $act.selector().text("条目").findAll();
for (var i = 0; i < list.size(); i++) { //遍历每一个
    log("第" + i + "个：" + list.get(i).text);
}
```


### find(index)

> 立刻在当前屏幕上找一次，取出第 index 个符合条件的节点。
> 
> 先把符合条件的节点按顺序排好，再取第 index 个（从 0 开始数）。index 超过总数时退而取第一个。
> 一个都没有时返回 null。

- 参数 : index {int} 取第几个，从 0 开始数；超过总数时取第一个
- 返回 : {Node} 第 index 个符合条件的节点；一个都没有时返回 null
- 版本 : 1.0.0


```javascript
//找文字是“条目”的节点，取第 3 个（下标 2）
var node = $act.selector().text("条目").find(2);
if (node != null) {
    log("第三个：" + node.text);
}
```


### findFirst()

> 立刻在当前屏幕上找一次，取出第一个符合条件的节点。
> 
> 它只找一次、不等。找到就返回那个节点，一个都没有时返回 null。

- 返回 : {Node} 第一个符合条件的节点；一个都没有时返回 null
- 版本 : 1.0.0


```javascript
//找文字是“登录”的第一个节点
var node = $act.selector().text("登录").findFirst();
if (node != null) {
    node.click(); //找到了就点它
}
```


### findLast()

> 立刻在当前屏幕上找一次，取出最后一个符合条件的节点。
> 
> 它只找一次、不等。找到就返回排在最后那个节点，一个都没有时返回 null。

- 返回 : {Node} 最后一个符合条件的节点；一个都没有时返回 null
- 版本 : 1.0.0


```javascript
//找文字是“条目”的最后一个节点
var node = $act.selector().text("条目").findLast();
if (node != null) {
    log("最后一个：" + node.text);
}
```


### waitAll()

> 一直等，直到屏幕上出现符合条件的节点，然后把它们全部取出来。
> 
> 和 findAll 不同：它不会只找一次就放弃，而是每隔一小段时间就重新找一次，
> 默认最多重试 120 次、每次间隔 500 毫秒（大约一共等 60 秒）。等这么久还是没有，就返回空列表。

- 返回 : {Node[]} 找到的节点列表；超时仍没有时是空列表
- 版本 : 1.0.0


```javascript
//一直等到“登录”出现，然后取出来
var list = $act.selector().text("登录").waitAll();
if (list.size() > 0) {
    log("终于出现了，一共" + list.size() + "个");
}
```


### waitAll(failCallback)

> 边等边做别的事：在等待出现符合条件的节点时，每找一圈没找到，就执行一次 failCallback 函数。
> 
> 典型用途：等列表加载出新内容时，可以在回调里顺手把列表往上滑一下，做到“边滑边等”。
> 一旦找到了节点就立即返回；超时仍没有则返回空列表。

- 参数 : failCallback {function} 每找一圈都没找到时要执行的函数（可传 null 表示不做任何事）
- 返回 : {Node[]} 找到的节点列表；超时仍没有时是空列表
- 版本 : 1.0.0


```javascript
//一边等“下一条”出现，每一圈没找到就把列表往上滑一下
var list = $act.selector().text("下一条").waitAll(function () {
    log("还没出现，先滑一下");
    var scroller = $act.selector().scrollable(true).findFirst();
    if (scroller != null) {
        scroller.move("up");
    }
});
if (list.size() > 0) {
    log("出现了");
}
```


### wait(index, failCallback)

> 一直等到出现符合条件的节点，再取出第 index 个；等待期间每找一圈没找到就执行一次回调。
> 
> index 从 0 开始数，超过总数时取第一个。一直等到超时仍没有时返回 null。
> failCallback 的作用和 waitAll(回调) 一样：边等边做别的事（比如滑列表）。

- 参数 : index {int} 找到后取第几个，从 0 开始数；超过总数取第一个
- 参数 : failCallback {function} 每找一圈都没找到时要执行的函数（可传 null）
- 返回 : {Node} 第 index 个节点；超时仍没有时返回 null
- 版本 : 1.0.0


```javascript
//边等边滑，等“条目”出现后取第 0 个
var node = $act.selector().text("条目").wait(0, function () {
    log("还没出现，滑一下");
});
if (node != null) {
    log("等到了：" + node.text);
}
```


### wait(index)

> 一直等到出现符合条件的节点，再取出第 index 个。
> 
> index 从 0 开始数，超过总数时取第一个。一直等到超时仍没有时返回 null。

- 参数 : index {int} 找到后取第几个，从 0 开始数；超过总数取第一个
- 返回 : {Node} 第 index 个节点；超时仍没有时返回 null
- 版本 : 1.0.0


```javascript
//一直等“条目”出现，取第 0 个
var node = $act.selector().text("条目").wait(0);
if (node != null) {
    log("等到了：" + node.text);
}
```


### waitFirst()

> 一直等到出现符合条件的节点，再取出第一个。
> 
> 这是最常用的“等节点”写法：自动反复查找，直到它出现或超时，然后取第一个。
> 超时仍没有时返回 null。

- 返回 : {Node} 第一个符合条件的节点；超时仍没有时返回 null
- 版本 : 1.0.0


```javascript
//一直等“登录”出现，然后点它
var node = $act.selector().text("登录").waitFirst();
if (node != null) {
    node.click();
}
```


### waitFirst(failCallback)

> 一直等到出现符合条件的节点再取第一个；等待期间每找一圈没找到就执行一次回调。
> 
> 比如边滑列表边等“下一条”出现。一旦找到就返回第一个；超时仍没有则返回 null。

- 参数 : failCallback {function} 每找一圈都没找到时要执行的函数（可传 null）
- 返回 : {Node} 第一个符合条件的节点；超时仍没有时返回 null
- 版本 : 1.0.0


```javascript
//边等边滑，等“下一条”出现后取第一个
var node = $act.selector().text("下一条").waitFirst(function () {
    log("还没出现，滑一下");
});
if (node != null) {
    log("等到了");
}
```


### waitLast()

> 一直等到出现符合条件的节点，再取出最后一个。
> 
> 自动反复查找，直到它出现或超时，然后取排在最后的那个。超时仍没有时返回 null。

- 返回 : {Node} 最后一个符合条件的节点；超时仍没有时返回 null
- 版本 : 1.0.0


```javascript
//一直等“条目”出现，取最后一个
var node = $act.selector().text("条目").waitLast();
if (node != null) {
    log("等到了最后一个：" + node.text);
}
```


### waitLast(failCallback)

> 一直等到出现符合条件的节点再取最后一个；等待期间每找一圈没找到就执行一次回调。

- 参数 : failCallback {function} 每找一圈都没找到时要执行的函数（可传 null）
- 返回 : {Node} 最后一个符合条件的节点；超时仍没有时返回 null
- 版本 : 1.0.0


```javascript
//边等边滑，等“条目”出现后取最后一个
var node = $act.selector().text("条目").waitLast(function () {
    log("还没出现，滑一下");
});
if (node != null) {
    log("等到了最后一个");
}
```


### setWaitTime(times)

> 设置“等待类方法”最多重试找多少轮。
> 
> waitFirst、waitLast、waitAll 这些方法会反复找节点。这个方法决定一共最多找多少轮，默认是 120 轮。
> 比如填 10，就最多找 10 轮就放弃。要在调用 wait 系列之前先设置。

- 参数 : times {int} 最多重试多少轮
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//改成最多找 10 轮，然后再去等“登录”
var node = $act.selector().setWaitTime(10).text("登录").waitFirst();
if (node != null) {
    node.click();
}
```


### setWaitDur(times)

> 设置“等待类方法”每两轮之间间隔多少毫秒。
> 
> 每找一圈没找到，就先歇一会儿再找下一圈。这个方法设置歇多久，默认 500 毫秒（半秒）。
> 填 0 表示不歇，一直高频找。要在调用 wait 系列之前先设置。

- 参数 : times {int} 每轮之间停顿的毫秒数（1000 = 1 秒）
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.0.0


```javascript
//改成每圈间隔 1000 毫秒（1秒），然后再去等“登录”
var node = $act.selector().setWaitDur(1000).text("登录").waitFirst();
if (node != null) {
    node.click();
}
```


### setMainWindow(yes)

> 设置是否只在“主窗口”里找节点。
> 
> 屏幕上可能叠着好几个窗口。填 true 时，只扫描应用的主窗口，忽略悬浮窗、输入法等其他窗口里的节点；
> 填 false 则扫描全部窗口。默认扫描全部。

- 参数 : yes {boolean} true 只找主窗口；false 找全部窗口
- 返回 : {UiSelector} 返回选择器自身，可继续链式加条件
- 版本 : 1.7.8


```javascript
//只在主窗口里找“登录”，忽略其他悬浮层
var node = $act.selector().setMainWindow(true).text("登录").findFirst();
if (node != null) {
    node.click();
}
```


