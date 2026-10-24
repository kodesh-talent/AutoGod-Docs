# 综合案例

- 更新时间:2026-10-22 10:58:41



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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="单选按钮"
                title="Radio" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <radio-group dir="h" w="max">
                    <radio color="#3574F0" text="吃饭" />
                    <radio color="#518855" text="睡觉" />
                    <radio color="#B44A4A" text="游戏" />
                </radio-group>
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <radio-group dir="h" w="max">
                    <radio color="#3574F0" text="吃饭" />
                    <radio color="#518855" text="睡觉" />
                    <radio color="#B44A4A" text="游戏" />
                </radio-group>
                <!--设置选中-->
                <text gravity="center" h="50" selectable="true" text="设置选中 check=true" />
                <radio-group dir="h" w="max">
                    <radio color="#3574F0" text="吃饭" />
                    <radio check="true" color="#518855" text="睡觉" />
                    <radio color="#B44A4A" text="游戏" />
                </radio-group>
                <!--设置文本-->
                <text gravity="center" h="50" selectable="true" text="设置文本 text=文本" />
                <radio-group dir="h" w="max">
                    <radio color="#3574F0" text="我是文本1" />
                    <radio color="#518855" text="我是文本2" />
                </radio-group>
                <!--设置文本颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本颜色 textColor=文本颜色" />
                <radio-group dir="h" w="max">
                    <radio color="#3574F0" text="我是文本1" textColor="#57965C" />
                    <radio color="#518855" text="我是文本2" textColor="#C94F4F" />
                </radio-group>
                <!--设置最小宽度-->
                <text gravity="center" h="50" selectable="true" text="设置最小宽度 minW=100" />
                <radio-group dir="v" w="max">
                    <radio bg="#57965C" minW="100" text="最小宽度:100" />
                    <radio bg="#3574F0" minW="150" text="最小宽度:150" />
                    <radio bg="#C94F4F" minW="200" text="最小宽度:200" />
                </radio-group>
                <!--设置最小高度-->
                <text gravity="center" h="50" selectable="true" text="设置最小高度 minH=50" />
                <radio-group dir="h" w="max">
                    <radio bg="#57965C" minH="50" text="最小高度:50" />
                    <radio bg="#3574F0" minH="60" text="最小高度:60" />
                    <radio bg="#C94F4F" minH="70" text="最小高度:70" />
                </radio-group>
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=10" />
                <radio-group dir="v" w="max">
                    <radio bg="#57965C" padding="10" text="内边距:10" />
                    <radio bg="#3574F0" padding="20" text="内边距:20" />
                    <radio bg="#C94F4F" padding="30" text="内边距:30" />
                </radio-group>
                <!--设置重力-->
                <text gravity="center" h="50" selectable="true" text="设置重力 gravity=重力" />
                <!--将宽度设置到最大才能看到效果-->
                <radio-group dir="v" w="max">
                    <radio gravity="start" text="开始" w="max" />
                    <radio gravity="center" text="中间" w="max" />
                    <radio gravity="end" text="结束" w="max" />
                </radio-group>
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=背景颜色" />
                <radio-group dir="v" w="max">
                    <radio bg="#57965C" text="看我背景颜色" />
                    <radio bg="#3574F0" text="看我背景颜色" />
                </radio-group>
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true" text="设置背景图片 bgImg=图片" />
                <radio-group dir="h" w="max">
                    <radio bgImg="example/$ui - 交互界面/17.radio-单选按钮/img/img.png" color="bg"
                        gravity="center" text="睡觉" textColor="bg" weight="0.2" />
                    <radio bgImg="example/$ui - 交互界面/17.radio-单选按钮/img/img_1.png" color="bg"
                        gravity="center" text="游戏" textColor="bg" weight="0.2" />
                    <radio bgImg="example/$ui - 交互界面/17.radio-单选按钮/img/img_2.png" color="bg"
                        gravity="center" text="吃饭" textColor="bg" weight="0.2" />
                </radio-group>
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("example/$ui - 交互界面/10.input-输入框/input.xml");
//绑定标题栏返回按钮
ui.id("mAppbar").back(function(){
    ui.finish();
});
//先获取控件
var mButton = ui.id("mButton");
var mInput = ui.id("mInput");
//找到按钮、点击按钮的时候就显示输入框的内容
mButton.click(function(){
    //获取输入框的内容
    var content = mInput.getText();
    //显示输入框的内容
    mButton.snack("内容:"+content);
});
//显示界面
ui.show();
```


