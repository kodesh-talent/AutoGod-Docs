# 案例-功能交互

- 更新时间:2026-10-22 10:58:42



本示例将展示一个简单的网页交互功能：实现html与脚本环境功能的相互调用


## Xml代码


```html
// HTML 必须作为字符串传给 loadHtml，不能直接当作 JavaScript 执行。
var html =
    "<!DOCTYPE html>\n" +
    "<html><body>\n" +
    "<button onclick=\"test()\">测试</button>\n" +
    "<script>function test(){ alert(\"来自网页\"); }</script>\n" +
    "</body></html>\n";
var web = $ui.layout("<ui><webview id=\"webview\" /></ui>").id("webview");
web.loadHtml(html);
web.onLoaded(function () {
    web.addFunc("getName", function () { return "示例用户"; });
});
```


## Html代码


```html
// HTML 本身不是 Rhino 脚本；把它保存为字符串后交给 WebView。
var html =
    "<!DOCTYPE html>\n" +
    "<html lang=\"en\">\n" +
    "<head>\n" +
    "    <meta charset=\"UTF-8\">\n" +
    "    <!--\n" +
    "    适配安卓设备屏幕大小\n" +
    "    -->\n" +
    "    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\"></meta>\n" +
    "    <title>Title</title>\n" +
    "</head>\n" +
    "<body>\n" +
    "\n" +
    "<button onclick=\"test1()\">测试</button>\n" +
    "<button onclick=\"test2()\">获取无障碍权限</button>\n" +
    "<button onclick=\"test3()\">获取名字</button>\n" +
    "\n" +
    "</body>\n" +
    "\n" +
    "<script>\n" +
    "    function test1() {\n" +
    "        $.alert(\"我是测试弹窗\");\n" +
    "    }\n" +
    "\n" +
    "    function test2() {\n" +
    "        //无返回参数\n" +
    "        $.call(\"getWza\");\n" +
    "    }\n" +
    "\n" +
    "    function test3() {\n" +
    "        //有返回参数\n" +
    "        var name = $.call(\"getName\");\n" +
    "        $.alert(\"我的名字\", name);\n" +
    "    }\n" +
    "\n" +
    "    //没有参数\n" +
    "    function test4() {\n" +
    "        $.log(\"我被调用了!!!!!!\");\n" +
    "    }\n" +
    "\n" +
    "    //有参数 情人\n" +
    "    function test5(what) {\n" +
    "        return \"我是你的\" + decodeURIComponent(what);\n" +
    "    }\n" +
    "</script>\n" +
    "\n" +
    "</html>\n";
// 页面加载后，网页中的 $.call("getName") 可以调用这个函数。
var web = $ui.layout("<ui><webview id=\"webview\" /></ui>").id("webview");
web.onLoaded(function () {
    web.addFunc("getName", function () { return "示例用户"; });
});
web.loadHtml(html);
```


## JS代码


```javascript
var ui = $ui.layout("main.xml");
var mAppbar = ui.id("mAppbar");
if (mAppbar != null) {
    mAppbar.back(function() {
        ui.finish();
    });
}
var wv = ui.id("webview");
var but = ui.id("but");
wv.onLoaded(function() {
    //获取无障碍权限
    wv.addFunc("getWza", function() {
        //获取无障碍权限
        $permit.wza();
    });
    //返回我的名字
    wv.addFunc("getName", function() {
        return "张三";//只能返回字符串(function(字符串) 几乎所有的类型)
    });
});
but.click(function() {
    //调用html中提供的方法
    wv.callJsStr("test5", "小情人", function(result) {
        log("获得返回值:" + result);
    });
});
//最好放在最后显示主界面
ui.show();
```


