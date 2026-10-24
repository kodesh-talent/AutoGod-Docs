# $plugin - 插件系统

- 更新时间:2026-10-22 10:55:50

> 插件系统对象，脚本里叫 $plugin。
> 
> 它可以加载并运行"插件 App"（另一个独立安装的 APK）里提供的功能：主脚本通过包名加载插件，
> 拿到插件暴露出来的对象后，就能直接调用插件里写好的函数。适合把复杂功能打包成独立插件、按需加载。



```javascript
var plugins = $plugin.ls(); //列出本机已安装的插件
```




### load(packageName)

> 按包名加载一个插件 App，并初始化它的主类，返回可以直接调用的插件对象。
> 
> 插件需要事先在它的 AndroidManifest 里配置好主类名，加载成功后就能拿到这个类的实例，
> 然后像调用普通对象方法一样调用插件提供的功能。

- 参数 : packageName {string} 要加载的插件 App 的包名（例如 "com.example.myplugin"）
- 返回 : {object} 加载并初始化成功后得到的插件对象；插件不存在、未配置主类或初始化失败时返回 null
- 版本 : 1.4.0


```javascript
//加载插件
var myObj = $plugin.load("com.example.myplugin");
//加载成功后，就可以调用插件里自己定义的函数
myObj.我的函数();
```


### ls()

> 列出已安装插件。
> 
> 扫描本机所有 App，找出那些配置了插件主类信息的应用，整理成列表返回。

- 返回 : {AppInfo[]} 已安装插件的信息列表，每项含 appName 应用名、pkgName 包名、icon 图标图片；没有插件时返回空列表
- 版本 : 1.4.0


```javascript
//罗列所有插件应用
var infoList = $plugin.ls();
//打印信息
for (var i = 0; i < infoList.length; i++) {
    var info = infoList[i];
    log("应用名:" + info.appName);
    log("包名:" + info.pkgName);
    //info.icon 是插件图标图片对象，需要时可再处理
}
```


