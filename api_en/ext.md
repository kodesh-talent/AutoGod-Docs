# $ext - 拓展:加载Dex,Apk,Jar,So

- 更新时间:2026-10-22 10:55:48

> 扩展加载对象，脚本里叫 $ext。
> 
> 它可以在脚本运行时动态加载外部的 dex/apk/jar/so 文件，把里面的 Java 类引入脚本使用，
> 相当于给脚本临时扩充能力。加载成功后会返回一个类加载器，之后就能用里面的类了。



```javascript
$ext.loadDex("/sdcard/Download/helper.dex");
```




### loadApk(apkPath)

> 加载一个外部 APK 文件，把它里面的类引入脚本可用。

- 参数 : apkPath {string} 要加载的 apk 文件路径
- 返回 : {DexClassLoader} 加载成功后的类加载器，可用它反射使用 apk 里的类
- 版本 : 1.2.5


```javascript
$ext.loadApk("/sdcard/测试.apk");
```


### loadDex(dexPath)

> 加载一个外部 dex 文件，把它里面的类引入脚本可用。
> 
> $ext 会把每个加载过的 dex 按一个唯一的类加载器 ID 缓存起来。
> 
> 首次加载时会保存 ID 和类加载器。
> 
> 之后再加载同一个 dex 会直接复用缓存，不会重复加载。
> 
> 如果想强制重新加载，要先调用 clear() 清掉缓存。

- 参数 : dexPath {string} 要加载的 dex 文件路径
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.1.0


```javascript
$ext.loadDex("./res/demo.dex");
//加载后即可在脚本里使用 dex 里的类
```


### loadDexs(paths)

> 一次性加载多个 dex 文件，合并到同一个类加载器里。

- 参数 : paths {string[]} 要加载的多个 dex 文件路径数组
- 返回 : {DexClassLoader} 合并加载后的类加载器
- 版本 : 1.2.6


```javascript
//依次加载三个 dex
$ext.loadDexs(["/res/demo1.dex","/res/demo2.dex","/res/demo3.dex"]);
```


### loadJar(jarPath)

> 加载一个外部 jar 文件，把它里面的类引入脚本可用。
> 
> $ext 会把每个加载过的 jar 按一个唯一的类加载器 ID 缓存起来。
> 
> 首次加载时会保存 ID 和类加载器。
> 
> 之后再加载同一个 jar 会直接复用缓存。
> 
> 想强制重新加载要先调用 clear() 清缓存。

- 参数 : jarPath {string} 要加载的 jar 文件路径
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.1.0


```javascript
$ext.loadJar("/res/demo.jar");
//加载后即可使用 jar 里的类
```


### loadJars(paths)

> 一次性加载多个 jar 文件，合并到同一个类加载器里。
> 
> 用法和 loadDexs 一样，只是文件类型换成 jar。

- 参数 : paths {string[]} 要加载的多个 jar 文件路径数组
- 返回 : {DexClassLoader} 合并加载后的类加载器
- 版本 : 1.2.6


```javascript
//依次加载多个 jar
$ext.loadJars(["/res/demo1.jar","/res/demo2.jar","/res/demo3.jar"]);
```


### loadDex(options)

> 用配置对象的方式加载 dex（可同时加载依赖的 so 原生库）。
> 
> 适合一个 dex 还依赖若干 .so 文件的情况，一次性把 dex 和 so 都配好。

- 参数 : options {LoadExtConfig} 配置对象，含主 dex 路径和 so 列表
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.1.0


```javascript
var options = {
    dex: "/res/demo.dex",  //主 dex 文件路径
    so:[
         //要连带加载的 so 原生库列表
         {
            路径: "/res/libxxx.so",  //so 文件路径
            加载: true              //是否立即加载
         },
         //...
    ]
}
$ext.loadDex(options);
//加载完成后即可使用 dex 和它依赖的 so
```


### loadJar(options)

> 用配置对象的方式加载 jar（可同时加载依赖的 so 原生库）。
> 
> 适合一个 jar 还依赖若干 .so 文件时，一次性把 jar 和 so 都配好。
> 
> 用法和 loadDex(options) 一样，只是主文件类型换成 jar。

- 参数 : options {LoadExtConfig} 配置对象，含主 jar 路径和 so 列表
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.1.0


```javascript
var options = {
    jar: "/res/demo.jar",  //主 jar 文件路径
    so:[
         //要连带加载的 so 原生库列表
         {
            路径: "/res/libxxx.so",  //so 文件路径
            加载: true              //是否立即加载
         },
         //...
    ]
}
$ext.loadJar(options);
//加载完成后即可使用 jar 里的类
```


### loadApk(options)

> 用配置对象的方式加载 apk（可同时加载依赖的 so 原生库）。

- 参数 : options {LoadExtConfig} 配置对象，含主 apk 路径和 so 列表
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.2.5


```javascript
var options = {
    apk: "/sdcard/测试.apk",  //主 apk 文件路径
    so:[
         //要连带加载的 so 原生库列表
         {
            路径: "/res/libxxx.so",  //so 文件路径
            加载: true              //是否立即加载
         },
         //...
    ]
}
$ext.loadApk(options);
//加载完成后即可使用 apk 里的类
```


### clear()

> 清除缓存的类加载器
> 
> $ext 会把加载过的 jar/dex 按唯一的类加载器 ID 缓存起来。
> 
> 首次加载时会保存 ID 和类加载器。
> 
> 这个方法就是把这些缓存的 ID 和类加载器全部清掉。
> 
> 清掉后再加载同一个文件就会重新加载，而不是复用旧缓存。
> 
> 注意：如果已经加载过 so 文件，本方法慎用。
> 因为 so 只能被一个类加载器加载一次，反复清缓存重载可能报错。
> 
> 一般只在需要热更新重新加载 dex/jar 时才调用。

- 版本 : 1.1.0


```javascript
$ext.clear();
```


### delete()

> 删除缓存文件
> 
> 不仅清掉内存里的类加载器，还把解压缓存到磁盘上的文件也一起删掉。
> 
> 适合彻底清理、释放存储空间时使用。

- 版本 : 1.1.1


```javascript
$ext.delete();
```


