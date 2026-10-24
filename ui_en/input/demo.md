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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="输入框"
                title="Input" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 设置图片" />
                <linear dir="v" gravity="center" w="max">
                    <input style="outline" id="mInput" w="max" />
                    <!--简单的示例:点击按钮的时候会显示输入框的内容-->
                    <button style="outline" id="mButton" text="获取内容" w="max" />
                </linear>
                <!--设置样式-->
                <text gravity="center" h="50" selectable="true" text="设置样式 style=样式" />
                <linear dir="v" gravity="center" w="max">
                    <input style="outline" text="轮廓样式" w="max" />
                    <input style="fill" text="填充样式" w="max" />
                </linear>
                <!--设置提示-->
                <text gravity="center" h="50" selectable="true" text="设置提示 tip=提示" />
                <input hint="请输入" w="max" />
                <!--设置文本-->
                <text gravity="center" h="50" selectable="true" text="设置文本 text=文本" />
                <input text="我是文本" w="max" />
                <!--设置默认文本-->
                <text gravity="center" h="50" selectable="true" text="设置默认文本 def=文本" />
                <input def="我是文本" w="max" />
                <!--设置文本颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置文本颜色 textColor=颜色" />
                <input text="我是文本" textColor="#57965C" w="max" />
                <!--设置文本尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置文本尺寸 textSize=尺寸" />
                <linear dir="v" gravity="center" w="max">
                    <input text="尺寸:10" textSize="10" w="max" />
                    <input text="尺寸:20" textSize="20" w="max" />
                </linear>
                <!--设置字数限制-->
                <text gravity="center" h="50" selectable="true" text="设置字数限制 len=长度" />
                <input len="10" text="123" w="max" />
                <!--设置最大行数-->
                <text gravity="center" h="50" selectable="true" text="设置最大行数 maxLines=行数" />
                <input maxLines="5" w="max" />
                <!--设置最小行数-->
                <text gravity="center" h="50" selectable="true" text="设置最小行数 minLines=行数" />
                <input minLines="3" w="max" />
                <!--设置单行模式-->
                <text gravity="center" h="50" selectable="true"
                    text="设置单行模式 singleLine=true" />
                <input singleLine="true" w="max" />
                <!--设置帮助文字-->
                <text gravity="center" h="50" selectable="true" text="设置帮助文字 help=帮助" />
                <input help="请输入名称" w="max" />
                <!--设置前缀-->
                <text gravity="center" h="50" selectable="true" text="设置前缀 prefix=前缀" />
                <input prefix="邮箱:" w="max" />
                <!--设置前缀颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置前缀 prefixColor=前缀颜色" />
                <input prefix="邮箱:" prefixColor="#C94F4F" w="max" />
                <!--设置后缀-->
                <text gravity="center" h="50" selectable="true" text="设置后缀 suffix=后缀" />
                <input suffix="@qq.com" w="max" />
                <!--设置后缀颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置后缀 suffixColor=后缀颜色" />
                <input suffix="@qq.com" suffixColor="#C94F4F" w="max" />
                <!--设置类型-->
                <text gravity="center" h="50" selectable="true" text="设置类型 type=类型" />
                <linear dir="v" gravity="center" w="max">
                    <!--密码-->
                    <input text="abcdefg" type="pass" w="max" />
                    <!--数字-->
                    <input text="3.1415926" type="num" w="max" />
                    <!--号码-->
                    <input text="123593749723" type="phone" w="max" />
                </linear>
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <input color="#C94F4F" text="主题颜色:红色" w="max" />
                <!--设置边框颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置边框颜色 strokeColor=颜色" />
                <input strokeColor="#C94F4F" text="边框颜色:红色" w="max" />
                <!--设置边框宽度(dp)-->
                <text gravity="center" h="50" selectable="true"
                    text="设置边框宽度 strokeWidth=宽度" />
                <input strokeWidth="10" text="边框加厚" w="max" />
                <!--设置弧度-->
                <text gravity="center" h="50" selectable="true" text="设置弧度 radius=弧度" />
                <input radius="25" text="设置四角弧度" w="max" />
                <input radius="5,20" text="设置同角弧度" w="max" />
                <input radius="30,10,10,30" text="定制对角度弧度" w="max" />
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=内边距" />
                <input padding="15" text="内边距:15" w="max" />
                <input padding="25" text="内边距:25" w="max" />
                <!--设置重力-->
                <text gravity="center" h="50" selectable="true" text="设置重力 gravity=重力" />
                <input gravity="start" text="开始" w="max" />
                <input gravity="end" text="结束" w="max" />
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <input bg="#57965C" text="看我背景" w="max" />
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true" text="设置背景图片 bgImg=图片" />
                <input bgImg="example/$ui - 交互界面/10.input-输入框/img/img.png" text="看我背景"
                    w="max" />
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


