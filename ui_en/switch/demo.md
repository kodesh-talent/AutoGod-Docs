# 综合案例

- 更新时间:2026-10-22 10:58:42



使用脚本创建界面


```html
// 中英文示例任选一套运行；布局中的本地图片需要提前准备。
// 布局是普通字符串，逐行连接，不使用 ES6 模板字符串。
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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="开关"
                title="Switch" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" gravity="center" w="max">
                    <switch id="demoSwitch" check="true" color="#57965C" margin="3" text="开关" />
                    <switch check="true" color="#C94F4F" margin="3" />
                    <switch check="true" color="#3574F0" margin="3" />
                </linear>
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <linear dir="h" w="max">
                    <switch color="#57965C" margin="5" text="吃饭" />
                    <switch color="#C94F4F" margin="5" text="睡觉" />
                    <switch color="#3574F0" margin="5" text="游戏" />
                </linear>
                <linear dir="h" w="max">
                    <switch check="true" color="#57965C" margin="5" text="吃饭" />
                    <switch check="true" color="#C94F4F" margin="5" text="睡觉" />
                    <switch check="true" color="#3574F0" margin="5" text="游戏" />
                </linear>
                <!--设置文本-->
                <text gravity="center" h="50" selectable="true" text="设置文本 text=文本" />
                <switch text="我是文本" w="max" />
                <!--设置文本大小-->
                <text gravity="center" h="50" selectable="true" text="设置文本大小 textSize=尺寸" />
                <switch text="我的尺寸:10" textSize="10" w="max" />
                <switch text="我的尺寸:17" textSize="17" w="max" />
                <!--设置文本颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本颜色 textColor=颜色" />
                <switch text="看我颜色" textColor="#C94F4F" w="max" />
                <switch text="看我颜色" textColor="#3574F0" w="max" />
                <!--设置是否选中-->
                <text gravity="center" h="50" selectable="true" text="设置是否选中 check=true" />
                <switch check="false" text="没选择" w="max" />
                <switch check="true" text="选中" w="max" />
                <!--设置最小宽度-->
                <text gravity="center" h="50" selectable="true" text="设置最小宽度 minW=数字" />
                <linear dir="v" w="max">
                    <!--为了看清效果，这里设置背景颜色-->
                    <switch bg="#57965C" margin="5" minW="200" text="最小宽度:200" />
                    <switch bg="#C94F4F" margin="5" minW="250" text="最小宽度:250" />
                </linear>
                <!--设置最小高度-->
                <text gravity="center" h="50" selectable="true" text="设置最小高度 minH=数字" />
                <linear dir="h" w="max">
                    <!--为了看清效果，这里设置背景颜色-->
                    <switch bg="#57965C" margin="5" minH="60" text="最小高度:60" />
                    <switch bg="#C94F4F" margin="5" minH="80" text="最小高度:80" />
                </linear>
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=数字" />
                <linear dir="v" w="max">
                    <!--为了看清效果，这里设置背景颜色-->
                    <switch bg="#57965C" margin="5" padding="10" text="内边距:10" />
                    <switch bg="#C94F4F" margin="5" padding="20" text="内边距:20" />
                </linear>
                <!--设置重力-->
                <text gravity="center" h="50" selectable="true" text="设置重力 gravity=对齐方式" />
                <linear dir="v" w="max">
                    <switch gravity="start" margin="5" text="开始" w="max" />
                    <switch gravity="center" margin="5" text="中间" w="max" />
                    <switch gravity="end" margin="5" text="结束" w="max" />
                </linear>
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <linear dir="h" w="max">
                    <switch bg="#57965C" margin="5" text="吃饭" />
                    <switch bg="#C94F4F" margin="5" text="睡觉" />
                    <switch bg="#3574F0" margin="5" text="游戏" />
                </linear>
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true" text="设置背景图片 bgImg=图片" />
                <linear dir="v" w="max">
                    <!--
                    textColor="bg" 是一种动态设置文本颜色的方式，表示当前字体颜色是背景颜色。
                    -->
                    <switch bgImg="example/$ui - 交互界面/03.check-复选框/img/bg01.png" margin="2"
                        text="吃饭" textColor="bg" w="250" />
                    <switch bgImg="example/$ui - 交互界面/03.check-复选框/img/bg02.png" margin="2"
                        text="睡觉" textColor="bg" w="250" />
                    <switch bgImg="example/$ui - 交互界面/03.check-复选框/img/bg03.png" margin="2"
                        text="游戏" textColor="bg" w="250" />
                </linear>
            </linear>
        </nested>
    </coord>
</ui>
`;
// 直接解析布局字符串，无需另建布局文件。
var ui = $ui.layout(layout);
// 按布局中的真实标识查找应用条，返回按钮用于关闭当前界面。
ui.id("mAppbar").back(function () {
    ui.finish();
});
// 回调参数是布尔值，true 表示选中，false 表示未选中。
ui.id("demoSwitch").onCheck(function (checked) {
    toast(checked ? "开关已打开" : "开关已关闭");
});
// 事件设置完毕后显示界面。
ui.show();
```


继续操作英文完整示例中已经创建的界面。
先运行英文示例，再运行这段代码，ui 是前面创建的界面对象。不要重新加载其他控件的布局文件。


```html
// 修改开关文字，不会重新创建界面。
var control = ui.id("demoSwitch");
control.setText("示例开关");
```


