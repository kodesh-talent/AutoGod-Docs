# 综合案例

- 更新时间:2026-10-22 10:58:40



## Xml代码


```javascript
// 将布局内容作为字符串传入解析方法；返回值是可查找控件的界面对象。
var layout = `
<ui>
    <statusbar />
    <!--使用锚点布局配合滚动布局可以使应用条自带动画-->
    <coord w="max">
        <!--应用标题栏-->
        <appbar-layout w="max">
            <!--
            back:开启返回按钮
            scrollFlags:配置滚动布局滚动时的动画标记
            -->
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="编辑框"
                title="Edit" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" w="max">
                    <edit text="我是" textColor="#57965C" />
                    <edit text="一个" />
                    <edit text="简约的" textColor="#C94F4F" />
                    <edit text="编辑框" textColor="#3574F0" />
                </linear>
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 监听点击事件" />
                <edit id="mEdit" text="我是文本" w="max" />
                <!--设置提示-->
                <text gravity="center" h="50" selectable="true" text="设置提示 hint=提示" />
                <edit hint="提示文本" w="max" />
                <!--设置文本-->
                <text gravity="center" h="50" selectable="true" text="设置文本 text=我是文本" />
                <edit text="我是文本" w="max" />
                <!--设置文本颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本颜色 textColor=颜色" />
                <edit text="我是文本" textColor="#C94F4F" w="max" />
                <!--设置默认文本-->
                <text gravity="center" h="50" selectable="true" text="设置默认文本 def=文本" />
                <edit def="默认文本" w="max" />
                <!--设置类型-->
                <text gravity="center" h="50" selectable="true" text="设置类型 type=类型" />
                <!--密码类型-->
                <text gravity="center" h="50" selectable="true" text="设置类型 type=pass" />
                <edit text="123456???" type="pass" w="max" />
                <!--数字类型-->
                <text gravity="center" h="50" selectable="true" text="设置类型 type=num" />
                <edit text="123" type="num" w="max" />
                <!--手机号码类型-->
                <text gravity="center" h="50" selectable="true" text="设置类型 type=phone" />
                <edit text="15047070177" type="phone" w="max" />
                <!--设置文本尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置文本尺寸 textSize=15" />
                <edit text="文本尺寸:10" textSize="10" w="max" />
                <edit text="文本尺寸:15" textSize="15" w="max" />
                <!--设置最小宽度-->
                <text gravity="center" h="50" selectable="true" text="设置最小宽度 minW=100" />
                <edit bg="#5557965C" minW="200" text="最小宽度:200" />
                <edit bg="#55C94F4F" minW="250" text="最小宽度:250" />
                <!--设置最小高度-->
                <text gravity="center" h="50" selectable="true" text="设置最小高度 minH=100" />
                <linear dir="h" gravity="center" w="max">
                    <edit bg="#5557965C" minH="100" text="最小高度:100" />
                    <edit bg="#55C94F4F" minH="150" text="最小高度:150" />
                </linear>
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true"
                    text="设置内边距 padding=左,上,右,下" />
                <edit bg="#5557965C" padding="10,0,20,30" text="看我内边距" />
                <!--设置重力-->
                <text gravity="center" h="50" selectable="true" text="设置重力 gravity=重力" />
                <!--为了演示效果，宽度设置到最大 w=max -->
                <edit gravity="start|center" text="我在左边" w="max" />
                <edit gravity="center" text="我在中间" w="max" />
                <edit gravity="end|center" text="我在右边" w="max" />
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <edit bg="#5557965C" text="看我背景颜色" w="max" />
                <edit bg="#55C94F4F" text="看我背景颜色" w="max" />
                <edit bg="#553574F0" text="看我背景颜色" w="max" />
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true"
                    text="设置背景图片 bgImg=图片地址" />
                <edit bgImg="example/$ui - 交互界面/06.edit-编辑框/img/bg-edit.png"
                    text="看我背景图片" textColor="#FFFFFF" w="max" />
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("example/$ui - 交互界面/05.drop-下拉框/drop.xml");
//绑定标题栏返回按钮
ui.id("appbar").back(function(){
    ui.finish();
});
//找到编辑框组件
var mEdit = ui.id("mEdit");
//找到编辑框设置文本
mEdit.setText("我是被设置的文本");
//监听文本变化并且输出到控制台 (完整参数:String text, int start, int before, int count)
mEdit.onChanged(function(text){
    log(text);
});
//显示界面
ui.show();
```


