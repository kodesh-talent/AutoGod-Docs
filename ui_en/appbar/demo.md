# 综合案例

- 更新时间:2026-10-22 10:58:39



## Xml代码


```html
// 将布局保存为 ES5 字符串；每行末尾的加号用于拼接。
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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="应用条"
                title="Appbar" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true"
                    text="基础用法 设置菜单按钮点击事件" />
                <appbar-layout w="max">
                    <!--
                    在应用条(appbar)中所有的标签中的文本(text)属性值不能重复
                    因为在监听菜单的时候只会根据(text)文本属性值进行匹配
                    -->
                    <appbar back="true" id="appbar" subTitle="副标题" title="应用条" w="max">
                        <menu icon="ic_settings_fill" text="设置" />
                        <!-- menu、item、都可以作为菜单选项 -->
                        <item icon="ic_share_fill" text="分享" />
                        <!--在menu中可以使用item配置多级子标签-->
                        <menu text="更多">
                            <item text="关于软件" />
                            <item text="检查更新" />
                            <!--在item标签中还可以嵌套使用item作为子标签-->
                            <item text="更多选项">
                                <item text="关于软件11" />
                                <item text="检查更新22" />
                            </item>
                        </menu>
                    </appbar>
                </appbar-layout>
                <!--设置主菜单-->
                <text gravity="center" h="50" selectable="true" text="设置主菜单 menu标签" />
                <appbar-layout w="max">
                    <appbar subTitle="副标题" title="应用条" w="max">
                        <menu icon="ic_settings_fill" text="设置" />
                        <!-- menu、item、都可以作为菜单选项 -->
                        <menu icon="ic_share_fill" text="分享" />
                        <!-- menu标签也等价于item标签 -->
                        <item icon="ic_article_fill" text="日志" />
                    </appbar>
                </appbar-layout>
                <!--设置主菜单颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置主菜单颜色 iconTint=颜色" />
                <appbar-layout w="max">
                    <appbar subTitle="副标题" title="应用条" w="max">
                        <menu icon="ic_settings_fill" iconTint="#3574F0" text="设置" />
                        <menu icon="ic_share_fill" iconTint="#C94F4F" text="分享" />
                        <!-- menu标签也等价于item标签 -->
                        <item icon="ic_article_fill" iconTint="#57965C" text="日志" />
                    </appbar>
                </appbar-layout>
                <!--设置多级菜单-->
                <text gravity="center" h="50" selectable="true" text="设置多级菜单 menu-item标签" />
                <appbar-layout w="max">
                    <!--
                    在应用条(appbar)中所有的标签中的文本(text)属性值不能重复
                    因为在监听菜单的时候只会根据(text)文本属性值进行匹配
                    -->
                    <appbar subTitle="副标题" title="应用条" w="max">
                        <menu icon="ic_settings_fill" text="设置" />
                        <!-- menu标签也等价于item标签 -->
                        <item icon="ic_share_fill" text="分享" />
                        <!--在menu中可以使用item配置多级子标签-->
                        <menu text="更多">
                            <item text="关于软件" />
                            <item text="检查更新" />
                            <!--在item标签中还可以嵌套使用item作为子标签-->
                            <item text="更多选项">
                                <item text="关于软件11" />
                                <item text="检查更新22" />
                            </item>
                        </menu>
                    </appbar>
                </appbar-layout>
                <!--设置多级菜单图标-->
                <text gravity="center" h="50" selectable="true"
                    text="设置多级菜单图标 more moreTint" />
                <appbar-layout w="max">
                    <!--
                    在应用条(appbar)中所有的标签中的文本(text)属性值不能重复
                    因为在监听菜单的时候只会根据(text)文本属性值进行匹配
                    -->
                    <appbar subTitle="副标题" title="应用条" w="max">
                        <!--设置多级菜单的图标
                        more=图标 (或者moreIcon)
                        moreTint=图标颜色 (或者moreIconTint、moreIconColor)
                        -->
                        <menu more="ic_dehaze_outline" moreTint="#3574F0" text="更多">
                            <item text="关于软件" />
                            <item text="检查更新" />
                            <!--在item标签中还可以嵌套使用item作为子标签-->
                            <item text="更多选项">
                                <item text="关于软件11" />
                                <item text="检查更新22" />
                            </item>
                        </menu>
                    </appbar>
                </appbar-layout>
                <!--设置标题-->
                <text gravity="center" h="50" selectable="true" text="设置标题 title=标题" />
                <appbar-layout w="max">
                    <appbar title="标题" w="max" />
                </appbar-layout>
                <!--设置副标题-->
                <text gravity="center" h="50" selectable="true" text="设置副标题 subTitle=副标题" />
                <appbar-layout w="max">
                    <appbar subTitle="副标题" title="标题" w="max" />
                </appbar-layout>
                <!--设置标题颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置标题颜色 titleColor=标题颜色" />
                <appbar-layout w="max">
                    <appbar title="标题" titleColor="#C94F4F" w="max" />
                </appbar-layout>
                <!--设置副标题颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置副标题颜色 subTitleColor=副标题颜色" />
                <appbar-layout w="max">
                    <appbar subTitle="设置副标题颜色" subTitleColor="#C94F4F" title="应用条"
                        w="max" />
                </appbar-layout>
                <!--设置显示返回按钮-->
                <text gravity="center" h="50" selectable="true" text="设置显示返回按钮 back=true" />
                <appbar-layout w="max">
                    <appbar back="true" subTitle="设置显示返回按钮" title="应用条" w="max" />
                </appbar-layout>
                <!--设置显示返回按钮颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置显示返回按钮颜色 backTint=颜色" />
                <appbar-layout w="max">
                    <appbar back="true" backTint="#C94F4F" subTitle="设置显示返回按钮颜色"
                        title="应用条" w="max" />
                </appbar-layout>
                <!--设置图标-->
                <text gravity="center" h="50" selectable="true" text="设置图标 icon=图标" />
                <appbar-layout w="max">
                    <appbar icon="ic_message_outline" subTitle="设置图标" title="应用条" w="max" />
                </appbar-layout>
                <!--设置图标颜色-->
                <text gravity="center" h="50" selectable="true" text="设置图标颜色 iconTint=颜色" />
                <appbar-layout w="max">
                    <appbar icon="ic_message_outline" iconTint="#C94F4F" subTitle="设置图标颜色"
                        title="应用条" w="max" />
                </appbar-layout>
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <appbar-layout w="max">
                    <appbar bg="#5557965C" subTitle="设置背景颜色" subTitleColor="#C94F4F"
                        title="应用条" w="max" />
                </appbar-layout>
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true"
                    text="设置背景图片 bgImg=图片地址" />
                <appbar-layout w="max">
                    <appbar bgImg="example/$ui - 交互界面/01.appbar-应用条/img/bg-appbar.png"
                        subTitle="副标题" subTitleColor="#C94F4F" title="标题" w="max" />
                </appbar-layout>
            </linear>
        </nested>
    </coord>
</ui>
`;
// 解析布局字符串得到界面对象。
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("example/$ui - 交互界面/01.appbar-应用条/appbar.xml");
//绑定标题栏返回按钮
ui.id("mAppbar").back(function(){
    ui.finish();
});
var appbar = ui.id("appbar");
//设置返回按钮点击事件
appbar.back(function(){
    toast("点击了:返回按钮");
});
//设置菜单选项点击事件
appbar.menu(function(text){
    toast("点击了:"+text);
});
//显示界面
ui.show();
```


