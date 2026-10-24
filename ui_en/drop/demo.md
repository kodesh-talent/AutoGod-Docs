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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="下拉框"
                title="Drop" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" gravity="start|center" w="max">
                    <drop color="#57965C" text="吃饭">
                        <item text="吃饭" />
                        <item text="睡觉" />
                    </drop>
                    <drop style="outline" color="#C94F4F" hint="请选择" prefix="爱好:" text="睡觉">
                        <item text="吃饭" />
                        <item text="睡觉" />
                    </drop>
                </linear>
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 监听点击事件" />
                <drop id="drop" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置选项-->
                <text gravity="center" h="50" selectable="true" text="设置选项 item标签" />
                <drop w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置风格-->
                <text gravity="center" h="50" selectable="true" text="设置风格 style=outline" />
                <drop style="outline" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <drop style="outline" color="#F44236" def="睡觉" hint="你的爱好" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置提示-->
                <text gravity="center" h="50" selectable="true" text="设置提示 hint=提示" />
                <drop style="outline" hint="你的爱好" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置提示颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置提示颜色 hintColor=颜色" />
                <drop style="outline" hint="你的爱好" hintColor="#C94F4F" text="吃饭" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置默认选项(和text的效果一样)-->
                <text gravity="center" h="50" selectable="true" text="设置默认选项 def=默认文字" />
                <drop style="outline" def="睡觉" hint="你的爱好" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置默认文本(和def的效果一样)-->
                <text gravity="center" h="50" selectable="true" text="设置默认文本 text=默认文字" />
                <drop style="outline" hint="你的爱好" text="睡觉" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置文本颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本颜色 textColor=颜色" />
                <drop style="outline" def="睡觉" hint="你的爱好" textColor="#F44236" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置文本尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置文本尺寸 textSize=尺寸" />
                <drop style="outline" def="睡觉" textSize="18" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <drop style="outline" def="睡觉" textSize="25" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置前缀-->
                <text gravity="center" h="50" selectable="true" text="设置前缀 prefix=邮箱" />
                <drop prefix="邮箱：" text="123456789@qq.com" textSize="18" w="max">
                    <item text="123456789@qq.com" />
                    <item text="222333555@qq.com" />
                </drop>
                <!--设置前缀颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置前缀颜色 prefixColor=颜色" />
                <drop prefix="邮箱：" prefixColor="#C94F4F" text="123456789@qq.com" textSize="18"
                    w="max">
                    <item text="123456789@qq.com" />
                    <item text="222333555@qq.com" />
                </drop>
                <!--设置后缀-->
                <text gravity="center" h="50" selectable="true" text="设置后缀 suffix=后缀" />
                <drop prefix="邮箱：" suffix="@qq.com" text="123456789" textSize="18" w="max">
                    <item text="123456789" />
                    <item text="222333555" />
                </drop>
                <!--设置后缀颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置后缀颜色 suffixColor=颜色" />
                <drop prefix="邮箱：" suffix="@qq.com" suffixColor="#C94F4F" text="123456789"
                    textSize="18" w="max">
                    <item text="123456789" />
                    <item text="222333555" />
                </drop>
                <!--设置隐藏尾部倒三角图标-->
                <text gravity="center" h="50" selectable="true"
                    text="设置隐藏尾部倒三角图标 hideIcon=true" />
                <drop style="outline" hideIcon="true" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置重力-->
                <text gravity="center" h="50" selectable="true" text="设置重力 gravity=重力" />
                <drop style="outline" def="吃饭" gravity="start" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <drop style="outline" def="吃饭" gravity="center" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <drop style="outline" def="吃饭" gravity="end" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=内边距" />
                <drop style="outline" def="吃饭" padding="10" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <drop style="outline" def="吃饭" padding="20" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=背景颜色" />
                <drop style="outline" bg="#57965C" def="吃饭" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true"
                    text="设置背景图片 bgImg=背景图片" />
                <drop style="outline" bgImg="example/$ui - 交互界面/05.drop-下拉框/img/img.png" def="吃饭" w="max">
                    <item text="吃饭" />
                    <item text="睡觉" />
                </drop>
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
//找到下拉框并且设置监听事件
ui.id("drop").onCheck(function(title,index){
    toast("选择了:"+title);
});
//显示界面
ui.show();
```


