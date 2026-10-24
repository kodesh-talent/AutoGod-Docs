# Node - 节点信息

- 更新时间:2026-10-22 10:55:44

> 界面节点（也叫“控件”）对象。
> 
> 手机屏幕上每一个能看到、能点、能输入的东西——比如一个按钮、一段文字、一个输入框、一个图标——
> 在安卓系统里都对应着一个“界面节点”。本应用把这些系统节点封装成了 Node 对象：
> 你可以读取它显示了什么文字、在屏幕的哪个位置、能不能点，还能直接对它执行点击、滑动、输入文字等操作。
> 
> 新手提示：Node 对象一般不用你自己 new，而是先用选择器 $act.selector() 按条件（文字、资源id、类名等）筛出节点，
> 再用 findFirst、findAll 等方法拿到它；找不到时拿到的是 null，使用前一定要先判断 null。



```javascript
//第一步：创建一个选择器，准备去屏幕上找控件
var selector = $act.selector();
//第二步：给选择器加条件——只要按钮文字是“登录”的节点
selector = selector.text("登录").cls("android.widget.Button");
//第三步：在当前屏幕上找到符合条件的第一个节点
var node = selector.findFirst();
//第四步：判断到底找没找到（没找到时 node 为 null）
if (node != null) {
    node.draw(); //把这个节点在屏幕上的位置画一个框出来，方便确认找对了没有
}
```




### const {Integer} x;

> 节点左上角的横坐标 x（整数，单位：像素）。
> 
> 表示这个节点从屏幕最左边往右数的位置，数字越大越靠右。
> 注意这是节点“左上角”的位置，不是中心点；要点击一般用中心点 cx、cy。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到“登录”按钮节点
if (node != null) {
    log("节点左上角距离左边：" + node.x + " 像素"); //直接读 x 字段
}
```


### const {Integer} y;

> 节点左上角的纵坐标 y（整数，单位：像素）。
> 
> 表示这个节点从屏幕最上边往下数的位置，数字越大越靠下。
> 注意这是节点“左上角”的位置，不是中心点；要点击一般用中心点 cx、cy。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到“登录”按钮节点
if (node != null) {
    log("节点左上角距离上边：" + node.y + " 像素"); //直接读 y 字段
}
```


### const {Integer} w;

> 节点的宽度 w（整数，单位：像素）。
> 
> 表示这个节点在屏幕上占了多宽，从左到右量。数字越大越宽。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("节点宽度：" + node.w + " 像素"); //直接读 w 字段
}
```


### const {Integer} h;

> 节点的高度 h（整数，单位：像素）。
> 
> 表示这个节点在屏幕上占了多高，从上到下量。数字越大越高。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("节点高度：" + node.h + " 像素"); //直接读 h 字段
}
```


### const {Integer} cx;

> 节点中心点的横坐标 cx（整数，单位：像素）。
> 
> 这是节点正中间那个点的水平位置。要点击、长按这个节点时，系统默认就是点在 (cx, cy) 这个中心点上，
> 所以它是最常用的坐标。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("节点中心横坐标：" + node.cx); //直接读 cx 字段
}
```


### const {Integer} cy;

> 节点中心点的纵坐标 cy（整数，单位：像素）。
> 
> 这是节点正中间那个点的垂直位置。要点击、长按这个节点时，系统默认就是点在 (cx, cy) 这个中心点上。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("节点中心纵坐标：" + node.cy); //直接读 cy 字段
}
```


### const {Boolean} clickable;

> 这个节点能不能被点击（true 能点，false 不能点）。
> 
> 按钮、可点的文字一般是 true。如果你想点它之前先确认一下，可以读这个字段。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("能不能点：" + node.clickable); //输出 true 或 false
}
```


### const {Boolean} longClickable;

> 这个节点能不能被长按（true 能长按，false 不能）。
> 
> 长按通常用来弹出菜单（比如长按图标卸载、长按文字复制）。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("能不能长按：" + node.longClickable); //输出 true 或 false
}
```


### const {Boolean} enabled;

> 这个节点现在是否处于“可用”状态（true 可用，false 灰掉不可用）。
> 
> 灰掉的按钮一般是 false，这时候点了也没反应。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("是否可用：" + node.enabled); //输出 true 或 false
}
```


### const {Boolean} selected;

> 这个节点当前是否被“选中”（true 选中，false 未选中）。
> 
> 比如标签页里高亮的那一项、列表里被选中的那一行，通常就是 true。


```javascript
var node = $act.selector().text("未读").findFirst(); //找到节点
if (node != null) {
    log("是否选中：" + node.selected); //输出 true 或 false
}
```


### const {Boolean} scrollable;

> 这个节点能不能滚动（true 能上下左右滑动列表，false 不能）。
> 
> 聊天记录、商品列表、设置清单这种长列表容器一般是 true。


```javascript
var node = $act.selector().cls("android.widget.ListView").findFirst(); //找到列表
if (node != null) {
    log("能不能滚动：" + node.scrollable); //输出 true 或 false
}
```


### const {Boolean} checkable;

> 这个节点是不是一个“可勾选”的控件（true 是复选框/开关类，false 不是）。
> 
> 注意它只表示“允不允许被勾选”，不代表“当前有没有勾上”；当前勾没勾要看 checked 字段。


```javascript
var node = $act.selector().cls("android.widget.CheckBox").findFirst(); //找到复选框
if (node != null) {
    log("是否可勾选：" + node.checkable); //输出 true 或 false
}
```


### const {Boolean} checked;

> 这个节点当前有没有被勾上（true 已勾选，false 未勾选）。
> 
> 只有本身是复选框、开关这类可勾选控件（checkable 为 true）时，这个字段才有意义。


```javascript
var node = $act.selector().cls("android.widget.CheckBox").findFirst(); //找到复选框
if (node != null) {
    log("当前是否勾上：" + node.checked); //输出 true 或 false
}
```


### const {Boolean} visible;

> 这个节点现在对用户是否可见（true 看得见，false 被遮住或看不见）。
> 
> 屏幕上看不到的节点一般点了也没用，操作前建议确认这个字段为 true。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("是否可见：" + node.visible); //输出 true 或 false
}
```


### const {int[]} region;

> 节点在屏幕上占的整块区域（一个整数数组，格式为 [左边, 上边, 宽度, 高度]）。
> 
> 数组一共 4 个数字：第 1 个是节点左边离屏幕左边缘的距离，第 2 个是上边离屏幕上边缘的距离，
> 第 3 个是宽度，第 4 个是高度，单位都是像素。它和 x、y、w、h 表示的是同一块区域，只是打包成了一个数组。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var r = node.region;                //取出区域数组
    log("左=" + r[0] + " 上=" + r[1] + " 宽=" + r[2] + " 高=" + r[3]);
}
```


### const {Boolean} multiLine;

> 这个文字控件是不是多行文本（true 多行，false 单行）。
> 
> 一个长输入框、一段多行说明文字通常是 true；单行输入框是 false。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("是否多行：" + node.multiLine); //输出 true 或 false
}
```


### const {Integer} drawOrder;

> 这个节点在屏幕上的“绘制顺序”（整数，数字越小越先绘制）。
> 
> 当几个节点位置重叠时，绘制顺序靠后的会盖在上面。一般用来判断谁在上谁在下，平时很少用到。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("绘制顺序：" + node.drawOrder); //输出一个整数
}
```


### const {String} desc;

> 这个节点的“内容描述”文字（字符串）。
> 
> 很多图标、图片按钮本身没有文字，但开发者会给它写一段描述（比如“返回箭头”），读屏软件就是靠它念出来的。
> 找不到文字、只能靠图标认按钮时，常常可以用它。没有描述时为 null。


```javascript
var node = $act.selector().desc("返回").findFirst(); //按描述找节点
if (node != null) {
    log("描述是：" + node.desc); //输出这段描述文字
}
```


### const {String} stateDesc;

> 这个节点的“状态描述”文字（字符串），仅安卓 11（API 30）及以上系统才有。
> 
> 它用来描述控件当前的状态，比如开关是“开”还是“关”、进度到了多少。老系统上这个字段会是 null。


```javascript
var node = $act.selector().text("音量").findFirst(); //找到节点
if (node != null) {
    log("状态描述：" + node.stateDesc); //输出状态文字，老系统可能是 null
}
```


### const {String} tip;

> 这个节点的“提示”文字（字符串），也就是手指长按图标后弹出的那行小提示。
> 
> 比如把手指停在某个按钮上弹出的“这是删除按钮”。没有提示时为 null。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("提示文字：" + node.tip); //输出提示，没有则是 null
}
```


### const {String} id;

> 这个节点的“资源 id”（字符串），是开发者给控件起的唯一编号。
> 
> 它长这样：com.xxx.xxx:id/button_login。同一个界面里 id 通常是固定不变的，
> 比靠文字查找更稳定（文字可能随语言变化）。没有 id 时为 null。


```javascript
var node = $act.selector().id("com.example.app:id/btn_login").findFirst(); //按 id 找
if (node != null) {
    log("资源id：" + node.id); //输出完整 id 字符串
}
```


### const {String} pkg;

> 这个节点所属应用的“包名”（字符串）。
> 
> 包名是每个 App 的唯一身份，比如微信是 com.tencent.mm。可以用它判断这个节点属于哪个 App。


```javascript
var node = $act.selector().text("微信").findFirst(); //找到节点
if (node != null) {
    log("所属包名：" + node.pkg); //输出例如 com.tencent.mm
}
```


### const {String} cls;

> 这个节点的“类名”（字符串），表示它是哪种安卓控件。
> 
> 常见取值：android.widget.Button（按钮）、android.widget.TextView（文字）、
> android.widget.EditText（输入框）、android.widget.ImageView（图片）等。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("控件类型：" + node.cls); //输出例如 android.widget.Button
}
```


### const {String} text;

> 这个节点上显示的“文本内容”（字符串）。
> 
> 按钮上写的字、标签上的字、输入框里已经填的字，都存在这里。没有文字时为 null。
> 这是最常用的查找条件之一。


```javascript
var node = $act.selector().text("登录").findFirst(); //按文字找节点
if (node != null) {
    log("它显示的文字是：" + node.text); //输出“登录”
}
```


### const {Integer} windowId;

> 这个节点所在“窗口”的编号（整数）。
> 
> 手机屏幕上可能同时叠着好几个窗口（比如主界面、弹窗、状态栏），每个窗口有自己的编号。
> 一般用来区分节点属于哪个窗口，平时很少直接用到。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("所在窗口编号：" + node.windowId); //输出一个整数
}
```


### const {AccessibilityNodeInfo} node;

> 安卓系统原生的节点对象（AccessibilityNodeInfo），属于“底层原始数据”。
> 
> 上面这些字段（文字、位置、能不能点等），原本都是从这个原始对象里读出来的。
> 普通用户用不到它；只有当本封装没提供、而你又需要安卓系统更底层的能力时，才通过 getNode() 拿到它自己操作。


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var raw = node.getNode();            //拿到安卓原生节点对象
    var count = raw.getChildCount();     //调用原生对象上的方法，比如读子节点个数
    log("子节点个数：" + count);
}
```


### parent()

> 获取这个节点的“父节点”（它上一层的那个容器节点）。
> 
> 界面是一层套一层的：一个按钮外面套着布局，布局外面又套着更大的布局。
> 这个方法就是往外层找上一层。拿到后可以继续读它的位置、文字，或再点它。
> 如果已经是最外层（没有父节点了），返回 null。

- 返回 : {Node} 父节点对象；没有父节点或当前节点为空时返回 null
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //先找到“登录”按钮
if (node != null) {
    var p = node.parent();   //往上找它的父节点
    if (p != null) {
        log("父节点的文字：" + p.text); //读父节点的文字
    }
}
```


### childNum()

> 数一下这个节点下面直接“有几个子节点”。
> 
> 一个布局里面往往塞着好几个按钮、文字，这个方法就告诉你它直接包含几个孩子节点。
> 它只数“直接子节点”，不数孙子节点。当前节点为空时返回 0。

- 返回 : {int} 直接子节点的个数；当前节点为空时返回 0
- 版本 : 1.4.3


```javascript
var node = $act.selector().cls("android.widget.LinearLayout").findFirst(); //找一个布局
if (node != null) {
    var n = node.childNum(); //数它直接有几个子节点
    log("直接子节点个数：" + n);
}
```


### childs()

> 取出这个节点下面所有“直接子节点”，打包成一个列表。
> 
> 上一个 childNum() 只告诉你个数，这个方法直接把这些孩子节点一个个拿出来。
> 拿到列表后可以用 for 循环遍历，逐个读取文字、点击等。没有子节点时返回一个空列表。

- 返回 : {Node[]} 直接子节点组成的列表（Node 列表）；没有子节点时是空列表
- 版本 : 1.4.3


```javascript
var node = $act.selector().cls("android.widget.LinearLayout").findFirst(); //找一个布局
if (node != null) {
    var list = node.childs();       //取出所有直接子节点列表
    for (var i = 0; i < list.size(); i++) { //遍历每一个子节点
        log("第" + i + "个子节点文字：" + list.get(i).text);
    }
}
```


### child(index)

> 按编号取出这个节点下面“指定的那一个直接子节点”。
> 
> 孩子节点是按顺序排好的：第 1 个编号是 0，第 2 个是 1，依此类推。
> 比如 child(0) 就是要第一个孩子。编号越界、或取不到时返回 null。

- 参数 : index {int} 要取的第几个子节点，从 0 开始数
- 返回 : {Node} 对应的子节点；取不到时返回 null
- 版本 : 1.4.3


```javascript
var node = $act.selector().cls("android.widget.LinearLayout").findFirst(); //找一个布局
if (node != null) {
    var c = node.child(0);  //取出第 1 个直接子节点
    if (c != null) {
        log("第一个子节点文字：" + c.text);
    }
}
```


### getX()

> 读取节点左上角的横坐标 x（单位：像素）。
> 
> 作用和直接写 node.x 完全一样，这是“面向对象”的标准写法。

- 返回 : {int} 节点左上角的横坐标
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var v = node.getX();      //读左上角横坐标
    log("左上角 x：" + v);
}
```


### getY()

> 读取节点左上角的纵坐标 y（单位：像素）。
> 
> 作用和直接写 node.y 完全一样。

- 返回 : {int} 节点左上角的纵坐标
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var v = node.getY();      //读左上角纵坐标
    log("左上角 y：" + v);
}
```


### getW()

> 读取节点的宽度 w（单位：像素）。
> 
> 作用和直接写 node.w 完全一样。

- 返回 : {int} 节点的宽度
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var v = node.getW();      //读宽度
    log("宽度：" + v);
}
```


### getH()

> 读取节点的高度 h（单位：像素）。
> 
> 作用和直接写 node.h 完全一样。

- 返回 : {int} 节点的高度
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var v = node.getH();      //读高度
    log("高度：" + v);
}
```


### getCx()

> 读取节点中心点的横坐标 cx（单位：像素）。
> 
> 这是点击节点时真正会按到的那个点的水平坐标。作用和直接写 node.cx 完全一样。

- 返回 : {int} 节点中心点的横坐标
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var v = node.getCx();     //读中心点横坐标
    log("中心点 x：" + v);
}
```


### getCy()

> 读取节点中心点的纵坐标 cy（单位：像素）。
> 
> 这是点击节点时真正会按到的那个点的垂直坐标。作用和直接写 node.cy 完全一样。

- 返回 : {int} 节点中心点的纵坐标
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var v = node.getCy();     //读中心点纵坐标
    log("中心点 y：" + v);
}
```


### getClickable()

> 读取这个节点能不能被点击（true 能点，false 不能点）。
> 
> 作用和直接写 node.clickable 完全一样。

- 返回 : {boolean} true 表示可点击，false 表示不可点击
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("能不能点：" + node.getClickable());
}
```


### getLongClickable()

> 读取这个节点能不能被长按（true 能长按，false 不能）。
> 
> 作用和直接写 node.longClickable 完全一样。

- 返回 : {boolean} true 表示可长按，false 表示不可长按
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("能不能长按：" + node.getLongClickable());
}
```


### getEnabled()

> 读取这个节点现在是否“可用”（true 可用，false 灰掉不可用）。
> 
> 作用和直接写 node.enabled 完全一样。

- 返回 : {boolean} true 表示可用，false 表示不可用（灰掉）
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("是否可用：" + node.getEnabled());
}
```


### getSelected()

> 读取这个节点当前是否“被选中”（true 选中，false 未选中）。
> 
> 作用和直接写 node.selected 完全一样。

- 返回 : {boolean} true 表示已选中，false 表示未选中
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("未读").findFirst(); //找到节点
if (node != null) {
    log("是否选中：" + node.getSelected());
}
```


### getScrollable()

> 读取这个节点能不能“滚动”（true 能上下左右滑列表，false 不能）。
> 
> 作用和直接写 node.scrollable 完全一样。

- 返回 : {boolean} true 表示可滚动，false 表示不可滚动
- 版本 : 1.3.6


```javascript
var node = $act.selector().cls("android.widget.ListView").findFirst(); //找列表
if (node != null) {
    log("能不能滚动：" + node.getScrollable());
}
```


### getCheckable()

> 读取这个节点是不是“可勾选”控件（true 是复选框/开关类，false 不是）。
> 
> 作用和直接写 node.checkable 完全一样。注意它只表示允不允许勾，当前勾没勾看 getChecked()。

- 返回 : {boolean} true 表示是可勾选控件，false 不是
- 版本 : 1.3.6


```javascript
var node = $act.selector().cls("android.widget.CheckBox").findFirst(); //找复选框
if (node != null) {
    log("是否可勾选：" + node.getCheckable());
}
```


### getChecked()

> 读取这个节点当前有没有“被勾上”（true 已勾选，false 未勾选）。
> 
> 作用和直接写 node.checked 完全一样。

- 返回 : {boolean} true 表示已勾选，false 表示未勾选
- 版本 : 1.3.6


```javascript
var node = $act.selector().cls("android.widget.CheckBox").findFirst(); //找复选框
if (node != null) {
    log("当前是否勾上：" + node.getChecked());
}
```


### getRegion()

> 读取节点在屏幕上占的整块区域，格式为 [左边, 上边, 宽度, 高度]（整数数组，单位：像素）。
> 
> 作用和直接写 node.region 完全一样。

- 返回 : {int[]} 长度为 4 的整数数组 [左边, 上边, 宽度, 高度]
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var r = node.getRegion(); //取出区域数组
    log("左=" + r[0] + " 上=" + r[1] + " 宽=" + r[2] + " 高=" + r[3]);
}
```


### getMultiLine()

> 读取这个文字控件是不是“多行文本”（true 多行，false 单行）。
> 
> 作用和直接写 node.multiLine 完全一样。

- 返回 : {boolean} true 表示多行文本，false 表示单行
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("是否多行：" + node.getMultiLine());
}
```


### getDrawOrder()

> 读取这个节点的“绘制顺序”（整数，数字越小越先绘制）。
> 
> 作用和直接写 node.drawOrder 完全一样。节点重叠时用来判断谁在上谁在下，平时很少用。

- 返回 : {int} 绘制顺序的整数值
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("绘制顺序：" + node.getDrawOrder());
}
```


### getTip()

> 读取这个节点的“提示”文字（字符串）。
> 
> 作用和直接写 node.tip 完全一样。没有提示时返回 null。

- 返回 : {String} 提示文字；没有时返回 null
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("提示文字：" + node.getTip()); //没有提示时为 null
}
```


### getDesc()

> 读取这个节点的“内容描述”文字（字符串）。
> 
> 作用和直接写 node.desc 完全一样。图标、图片按钮常用它来描述自己；没有描述时返回 null。

- 返回 : {String} 内容描述文字；没有时返回 null
- 版本 : 1.3.6


```javascript
var node = $act.selector().desc("返回").findFirst(); //按描述找节点
if (node != null) {
    log("描述是：" + node.getDesc());
}
```


### getId()

> 读取这个节点的“资源 id”（字符串）。
> 
> 作用和直接写 node.id 完全一样。形如 com.xxx.xxx:id/button_login；没有 id 时返回 null。

- 返回 : {String} 资源 id 字符串；没有时返回 null
- 版本 : 1.3.6


```javascript
var node = $act.selector().id("com.example.app:id/btn_login").findFirst(); //按 id 找
if (node != null) {
    log("资源id：" + node.getId());
}
```


### getPkg()

> 读取这个节点所属应用的“包名”（字符串）。
> 
> 作用和直接写 node.pkg 完全一样。比如微信就是 com.tencent.mm。

- 返回 : {String} 包名字符串
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("微信").findFirst(); //找到节点
if (node != null) {
    log("所属包名：" + node.getPkg());
}
```


### getCls()

> 读取这个节点的“类名”（字符串），表示它是哪种安卓控件。
> 
> 作用和直接写 node.cls 完全一样。例如 android.widget.Button、android.widget.EditText 等。

- 返回 : {String} 类名字符串
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("控件类型：" + node.getCls());
}
```


### getText()

> 读取这个节点上显示的“文本内容”（字符串）。
> 
> 作用和直接写 node.text 完全一样。没有文字时返回 null。

- 返回 : {String} 节点上的文本；没有时返回 null
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //按文字找节点
if (node != null) {
    log("它显示的文字是：" + node.getText());
}
```


### getWindowId()

> 读取这个节点所在“窗口”的编号（整数）。
> 
> 作用和直接写 node.windowId 完全一样。用来区分节点属于哪个窗口（主界面、弹窗等），平时很少用。

- 返回 : {int} 窗口编号
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    log("所在窗口编号：" + node.getWindowId());
}
```


### getNode()

> 拿到安卓系统原生的节点对象（AccessibilityNodeInfo），属于底层原始数据。
> 
> 上面这些字段和方法，原本都是从这个原生对象里读出来、包出来的。
> 普通用户用不到；只有当本封装没提供、而你又需要安卓系统更底层的能力时，才用它自己操作。

- 返回 : {AccessibilityNodeInfo} 安卓原生节点对象；当前节点为空时可能为 null
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    var raw = node.getNode();        //拿到安卓原生节点对象
    var count = raw.getChildCount(); //调用原生对象的方法，例如数子节点个数
    log("子节点个数：" + count);
}
```


### click()

> 点击这个节点（点在它的正中心）。
> 
> 相当于你的手指在这个按钮/文字的正中间按一下立刻抬起。这是最常用的点击方式，无需自己算坐标。

- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到“登录”按钮
if (node != null) {
    node.click(); //直接点它正中心，就像人手点了一下
}
```


### click(useAct)

> 点击这个节点，并指定用哪种方式点击。
> 
> 本方法和上面无参数的 click() 效果一样，只是多了一个开关：
> useAct 填 true 时，走安卓无障碍接口直接让节点自己被点（不需要悬浮窗权限，更快更隐蔽）；
> 填 false 时，走模拟人手在屏幕坐标上点一下（需要悬浮窗/触屏权限，和真人手指点屏幕一样）。

- 参数 : useAct {boolean} true 用无障碍接口点击；false 用模拟手势点屏幕坐标
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到“登录”按钮
if (node != null) {
    node.click(true); //用无障碍方式点它正中心
}
```


### click(px, py)

> 在这个节点“中心点旁边偏移一点”的位置点击。
> 
> 有时候不想点正中心（比如按钮中间有个图标会误触），就用这两个参数做偏移：
> 最终点的位置 = 节点中心横坐标 + px，节点中心纵坐标 + py。正数往右/往下偏，负数往左/往上偏，单位像素。

- 参数 : px {int} 相对中心点，水平方向的偏移像素（正数往右，负数往左）
- 参数 : py {int} 相对中心点，垂直方向的偏移像素（正数往下，负数往上）
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到按钮
if (node != null) {
    node.click(10, 0); //在中心点右边 10 像素的地方点一下
}
```


### press()

> 长按这个节点（按住它的正中心一小段时间再松开）。
> 
> 长按通常用来弹出菜单，比如长按应用图标弹出卸载、长按文字弹出复制。时长用系统默认值。

- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    node.press(); //长按它正中心
}
```


### press(dur)

> 长按这个节点，并自己指定按住多久（单位：毫秒）。
> 
> 1000 毫秒等于 1 秒。比如想按得久一点就传 2000。

- 参数 : dur {int} 按住的时长，单位毫秒（1000 = 1 秒）
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    node.press(1500); //按住中心 1.5 秒再松开
}
```


### press(px, py)

> 在这个节点“中心点旁边偏移一点”的位置长按（时长用系统默认值）。
> 
> 最终按住的位置 = 节点中心横坐标 + px，节点中心纵坐标 + py。正数往右/往下偏，负数往左/往上偏。

- 参数 : px {int} 相对中心点，水平方向的偏移像素（正数往右，负数往左）
- 参数 : py {int} 相对中心点，垂直方向的偏移像素（正数往下，负数往上）
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    node.press(0, 20); //在中心往下 20 像素处长按
}
```


### press(px, py, dur)

> 在这个节点“中心点旁边偏移一点”的位置长按，并自己指定按住多久。
> 
> 这是上面两个的组合：既能偏移位置，又能自定义时长。
> 最终按住位置 = 节点中心 + (px, py)，按住 dur 毫秒后松开。

- 参数 : px {int} 相对中心点，水平方向的偏移像素（正数往右，负数往左）
- 参数 : py {int} 相对中心点，垂直方向的偏移像素（正数往下，负数往上）
- 参数 : dur {int} 按住的时长，单位毫秒（1000 = 1 秒）
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    node.press(0, 20, 1500); //在中心往下20像素处，按住1.5秒
}
```


### press(useAct)

> 长按这个节点正中心，并指定用哪种方式（无障碍或模拟手势）。
> 
> useAct 填 true 走无障碍接口长按；填 false 走模拟人手在屏幕坐标上长按。

- 参数 : useAct {boolean} true 用无障碍接口；false 用模拟手势
- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到节点
if (node != null) {
    node.press(true); //用无障碍方式长按它中心
}
```


### move(dir)

> 在这个节点上，朝指定方向滑动一下（通常用来滚动列表）。
> 
> 从节点中心出发，朝 dir 指定的方向滑一段，常用于让聊天记录、商品列表上下翻页。
> dir 只能填这四个字符串之一："up"（向上滑，内容往下翻）、"down"（向下滑）、"left"（向左滑）、"right"（向右滑）。

- 参数 : dir {string} 滑动方向，只能是 "up"、"down"、"left"、"right" 之一
- 版本 : 1.3.6


```javascript
var list = $act.selector().cls("android.widget.ListView").findFirst(); //找到可滚动列表
if (list != null) {
    list.move("up"); //在列表上向上滑一下，相当于用手把列表往上推、显示下面的内容
}
```


### move(x2, y2, dur)

> 从这个节点的中心，拖动手指到屏幕上的另一个坐标点，并指定滑动用时。
> 
> 起点固定是节点中心 (cx, cy)，终点是你给的 (x2, y2)。dur 是从起点滑到终点花多少毫秒，
> 时间越长滑得越慢。常用于拖动滑块、解锁、拖图标到别处。

- 参数 : x2 {int} 终点横坐标（屏幕像素）
- 参数 : y2 {int} 终点纵坐标（屏幕像素）
- 参数 : dur {int} 滑动用时，单位毫秒（数字越大滑得越慢）
- 版本 : 1.3.6


```javascript
var node = $act.selector().cls("android.seekbar").findFirst(); //找到一个滑块
if (node != null) {
    node.move(800, 1500, 500); //从滑块中心拖到坐标(800,1500)，用时500毫秒
}
```


### move(x2, y2, dur, delay)

> 从节点中心拖到指定终点，可指定滑动用时，并在滑动前先停留一会儿。
> 
> 比上一个多一个 delay：手先按在节点中心不动，等 delay 毫秒后再开始滑，滑 dur 毫秒到达终点。
> 这个“先按住一会再滑”的动作更像真人，某些需要先按住才能拖的场景（如图标拖到删除区）会用到。

- 参数 : x2 {int} 终点横坐标（屏幕像素）
- 参数 : y2 {int} 终点纵坐标（屏幕像素）
- 参数 : dur {int} 滑动用时，单位毫秒
- 参数 : delay {int} 开始滑动前先按住不动的时长，单位毫秒
- 版本 : 1.3.6


```javascript
var node = $act.selector().cls("android.seekbar").findFirst(); //找到滑块
if (node != null) {
    node.move(800, 1500, 500, 200); //先按住200毫秒，再用500毫秒拖到(800,1500)
}
```


### move(px, py, x2, y2, dur, delay)

> 从节点中心“再偏移一点”的位置拖到指定终点，可指定滑动用时和按住延时。
> 
> 最灵活的一版：起点不是节点正中心，而是中心再加 (px, py) 偏移；然后先按住 delay 毫秒，
> 再用 dur 毫秒滑到终点 (x2, y2)。

- 参数 : px {int} 起点相对节点中心的水平偏移像素（正数往右，负数往左）
- 参数 : py {int} 起点相对节点中心的垂直偏移像素（正数往下，负数往上）
- 参数 : x2 {int} 终点横坐标（屏幕像素）
- 参数 : y2 {int} 终点纵坐标（屏幕像素）
- 参数 : dur {int} 滑动用时，单位毫秒
- 参数 : delay {int} 开始滑动前先按住不动的时长，单位毫秒
- 版本 : 1.3.6


```javascript
var node = $act.selector().cls("android.seekbar").findFirst(); //找到滑块
if (node != null) {
    //从中心偏左10像素处按住200毫秒，再用500毫秒拖到(800,1500)
    node.move(-10, 0, 800, 1500, 500, 200);
}
```


### draw()

> 在屏幕上给这个节点的位置画一个边框（悬浮框），把它圈出来。
> 
> 脚本找控件时，肉眼很难知道到底找对了没有。调用这个方法后，会在这个节点占的那块区域上
> 画一个框，方便你调试、确认。不需要时用 $draw 的清除方法关掉。

- 版本 : 1.3.6


```javascript
var node = $act.selector().text("登录").findFirst(); //找到“登录”按钮
if (node != null) {
    node.draw(); //在屏幕上把这个按钮框出来，看看找对位置没有
}
```


### input(text)

> 往这个输入框节点里填入文字。
> 
> 先把这个输入框聚焦，再把你给的文字输进去（相当于你打开输入法打字）。一般配合先点击输入框使用。

- 参数 : text {String} 要输入的文字内容
- 版本 : 1.3.6


```javascript
var input = $act.selector().cls("android.widget.EditText").findFirst(); //找到第一个输入框
if (input != null) {
    input.input("你好自动化"); //往这个输入框里填入这段文字
}
```


### input(text, useAcc)

> 往输入框节点填文字，并指定是否强制用无障碍方式输入。
> 
> 和上一个 input(text) 一样填字，多一个开关：useAcc 填 true 时强制走无障碍接口输入；
> 填 false 时，优先用本应用自己的输入法服务输入（更稳）。

- 参数 : text {boolean} true 强制用无障碍接口输入；false 优先用应用自带输入法服务
- 参数 : useAcc {String} 要输入的文字内容
- 版本 : 1.3.6


```javascript
var input = $act.selector().cls("android.widget.EditText").findFirst(); //找到输入框
if (input != null) {
    input.input("你好自动化", true); //强制用无障碍方式填入这段文字
}
```


### findFirst(selector)

> 在当前节点的“所有子孙后代”里，按选择器条件找出第一个符合的节点。
> 
> 之前用 $act.selector() 是在整屏上找；这个方法是“只在某个节点的内部”找——
> 比如先找到一个弹窗，再在这个弹窗里面找它的“确定”按钮，就不会误点到弹窗外面的同名按钮。
> 子孙包括它的儿子、孙子、曾孙……层层往下。找不到返回 null。

- 参数 : selector {UiSelector} 选择器对象，用 $act.selector() 创建并加好条件
- 返回 : {Node} 第一个符合条件的子孙节点；找不到时返回 null


```javascript
//第一步：先找到一个大容器，比如一个弹窗
var dialog = $act.selector().cls("android.app.Dialog").findFirst();
if (dialog != null) {
    //第二步：造一个选择器，条件是文字为“确定”
    var sub = $act.selector().text("确定");
    //第三步：只在这个弹窗内部，找第一个“确定”按钮
    var childNode = dialog.findFirst(sub);
    if (childNode != null) {
        log("在弹窗里找到确定按钮了");
        childNode.click(); //点它
    }
}
```


### findLast(selector)

> 在当前节点的“所有子孙后代”里，按选择器条件找出最后一个符合的节点。
> 
> 和 findFirst 一样是在节点内部找，只是取“最后一个”而不是第一个。
> 比如列表里有好多个同名字段，想要最下面那个时用它。找不到返回 null。

- 参数 : selector {UiSelector} 选择器对象，用 $act.selector() 创建并加好条件
- 返回 : {Node} 最后一个符合条件的子孙节点；找不到时返回 null


```javascript
var list = $act.selector().cls("android.widget.ListView").findFirst(); //先找到列表
if (list != null) {
    var sub = $act.selector().text("条目"); //条件：文字是“条目”
    var last = list.findLast(sub);         //在列表里找最后一个“条目”
    if (last != null) {
        log("找到最后一个条目了");
    }
}
```


### find(selector, index)

> 在当前节点的“所有子孙后代”里，按选择器条件找出“第 index 个”符合的节点。
> 
> 先把所有符合条件的子孙节点按顺序排好，再取第 index 个。index 从 0 开始数（0 就是第一个）。
> 如果 index 给得比总数还大，就退而取最后一个。一个都找不到时返回 null。

- 参数 : selector {UiSelector} 选择器对象，用 $act.selector() 创建并加好条件
- 参数 : index {num} 要取第几个，从 0 开始数；超过总数时取最后一个
- 返回 : {Node} 第 index 个符合条件的子孙节点；一个都找不到时返回 null


```javascript
var list = $act.selector().cls("android.widget.ListView").findFirst(); //先找到列表
if (list != null) {
    var sub = $act.selector().text("条目"); //条件：文字是“条目”
    var third = list.find(sub, 2);          //取第 3 个（下标从 0 开始，2 就是第三个）
    if (third != null) {
        log("找到第三个条目了：" + third.text);
    }
}
```


### findAll(selector)

> 在当前节点的“所有子孙后代”里，把所有符合选择器条件的节点一次性全部找出来。
> 
> 上面几个方法只取一个，这个方法把符合条件的全部打包成一个 Node 列表返回，
> 拿到后可以用 for 循环遍历，逐个点击或读文字。一个都找不到时返回空列表。

- 参数 : selector {UiSelector} 选择器对象，用 $act.selector() 创建并加好条件
- 返回 : {Node[]} 所有符合条件的子孙节点组成的列表；找不到时是空列表


```javascript
var list = $act.selector().cls("android.widget.ListView").findFirst(); //先找到列表
if (list != null) {
    var sub = $act.selector().text("条目"); //条件：文字是“条目”
    var all = list.findAll(sub);           //取出所有“条目”节点
    for (var i = 0; i < all.size(); i++) {  //遍历每一个
        log("第" + i + "个条目：" + all.get(i).text);
    }
}
```


