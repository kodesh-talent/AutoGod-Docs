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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="小片"
                title="Chip" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" w="max">
                    <chip check="true" color="#518855" text="吃饭" />
                    <chip check="true" color="#C94F4F" text="睡觉" />
                    <chip check="true" color="#3471E9" text="游戏" />
                    <chip check="true" color="#C435FF" text="游泳" />
                </linear>
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 监听点击事件" />
                <chip id="chip" text="点击我看看" w="max" />
                <!--设置文本-->
                <text gravity="center" h="50" selectable="true" text="设置文本 text=文本" />
                <chip text="我是文本" />
                <!--设置文本颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本颜色 textColor=文本颜色" />
                <chip text="看我颜色" textColor="#C94F4F" />
                <!--设置文本尺寸-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本尺寸 textSize=文本尺寸" />
                <chip text="看我尺寸" textSize="10" />
                <chip text="看我尺寸" textSize="15" />
                <chip text="看我尺寸" textSize="18" />
                <!--设置弧度-->
                <text gravity="center" h="50" selectable="true" text="设置弧度 radius=弧度" />
                <chip radius="5" text="看我弧度" />
                <chip radius="8" text="看我弧度" />
                <chip radius="11" text="看我弧度" />
                <!--设置图标-->
                <text gravity="center" h="50" selectable="true" text="设置图标 icon=图标" />
                <chip icon="ic_access_alarms_fill" text="看我图标" />
                <!--设置图标颜色-->
                <text gravity="center" h="50" selectable="true" text="设置图标颜色 iconTint=颜色" />
                <chip icon="ic_access_alarms_fill" iconTint="#57965C" text="看我图标颜色" />
                <!--设置可选中-->
                <text gravity="center" h="50" selectable="true" text="设置可选中 checkable=true" />
                <chip checkable="true" text="我可以选中" />
                <!--设置是否选中(前提:设置为可选中)-->
                <text gravity="center" h="50" selectable="true" text="设置是否选中 check=true" />
                <chip check="true" checkable="true" text="我被选中了" />
                <chip check="false" checkable="true" text="我没被选中" />
                <!--设置显示选中图标(前提:设置为可选中)-->
                <text gravity="center" h="50" selectable="true"
                    text="设置显示选中图标 showCheckIcon=true" />
                <chip check="true" checkable="true" showCheckIcon="true" text="我可以选中" />
                <!--设置显示选中图标颜色(前提:设置为可选中)-->
                <text gravity="center" h="50" selectable="true"
                    text="设置显示选中图标颜色 checkIconTint=颜色" />
                <chip check="true" checkIconTint="#C94F4F" checkable="true" showCheckIcon="true"
                    text="我可以选中" />
                <!--设置可点击-->
                <text gravity="center" h="50" selectable="true" text="设置可点击 clickable=true" />
                <chip clickable="true" text="我可以被点击" />
                <chip clickable="false" text="我不能被点击" />
                <!--设置涟漪-->
                <text gravity="center" h="50" selectable="true" text="设置涟漪 ripper=颜色" />
                <chip clickable="true" ripper="#3574F0" text="涟漪颜色" />
                <!--显示关闭按钮-->
                <text gravity="center" h="50" selectable="true"
                    text="显示关闭按钮 showCloseIcon=true(只有通过js设置该控件的关闭点击事件后才能触发点击效果)" />
                <chip showCloseIcon="true" text="我可以被点击" />
                <!--设置关闭按钮颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置关闭按钮颜色 closeIconTint=颜色" />
                <chip closeIconTint="#C94F4F" showCloseIcon="true" text="我可以被点击" />
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <chip color="#3574F0" text="主题颜色" />
                <chip color="#57965C" text="主题颜色" />
                <chip color="#C94F4F" text="主题颜色" />
                <!--设置最小宽度-->
                <text gravity="center" h="50" selectable="true" text="设置最小宽度 minW=数字" />
                <chip minW="60" text="60" />
                <chip minW="100" text="100" />
                <chip minW="130" text="130" />
                <!--设置最小高度-->
                <text gravity="center" h="50" selectable="true" text="设置最小高度 minH=数字" />
                <linear dir="h" gravity="center|bottom" w="max">
                    <!--对于chip而言，gravity属性几乎没有任何效果-->
                    <chip gravity="bottom" minH="60" text="60" />
                    <chip gravity="bottom" minH="100" text="100" />
                    <chip gravity="bottom" minH="130" text="130" />
                </linear>
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=数字" />
                <linear dir="h" w="max">
                    <chip padding="10" text="10" />
                    <chip padding="20" text="20" />
                    <chip padding="30" text="30" />
                </linear>
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("example/$ui - 交互界面/04.chip-小片/chip.xml");
//绑定标题栏返回按钮
ui.id("appbar").back(function(){
    ui.finish();
});
//找到多选按钮并且设置监听事件
ui.id("chip").click(function(){
    toast("我被点击了");
});
//显示界面
ui.show();
```


