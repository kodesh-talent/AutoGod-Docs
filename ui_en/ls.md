# 列表

- 更新时间:2026-10-22 10:58:41

> 列表-ls
> 
> 原生类型:{androidx.recyclerview.widget.RecyclerView}





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116225355027820&bvid=BV12EwszPEux&cid=36684696067&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

列表控件，算的算是一个比较复杂的控件，但是该组件确是最常用的组件之一，
因为它可以用来展示一个列表，比如一个商品列表、一个用户列表、一个消息列表等等。


![](./img/1036371318861000.png)

### layout - 子项布局

> 设置子项布局


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <ls id="mLs" w="max" h="max" margin="15" >
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <layout w="max">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <card w="max" margin="2">
                <linear w="max" dir="h" gravity="center|left" padding="15">
                    <!-- 这里才是真正显示数据的地方 -->
                    <text id="name" minW="120" />
                    <text id="age" />
                    <linear w="max" gravity="center|end" weight="1">
                        <button id="delBut" style="text" text="删除" textColor="red" />
                    </linear>
                </linear>
            </card>
        </layout>
    </ls>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/1036371318861000.png)


```javascript
var ui = $ui.layout("/ui.xml");
ui.show();
//找到列表控件
var ls = ui.id("mLs");
//绑定解析视图的方法(必须优先调用)
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText("姓名:" + itemData.name);
    itemUi.id("age").setText("年龄:" + itemData.age);
    itemUi.id("delBut").click(function() {
        $tip.show("删除", "确定删除:" + itemData.name + "吗？", function() {
            //列表删除指定下标的元素
            ls.del(position);
        });
    });
});
//设置数据
ls.flush([
    {
        name: "张三",
        age: 16
    }, {
        name: "李四",
        age: 18
    }
]);
```


### spanCount - 列数

> 设置列数
> 
> 当该属性被设置的时候，布局将采用网格布局来添加子项。


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <ls id="mLs" spanCount="2" w="max" h="max" margin="15" >
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <layout w="max">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <card w="max" margin="2">
                <linear w="max" dir="h" gravity="center|left" padding="15">
                    <!-- 这里才是真正显示数据的地方 -->
                    <text id="name" minW="120" />
                    <text id="age" />
                    <linear w="max" gravity="center|end" weight="1">
                        <button id="delBut" style="text" text="删除" textColor="red" />
                    </linear>
                </linear>
            </card>
        </layout>
    </ls>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/1036885281225000.png)

### padding - 内边距

> 设置内边距


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <ls id="mLs" w="max" h="max" padding="50" >
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <layout w="max">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <card w="max" margin="2">
                <linear w="max" dir="h" gravity="center|left" padding="15">
                    <!-- 这里才是真正显示数据的地方 -->
                    <text id="name" minW="120" />
                    <text id="age" />
                    <linear w="max" gravity="center|end" weight="1">
                        <button id="delBut" style="text" text="删除" textColor="red" />
                    </linear>
                </linear>
            </card>
        </layout>
    </ls>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/1036952604432100.png)

### bg - 背景颜色

> 设置背景颜色


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <ls id="mLs" bg="#1E1F22" w="max" h="max" margin="15" >
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <layout w="max">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <card w="max" margin="2">
                <linear w="max" dir="h" gravity="center|left" padding="15">
                    <!-- 这里才是真正显示数据的地方 -->
                    <text id="name" minW="120" />
                    <text id="age" />
                    <linear w="max" gravity="center|end" weight="1">
                        <button id="delBut" style="text" text="删除" textColor="red" />
                    </linear>
                </linear>
            </card>
        </layout>
    </ls>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/1037040261908500.png)

### bgImg - 背景图片

> 设置背景图片


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 示例用到的本地资源需要提前准备，请把文件路径改为项目中的实际路径。
var layoutXml = `
<ui>
    <statusbar />
    <ls id="mLs" bgImg="/res/bg-ls.png" w="max" h="max" margin="30" >
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <layout w="max">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <card w="max" margin="2">
                <linear w="max" dir="h" gravity="center|left" padding="15">
                    <!-- 这里才是真正显示数据的地方 -->
                    <text id="name" minW="120" />
                    <text id="age" />
                    <linear w="max" gravity="center|end" weight="1">
                        <button id="delBut" style="text" text="删除" textColor="red" />
                    </linear>
                </linear>
            </card>
        </layout>
    </ls>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/1037283848936000.png)

### scrollTop()

> 让列表平滑滚动回最顶部（第 0 项）。


```javascript
//先用一段 XML 创建界面：一个占满全屏的列表，每项就是一行文字
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
//先告诉列表怎么把数据填到每一行
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData); //把每条数据显示到那行的文字上
});
//塞 50 条数据进去
ls.flush(["第1项", "第2项", "第3项", "第4项", "第5项"]);
ls.scrollTop(); //自动滚回最上面
```


### scrollBottom()

> 让列表平滑滚动到最底部（最后一项）。


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙", "丁", "戊"]);
ls.scrollBottom(); //自动滚到最后一项
```


### scroll(position)

> 让列表平滑滚动到指定下标的那一项。
> 
> 下标从 0 开始：传 0 就是第一项，传 9 就是第十项。

- 参数 : position {Number} 要滚动到的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
//塞 20 条数据
var arr = [];
for (var i = 0; i < 20; i++) {
    arr.push("第" + (i + 1) + "项");
}
ls.flush(arr);
ls.scroll(9); //滚到第 10 项（下标 9）
```


### bindHolder(holder)

> 绑定“每行怎么填数据”的回调，这是列表最重要的一步，必须在 flush 之前调用。
> 
> 列表里每一行长什么样，是由 XML 里那个 layout 子节点决定的；但每行上显示的文字、按钮内容，要靠这个回调来填。
> 每次显示（或复用）一行时，系统都会回调你传进来的函数，三个参数依次是：
> <ul>
>   <li>itemUi：这一行的界面对象，用它的 id("...") 拿到行里的子控件；</li>
>   <li>itemData：这一行对应的数据（就是你 flush 数组里的那一项）；</li>
>   <li>position：这一行的下标（从 0 开始）。</li>
> </ul>

- 参数 : holder {function} 绑定回调，参数依次为该行界面对象、该行数据、该行下标


```javascript
//先用一段 XML 创建界面：一个列表，每行有名字和年龄两个文字
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><linear dir="h" padding="15"><text id="name" minW="120"/><text id="age"/></linear></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
//告诉列表：每一行怎么把数据填到那两个文字上
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText("姓名:" + itemData.name); //把名字填上
    itemUi.id("age").setText("年龄:" + itemData.age); //把年龄填上
});
//给列表塞两条数据
ls.flush([{name: "张三", age: 16}, {name: "李四", age: 18}]);
```


### flush(data)

> 一次性设置整个列表的数据并立刻刷新显示（会替换掉之前的所有数据）。
> 
> 传入一个数组，数组里每一项就是一行；每一项可以是简单字符串，也可以是带字段的对象（配合 bindHolder 填到子控件上）。

- 参数 : data {Array} 要显示的数据数组


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
//先告诉列表怎么把数据填到每行
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
//一次性塞三条数据并刷新
ls.flush(["苹果", "香蕉", "橙子"]);
```


### flush(data, position)

> 只替换列表里某一行的数据并刷新那一行，其它行不动。

- 参数 : data {Object} 新的数据
- 参数 : position {Number} 要替换的那一行的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["苹果", "香蕉", "橙子"]); //先放三条
ls.flush("西瓜", 1); //把下标 1（第二条）换成西瓜
```


### del(position)

> 删除列表里指定下标的那一行，并自动刷新列表。

- 参数 : position {Number} 要删除的那一行的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.del(0); //删掉第一条（甲）
```


### add(data)

> 在列表末尾追加一条数据，并自动刷新。

- 参数 : data {Object} 要追加的数据


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙"]);
ls.add("丙"); //末尾再追加一条
```


### add(data, position)

> 在列表的指定位置插入一条数据，原来那一行及后面的行往后顺移。

- 参数 : data {Object} 要插入的数据
- 参数 : position {Number} 插入位置的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.add("新", 1); //插到下标 1，变成 甲 新 乙 丙
```


### clear()

> 把列表里所有数据清空，列表变成空白。


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.clear(); //全部清空
```


### getData()

> 读出列表当前保存的全部数据（返回一个数组），不影响显示。

- 返回 : {Array} 列表当前的数据数组
- 版本 : 1.7.3


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
var data = ls.getData(); //把全部数据读出来
log("现在共有" + data.length + "条");
```


