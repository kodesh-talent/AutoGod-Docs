# $ext - 拓展:加载Dex,Apk,Jar,So

- 更新时间:2026-10-22 10:55:48

> 扩展加载对象，脚本里叫 $ext。
> 
> 它可以在脚本运行时动态加载外部的 dex/apk/jar/so 文件，把里面的 Java 类引入脚本使用，
> 相当于给脚本临时扩充能力。加载成功后会返回一个类加载器，之后就能用里面的类了。



```javascript
$ext.loadDex("/sdcard/Download/helper.dex");
```




### 加载apk(apk路径)

> 加载一个外部 APK 文件（上面 loadApk 的中文写法）。

- 参数 : apk路径 {字符串} 要加载的 apk 文件路径
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.7.0


```javascript
$拓展.加载apk("/sdcard/测试.apk");
```


### 加载dex(dex路径)

> 加载一个外部 dex 文件（上面 loadDex 的中文写法）。
> 
> 同样会按唯一 ID 缓存已加载的 dex。
> 
> 首次加载时保存 ID 和类加载器。
> 
> 重复加载同一个 dex 会复用缓存。
> 
> 想强制重新加载要先清除缓存。

- 参数 : dex路径 {字符串} 要加载的 dex 文件路径
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.7.0


```javascript
$拓展.加载dex("./res/demo.dex");
//加载后即可使用 dex 里的类
```


### 加载多个dex(路径数组)

> 一次性加载多个 dex 文件（上面 loadDexs 的中文写法）。

- 参数 : 路径数组 {字符串数组} 要加载的多个 dex 文件路径数组
- 返回 : {DexClassLoader} 合并加载后的类加载器
- 版本 : 1.7.0


```javascript
$拓展.加载多个dex(["/res/demo1.dex","/res/demo2.dex"]);
```


### 加载jar(jar路径)

> 加载一个外部 jar 文件（上面 loadJar 的中文写法）。
> 
> 同样按唯一 ID 缓存已加载的 jar。
> 
> 首次加载时保存 ID 和类加载器。
> 
> 重复加载会复用缓存。
> 
> 想强制重新加载要先清缓存。

- 参数 : jar路径 {字符串} 要加载的 jar 文件路径
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.7.0


```javascript
$拓展.加载jar("/res/demo.jar");
//加载后即可使用 jar 里的类
```


### 加载多个jar(jar路径数组)

> 一次性加载多个 jar 文件（上面 loadJars 的中文写法）。
> 
> 用法和 加载多个dex 一样，只是文件类型换成 jar。

- 参数 : jar路径数组 {字符串数组} 要加载的多个 jar 文件路径数组
- 返回 : {DexClassLoader} 合并加载后的类加载器
- 版本 : 1.7.0


```javascript
$拓展.加载多个jar(["/res/demo1.jar","/res/demo2.jar"]);
```


### 加载dex(配置)

> 用配置对象的方式加载 dex（上面 loadDex(options) 的中文写法）。
> 
> 适合 dex 还依赖若干 .so 原生库时一次性加载。

- 参数 : 配置 {LoadExtConfig} 配置对象，含主 dex 路径和 so 列表
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.7.0


```javascript
var 配置 = {
    dex: "/res/demo.dex",  //主 dex 文件路径
    so:[
         {路径:"so路径", 加载:false},
         {
           路径:"so路径",//so文件路径
           加载:false   //是否立即加载
         },
         //...
    ]
}
$拓展.加载dex(配置);
//加载完成后即可使用
```


### 加载jar(配置)

> 用配置对象的方式加载 jar（上面 loadJar(options) 的中文写法）。
> 
> 适合 jar 还依赖若干 .so 原生库时一次性加载。
> 
> 用法和 加载dex(配置) 一样，只是主文件类型换成 jar。

- 参数 : 配置 {LoadExtConfig} 配置对象，含主 jar 路径和 so 列表
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.7.0


```javascript
var 配置 = {
    jar: "/res/demo.jar",  //主 jar 文件路径
    so:[
         {路径:"so路径", 加载:false},
         {
            路径:"so路径",//so文件路径
            加载:false   //是否立即加载
         },
         //...
    ]
}
$拓展.加载jar(配置);
//加载完成后即可使用
```


### 加载apk(配置)

> 用配置对象的方式加载 apk（上面 loadApk(options) 的中文写法）。

- 参数 : 配置 {LoadExtConfig} 配置对象，含主 apk 路径和 so 列表
- 返回 : {DexClassLoader} 加载成功后的类加载器
- 版本 : 1.7.0


```javascript
var 配置 = {
    apk: "/sdcard/测试.apk",  //主 apk 文件路径
    so:[
         {路径:"so路径", 加载:false},
         {
            路径:"so路径",//so文件路径
            加载:false   //是否立即加载
         },
         //...
    ]
}
$拓展.加载apk(配置);
//加载完成后即可使用
```


### 清除缓存()

> 清除缓存的类加载器（上面 clear 的中文写法）。
> 
> 把缓存的 ID 和类加载器全部清掉。
> 
> 清掉后再加载同一文件会重新加载。
> 
> 如果想重新加载需要调用$拓展.清除缓存()清除id和类加载器
> 
> 一般只在需要热更新重载时才调用。
> 但是如果加载了so文件,这个函数最好只使用一次,因为so文件只能被一个类加载器加载一次
> 
> 所以加载过 so 后尽量别反复清缓存。

- 版本 : 1.7.0


```javascript
$拓展.清除缓存();
```


### 删除缓存()

> 删除缓存文件（上面 delete 的中文写法）。
> 
> 清掉内存类加载器的同时，把磁盘上解压的缓存文件也删掉。
> 
> 适合彻底清理、释放存储空间时使用。

- 版本 : 1.7.0


```javascript
$拓展.删除缓存();
```


