# $log - 日志框架

- 更新时间:2026-10-22 10:55:49

> 日志工具对象，脚本里叫 $log。
> 
> 不同级别（信息/调试/警告/错误）的日志会用不同颜色或标签区分。
> 



```javascript
$log.info("task started");
```




### i(args)

> 打印一条"信息"级别的日志（info 的简写）。
> 

- 参数 : args {string...} 要打印的内容，可传多个参数，会依次拼接
- 版本 : 1.0.0


```javascript
$log.i("信息");
```


### info(args)

> 打印一条"信息"级别的日志。
> 

- 参数 : args {string...} 要打印的内容，可传多个参数，会依次拼接
- 版本 : 1.0.0


```javascript
$log.info("信息");
```


### d(args)

> 打印一条"调试"级别的日志（debug 的简写）。
> 

- 参数 : args {string...} 要打印的调试内容，可传多个参数
- 版本 : 1.0.0


```javascript
$log.d("调试");
```


### debug(args)

> 打印一条"调试"级别的日志。
> 

- 参数 : args {string...} 要打印的调试内容，可传多个参数
- 版本 : 1.2.8


```javascript
$log.debug("调试");
```


### w(args)

> 打印一条"警告"级别的日志（warn 的简写）。
> 

- 参数 : args {string...} 要打印的警告内容，可传多个参数
- 版本 : 1.0.0


```javascript
$log.w("警告");
```


### warn(args)

> 打印一条"警告"级别的日志。
> 

- 参数 : args {string...} 要打印的警告内容，可传多个参数
- 版本 : 1.2.8


```javascript
$log.warn("警告");
```


### e(args)

> 打印一条"错误"级别的日志（err 的简写）。
> 

- 参数 : args {string...} 要打印的错误内容，可传多个参数
- 版本 : 1.0.0


```javascript
$log.e("异常");
```


### err(args)

> 打印一条"错误"级别的日志。
> 

- 参数 : args {string...} 要打印的错误内容，可传多个参数
- 版本 : 1.2.8


```javascript
$log.err("异常");
```


### v(args)

> 打印一条"啰嗦/最详细"级别的日志（verbose）。
> 

- 参数 : args {string...} 要打印的详细内容，可传多个参数
- 版本 : 1.0.0


```javascript
$log.v("冗余");
```


### log(args)

> 打印一条普通日志（效果和 info 一样，只是换个短名字）。
> 

- 参数 : args {string...} 要打印的内容，可传多个参数
- 版本 : 1.0.0


```javascript
$log.log("hello");
```


### print(args)

> 打印一条普通日志（效果和 info 一样）。

- 参数 : args {string...} 要打印的内容，可传多个参数
- 版本 : 1.2.0


```javascript
$log.print("hello");
```


### floaty()

> 打开日志悬浮窗

- 版本 : 1.0.0


```javascript
$log.floaty();
```


### closeFloaty()

> 关闭日志悬浮窗。
> 

- 版本 : 1.8.6


```javascript
$log.closeFloaty();
```


### activity()

> 打开日志界面

- 版本 : 1.1.2


```javascript
$log.activity();
```


### delete()

> 清空本地保存的日志缓存文件。
> 

- 版本 : 1.0.6


```javascript
$log.delete();
```


