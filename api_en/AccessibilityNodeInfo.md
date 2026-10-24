# AccessibilityNodeInfo - 安卓无障碍节点

- 更新时间:2026-10-22 10:55:45

> 安卓无障碍节点




### const {CharSequence} text;

> 获取该节点的文本内容


### const {CharSequence} contentDescription;

> 获取该节点的内容描述


### const {CharSequence} className;

> 获取该节点在界面上对应的控件类型（如 android.widget.Button、TextView 等），用来判断它是什么控件。


### const {CharSequence} viewIdResourceName;

> 获取该节点在代码里注册的资源 ID（形如 com.demo:id/xxx），这是最稳定、最常用的定位控件依据。


### const {Rect} boundsInScreen;

> 获取该节点在整个屏幕上占据的矩形区域（左上、右下坐标），可用来算出控件位置和中心点做点击。


### const {Rect} boundsInParent;

> 获取该节点在父视图中的位置边界


### const {boolean} isChecked;

> 判断这个复选框/开关当前是否处于勾选（打开）状态。


### const {boolean} isClickable;

> 判断该节点是否可以被点击


### const {boolean} isScrollable;

> 判断这个控件是不是可以滚动（比如列表、聊天记录），为 true 才能对它做滑动操作。


### const {boolean} isEditable;

> 判断这个控件是不是输入框、能否被编辑文本。


### const {boolean} isEnabled;

> 判断该节点是否处于启用状态


### const {boolean} isFocused;

> 判断该节点当前是否拥有输入焦点


### const {boolean} isVisibleToUser;

> 判断这个控件当前在界面上是否对用户可见，不可见的控件通常也点不到。


### const {boolean} isSelected;

> 判断该节点是否处于选中状态 (通常用于上下文菜单或列表项的单选/多选)


### const {boolean} isPassword;

> 判断该节点是否是密码输入框


### const {AccessibilityNodeInfo} parent;

> 获取该节点的父节点对象


### const {int} childCount;

> 获取该节点包含的子节点数量


### const {Object} window;

> 获取该节点所在的窗口信息


### getChild(index)

> 通过索引获取指定的子节点

- 参数 : index {int} 要取的第几个子节点，从 0 开始数
- 返回 : {Node} 对应位置的子节点；越界或不存在时返回 null


```javascript
var child = node.getChild(0);
if (child != null) log(child.getText());
```


### findAccessibilityNodeInfosByText(text)

> 根据文本内容在该节点的子树中查找节点

- 参数 : text {string} 要匹配的文本内容
- 返回 : {Node} 找到的节点；没找到时返回 null


```javascript
var submit = node.findAccessibilityNodeInfosByText("提交");
if (submit != null) submit.performAction(16);
```


### findAccessibilityNodeInfosByViewId(viewIdResourceName)

> 根据资源ID在该节点的子树中查找节点

- 参数 : viewIdResourceName {string} 要匹配的资源 ID，形如 com.demo:id/submit
- 返回 : {Node} 找到的节点；没找到时返回 null


```javascript
var button = node.findAccessibilityNodeInfosByViewId("com.demo:id/submit");
if (button != null) button.performAction(16);
```


### performAction(action)

> 对该节点执行点击操作
> 等同于用户直接用手指点击该控件

- 返回 : {boolean} 动作执行成功返回 true，失败（如控件不可操作）返回 false


```javascript
if (!node.performAction(16)) log("控件当前不可点击");
```


### performLongClick()

> 对该节点执行长按操作

- 返回 : {boolean} 长按成功返回 true，失败返回 false


```javascript
node.performLongClick();
```


### performFocus()

> 对该节点执行获取焦点操作

- 返回 : {boolean} 成功获取焦点返回 true，失败返回 false


```javascript
node.performFocus(); //让这个输入框获得输入焦点，弹出键盘
```


### performClearFocus()

> 对该节点执行清除焦点操作

- 返回 : {boolean} 成功清除焦点返回 true，失败返回 false


```javascript
node.performClearFocus(); //让这个输入框失去焦点，收起键盘
```


### performSelect()

> 对该节点执行选中操作 (通常用于列表项的选中)

- 返回 : {boolean} 选中成功返回 true，失败返回 false


```javascript
node.performSelect(); //选中这个列表项
```


### performClearSelection()

> 对该节点执行清除选中操作

- 返回 : {boolean} 取消选中成功返回 true，失败返回 false


```javascript
node.performClearSelection(); //取消这个列表项的选中
```


### performScrollForward()

> 向前滚动该节点 (例如：列表向下滑动，显示更下面的内容)

- 返回 : {boolean} 成功向下翻一页返回 true；已经滑到底没有更多内容时返回 false


```javascript
while (node.performScrollForward()) log("继续读取下一页");
```


### performScrollBackward()

> 向后滚动该节点 (例如：列表向上滑动，显示更上面的内容)

- 返回 : {boolean} 成功向上翻一页返回 true；已经滑到顶没有更多内容时返回 false


```javascript
node.performScrollBackward(); //列表向上滑，看上面更早的内容
```


### performPaste()

> 把系统剪贴板里已复制的内容，粘贴到这个输入框节点里。

- 返回 : {boolean} 粘贴成功返回 true，失败返回 false


```javascript
$sys.setClip("要粘贴的内容"); //先把内容放进剪贴板
node.performPaste();          //再粘贴到当前输入框
```


### performSetText(text)

> 直接把一段文本写进这个输入框节点（覆盖原有内容），不需要手动弹键盘逐字输入。

- 参数 : text {string} 要写入输入框的文本
- 返回 : {boolean} 设置成功返回 true，失败返回 false


```javascript
node.performSetText("你好世界"); //把输入框内容直接设成这句话
```


### getChildNodes()

> 递归获取该节点的所有子节点列表

- 返回 : {Node[]} 所有直接子节点组成的列表；没有子节点时返回空列表


```javascript
var kids = node.getChildNodes();
for (var i = 0; i < kids.length; i++) log(kids[i].getText());
```


### isClickable(feature)

> 判断该节点的某一项特定功能是否开启

- 参数 : feature {int} 要检查的功能常量（如是否支持输入焦点等）
- 返回 : {boolean} 该节点支持这项功能返回 true，否则返回 false


```javascript
var canFocus = node.isClickable(AccessibilityNodeInfo.FOCUS_INPUT);
log("支持输入焦点", canFocus);
```


### getActions()

> 获取节点的操作列表 (包含该节点可以执行的所有动作，如点击、滚动等)

- 返回 : {int[]} 这个节点当前支持执行的所有动作编号列表


```javascript
var actions = node.getActions();
log("支持的操作数量", actions.length);
```


