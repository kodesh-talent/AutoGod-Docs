# 综合案例

- 更新时间:2026-10-22 10:58:39



## 布局与脚本完整示例


```html
// 中英文版本任选一个运行；两段分别创建独立界面。
// 标签表示控件，属性改变外观；可以每次修改一个值，观察界面变化。
// 背景图片路径指向本地资源，请先准备对应图片或改成自己的图片路径。
var layoutXml = `
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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="按钮"
                title="Button" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--按钮概览-->
                <text gravity="center" h="50" selectable="true" text="按钮概览" />
                <linear dir="h" w="max">
                    <button text="按钮" />
                    <button style="outline" text="按钮" />
                    <button style="tonal" text="按钮" />
                    <button style="text" text="按钮" />
                </linear>
                <linear dir="h" w="max">
                    <button color="#518855" text="按钮" />
                    <!--
                    textColor="bg" 使用背景颜色作为文本颜色(使文字颜色随主题动态变化)
                    -->
                    <button color="#C94F4F" text="按钮" textColor="bg" />
                    <button style="tonal" color="#3471E9" text="按钮" textColor="bg" />
                    <button style="text" color="#C435FF" text="按钮" textColor="bg" />
                </linear>
                <linear dir="h" w="max">
                    <button style="text" icon="ic_delete_fill" iconTint="text" text="删除" />
                    <button style="text" icon="ic_home_fill" iconTint="text" text="主页" />
                    <button style="text" icon="ic_menu_fill" iconTint="text" text="菜单" />
                </linear>
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 设置点击事件" />
                <button id="button" text="请点击我" w="max" />
                <!--设置样式-->
                <text gravity="center" h="50" selectable="true"
                    text="设置样式 style=text|outline|icon|tonal" />
                <button text="默认样式" w="max" />
                <button style="icon" text="图标样式" w="max" />
                <button style="text" text="文本样式" w="max" />
                <button style="outline" text="边框样式" w="max" />
                <button style="tonal" text="色调样式" w="max" />
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <button color="#57965C" text="绿色主题颜色" w="max" />
                <button color="#C94F4F" text="红色主题颜色" w="max" />
                <button color="#3574F0" text="蓝色主题颜色" w="max" />
                <!--设置文本-->
                <text gravity="center" h="50" selectable="true" text="设置文本 text=我是文本" />
                <button style="outline" text="我是文本" w="max" />
                <!--设置文本字体-->
                <text gravity="center" h="50" selectable="true" text="设置文本字体 typeface=字体" />
                <button style="outline" text="斜体文本" typeface="italic" w="max" />
                <button style="outline" text="粗体文本" typeface="bold" w="max" />
                <button style="outline" text="粗体斜体文本" typeface="bold_italic" w="max" />
                <!--设置字体颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置字体颜色 textColor=颜色" />
                <button style="outline" text="绿色字体颜色" textColor="#57965C" w="max" />
                <button style="outline" text="红色字体颜色" textColor="#C94F4F" w="max" />
                <button style="outline" text="蓝色字体颜色" textColor="#3574F0" w="max" />
                <!--设置涟漪颜色-->
                <text gravity="center" h="50" selectable="true" text="设置涟漪颜色 ripper=颜色" />
                <button style="outline" ripper="#57965C" text="绿色涟漪颜色" w="max" />
                <button style="outline" ripper="#C94F4F" text="红色涟漪颜色" w="max" />
                <button style="outline" ripper="#3574F0" text="蓝色涟漪颜色" w="max" />
                <!--设置圆角弧度-->
                <text gravity="center" h="50" selectable="true" text="设置圆角弧度 radius=弧度" />
                <button style="outline" radius="5" text="弧度:5" w="max" />
                <button style="outline" radius="10" text="弧度:10" w="max" />
                <button style="outline" radius="15" text="弧度:15" w="max" />
                <!--设置文本尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置文本尺寸 textSize=尺寸" />
                <button style="outline" text="文本尺寸:10" textSize="10" w="max" />
                <button style="outline" text="文本尺寸:13" textSize="13" w="max" />
                <button style="outline" text="文本尺寸:16" textSize="16" w="max" />
                <!--设置图标-->
                <text gravity="center" h="50" selectable="true" text="设置图标 icon=图标" />
                <button icon="ic_settings_fill" text="设置图标" w="max" />
                <!--设置图标颜色-->
                <text gravity="center" h="50" selectable="true" text="设置图标颜色 iconTint=颜色" />
                <button icon="ic_settings_fill" iconTint="#C94F4F" text="设置图标颜色" w="max" />
                <!--设置图标尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置图标尺寸 iconSize=尺寸" />
                <button icon="ic_settings_fill" iconSize="18" text="设置图标尺寸:10" w="max" />
                <button icon="ic_settings_fill" iconSize="20" text="设置图标尺寸:20" w="max" />
                <button icon="ic_settings_fill" iconSize="30" text="设置图标尺寸:30" w="max" />
                <!--设置图标重力-->
                <text gravity="center" h="50" selectable="true"
                    text="设置图标重力 iconGravity=start|end|top" />
                <button icon="ic_settings_fill" iconGravity="start" text="设置图标重力:开始"
                    w="max" />
                <button icon="ic_settings_fill" iconGravity="end" text="设置图标重力:结束"
                    w="max" />
                <button h="70" icon="ic_settings_fill" iconGravity="top" text="设置图标重力:上方"
                    w="max" />
                <!--设置图标内边距-->
                <text gravity="center" h="50" selectable="true"
                    text="设置图标内边距 iconPadding=尺寸" />
                <button gravity="start|center" icon="ic_settings_fill" iconPadding="20"
                    text="设置图标内边距:20" w="max" />
                <button gravity="start|center" icon="ic_settings_fill" iconPadding="30"
                    text="设置图标内边距:30" w="max" />
                <button gravity="start|center" icon="ic_settings_fill" iconPadding="40"
                    text="设置图标内边距:40" w="max" />
                <!--设置最小宽度-->
                <text gravity="center" h="50" selectable="true" text="设置最小宽度 minW=尺寸" />
                <button minW="180" text="最小宽度:180" />
                <button minW="200" text="最小宽度:200" />
                <button minW="220" text="最小宽度:220" />
                <!--设置最小高度-->
                <text gravity="center" h="50" selectable="true" text="设置最小高度 minH=尺寸" />
                <button minH="50" text="最小高度:50" w="max" />
                <button minH="60" text="最小高度:60" w="max" />
                <button minH="70" text="最小高度:70" w="max" />
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true"
                    text="设置内边距 padding=左,上,右,下" />
                <button padding="10" text="内边距:10" w="max" />
                <button padding="20,10" text="内边距:20,10" w="max" />
                <button padding="10,10,10,20" text="内边距:10,10,10,20" w="max" />
                <!--设置重力-->
                <text gravity="center" h="50" selectable="true" text="设置重力 gravity=重力" />
                <button gravity="start" minH="80" text="左上角" w="max" />
                <button gravity="end|bottom" minH="80" text="右下角" w="max" />
                <button gravity="center" minH="80" text="设置重力:中间" w="max" />
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <button bg="#57965C" text="绿色背景" w="max" />
                <button bg="#C94F4F" text="红色背景" w="max" />
                <button bg="#3574F0" text="蓝色背景" w="max" />
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bgImg=图片" />
                <button bgImg="example/$ui - 交互界面/02.button-按钮/img/button_bg.png"
                    text="我是按钮" w="max" />
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layoutXml);
// 按布局中的 id 取得应用条，点击返回按钮时结束当前界面。
ui.id("mAppbar").back(function () {
    ui.finish();
});
// 绑定函数后，只有真正点击按钮才会执行函数内的语句。
ui.id("button").click(function () {
    ui.id("button").setText("已经点击");
});
ui.show(); // 完成事件绑定后显示界面。
```


## 再次修改按钮文字

前面的完整示例已绑定返回和点击事件。下面这段仅用于继续练习英文版本：
在运行英文示例后接着执行，沿用其中的 ui 对象，不需要另建布局文件。


```html
// 找到的按钮就是前面布局中 id 为 button 的那一个。
var button = ui.id("button");
button.setText("再次点击试试"); // 改变显示文字，不会改变原有点击事件。
```


