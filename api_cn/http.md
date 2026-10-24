# $http - 网络请求

- 更新时间:2026-10-22 10:55:49

> 网络请求对象（脚本里写作 $http），用来向服务器发 HTTP 请求（GET/POST/PUT/DELETE 等）并读取返回结果。
> 
> 它底层用 OkHttp 实现，会自动信任所有证书（方便访问自签名 https 站点）。
> 最常见的用法是 $http.get(网址) 或 $http.post({...配置...})，拿到一个 HttpResponse 响应对象，
> 再用它的 str() 读回的文字、json() 把回的 JSON 转成对象。
> 
> 注意：这些请求方法是“同步阻塞”的——网络慢时会卡住当前脚本，等服务器回应后才继续往下走。
> 请求在调用线程同步执行，网络较慢时会阻塞当前脚本；需要网络连接且目标地址可访问。



```javascript
//最简单的 GET 请求
var response = $http.get("https://example.com/");
if (response.isSuccess()) {
    log("返回内容：" + response.str());
}
```




## 基础用法


最基础的 POST 请求示例：带请求头、发一段 JSON 数据。
示例地址和鉴权值需要替换为自己的接口配置；这里只展示脚本写法。


```html
//向服务器 POST 一段 JSON 数据
var resp = $http.post({
    url: "https://example.com/api/login",  //请求地址
    head: {                                 //自定义请求头
        "Authorization": "Bearer xxxxx"
    },
    //数据直接写js对象格式即可，会自动转成 JSON 发送
    data: {
        user: "kodesh",
        pwd: "123456"
    }
});
if (resp.isSuccess()) {
    var text = resp.str(); //正文读取一次，将结果保存下来
    log("响应正文：" + text);
} else {
    log("请求失败：" + resp.getStatusCode() + "，" + resp.getDesc());
}
```


POST 发送一段普通字符串（不是 JSON）的示例。
示例地址和鉴权值需要替换为自己的接口配置；这里只展示脚本写法。


```html
//data 直接传一个字符串，会按纯文本发给服务器
var resp = $http.post({
    url: "https://example.com/api/echo",  //请求地址
    head: {                               //自定义请求头
        "Content-Type": "text/plain"
    },
    data: "这是一段普通文字"                 //直接传字符串
});
if (resp.isSuccess()) {
    var text = resp.str(); //正文读取一次，将结果保存下来
    log("响应正文：" + text);
} else {
    log("请求失败：" + resp.getStatusCode() + "，" + resp.getDesc());
}
```


### 示例-发送表单数据
示例地址和鉴权值需要替换为自己的接口配置；这里只展示脚本写法。


```html
//用 form 字段发送表单（application/x-www-form-urlencoded）
var resp = $http.post({
    url: "https://example.com/api/form",  //请求地址
    head: {                               //自定义请求头
        "Token": "abcdef"
    },
    form: {                               //表单字段，会按键值对提交
        username: "kodesh",
        age: "26"
    }
});
if (resp.isSuccess()) {
    var text = resp.str(); //正文读取一次，将结果保存下来
    log("响应正文：" + text);
} else {
    log("请求失败：" + resp.getStatusCode() + "，" + resp.getDesc());
}
```


### 示例-发送表单且文件
示例地址和鉴权值需要替换为自己的接口配置；这里只展示脚本写法。


```html
//例如发送的表单中含有一个头像图片
var resp = $http.post({
    url: "https://example.com/api/upload", //请求地址
    head: {                               //自定义请求头
        "Token": "abcdef"
    },
    //如果表单含文件，则用路径作为值，例如下面上传头像
    form: {
        nickname: "kodesh",               //普通表单字段
        avatar: "/sdcard/Pictures/head.jpg" //路径必须存在；存在时按文件上传，否则按文字发送
    }
});
if (resp.isSuccess()) {
    var text = resp.str(); //接收并消费一次响应正文
    log("响应正文：" + text);
} else {
    log("请求失败：" + resp.getDesc());
}
```


### 示例-发送单个文件
示例地址和鉴权值需要替换为自己的接口配置；这里只展示脚本写法。


```html
//通过名为 file 的表单项上传一个文件（data 传存在的文件路径）
var resp = $http.post({
    url: "https://example.com/api/file",  //请求地址
    head: {                               //自定义请求头
        "Token": "abcdef"
    },
    data: "/sdcard/Pictures/head.jpg"      //值是一个存在的文件路径，就会上传该文件
});
if (resp.isSuccess()) {
    var text = resp.str(); //正文读取一次，将结果保存下来
    log("响应正文：" + text);
} else {
    log("请求失败：" + resp.getStatusCode() + "，" + resp.getDesc());
}
```


### 示例-发送二进制
示例地址和鉴权值需要替换为自己的接口配置；这里只展示脚本写法。


```html
//例如发送一段二进制字符串: "我会被转换成二进制"
var resp = $http.post({
    url: "https://example.com/api/bin",  //请求地址
    head: {                               //自定义请求头
        "Token": "abcdef"
    },
    type: "byte",                         //声明按二进制发送
    data: "我会被转换成二进制"             //这段文字会被转成字节发出
});
if (resp.isSuccess()) {
    var text = resp.str(); //正文读取一次，将结果保存下来
    log("响应正文：" + text);
} else {
    log("请求失败：" + resp.getStatusCode() + "，" + resp.getDesc());
}
```


## 常用函数


### uri(uri)

> 把一段网址字符串解析成一个 Uri（统一资源定位符）对象。
> 
> 一般用于和安卓原生意图（Intent）配合，比如跳转拨号、发短信等。传 null 会返回 null。

- 参数 : uri {CharSequence} 要解析的网址字符串，例如 "smsto:10086"
- 返回 : {Uri} 解析得到的 Uri 对象；传 null 时返回 null
- 版本 : 1.3.7


```javascript
//构造一个"发短信"的 Uri，号码先做 URL 编码
var uri = $http.uri("smsto:" + $str.uriEncode("13693749475"));
log("解析后的地址：" + uri);
```


### get(url)

> 同步发起 GET 网络请求，并取得 HttpResponse 响应对象。
> 输入：String 字符串，填写请求网址。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> 当前实现不发送 data 或 form 正文；需要传查询条件时请按接口要求放到网址中。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : url {String} 请求地址，建议明确写出 http:// 或 https:// 协议
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var resp = $http.get("https://example.com/"); //最简形式，只传网址
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### get(opts)

> 同步发起 GET 网络请求，并取得 HttpResponse 响应对象。
> 输入：Object 配置对象，按照 HttpOptions 的字段填写；url 是必填地址，head 是字符串请求头对象，超时配置使用秒。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> 当前实现不发送 data 或 form 正文；需要传查询条件时请按接口要求放到网址中。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : opts {Object} 按 HttpOptions 结构填写的配置对象，至少包含 url
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var options = {
        url: "https://example.com/api/resource/1", //替换实际接口地址
        head: {"Accept": "application/json"}, //可选，请求服务器返回对象数据
        connectTimeout: 15, //连接等待时间，单位为秒
        callTimeout: 30 //整个调用的最长等待秒数
    };
    var resp = $http.get(options); //返回 HttpResponse，不是正文字符串
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### post(opts)

> 同步发起 POST 网络请求，并取得 HttpResponse 响应对象。
> 输入：Object 配置对象，按照 HttpOptions 的字段填写；url 是必填地址，head 是字符串请求头对象，超时配置使用秒。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> data 可填写对象或文字，form 可填写表单对象；两者建议只选一种。没有可用正文时，请求不会发出，返回的成功标志为假。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : opts {Object} 按 HttpOptions 结构填写的配置对象，至少包含 url
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var options = {
        url: "https://example.com/api/resource/1", //替换实际接口地址
        head: {"Accept": "application/json"}, //可选，请求服务器返回对象数据
        connectTimeout: 15, //连接等待时间，单位为秒
        callTimeout: 30, //整个调用的最长等待秒数
        data: {name: "小明"} //具体属性名和内容由服务端接口规定
    };
    var resp = $http.post(options); //返回 HttpResponse，不是正文字符串
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### del(opts)

> 同步发起 DELETE 网络请求，并取得 HttpResponse 响应对象。
> 输入：Object 配置对象，按照 HttpOptions 的字段填写；url 是必填地址，head 是字符串请求头对象，超时配置使用秒。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> 当前实现不发送 data 或 form 正文；需要传查询条件时请按接口要求放到网址中。
> del 和 delete 只是同一功能的两种名称。删除是否生效由服务器决定，示例中资源编号需要换成自己要操作的目标。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : opts {Object} 按 HttpOptions 结构填写的配置对象，至少包含 url
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var options = {
        url: "https://example.com/api/resource/1", //替换实际接口地址
        head: {"Accept": "application/json"}, //可选，请求服务器返回对象数据
        connectTimeout: 15, //连接等待时间，单位为秒
        callTimeout: 30 //整个调用的最长等待秒数
    };
    var resp = $http.del(options); //返回 HttpResponse，不是正文字符串
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### delete(opts)

> 同步发起 DELETE 网络请求，并取得 HttpResponse 响应对象。
> 输入：Object 配置对象，按照 HttpOptions 的字段填写；url 是必填地址，head 是字符串请求头对象，超时配置使用秒。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> 当前实现不发送 data 或 form 正文；需要传查询条件时请按接口要求放到网址中。
> del 和 delete 只是同一功能的两种名称。删除是否生效由服务器决定，示例中资源编号需要换成自己要操作的目标。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : opts {Object} 按 HttpOptions 结构填写的配置对象，至少包含 url
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var options = {
        url: "https://example.com/api/resource/1", //替换实际接口地址
        head: {"Accept": "application/json"}, //可选，请求服务器返回对象数据
        connectTimeout: 15, //连接等待时间，单位为秒
        callTimeout: 30 //整个调用的最长等待秒数
    };
    var resp = $http.delete(options); //返回 HttpResponse，不是正文字符串
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### put(opts)

> 同步发起 PUT 网络请求，并取得 HttpResponse 响应对象。
> 输入：Object 配置对象，按照 HttpOptions 的字段填写；url 是必填地址，head 是字符串请求头对象，超时配置使用秒。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> data 可填写对象或文字，form 可填写表单对象；两者建议只选一种。没有可用正文时，请求不会发出，返回的成功标志为假。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : opts {Object} 按 HttpOptions 结构填写的配置对象，至少包含 url
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var options = {
        url: "https://example.com/api/resource/1", //替换实际接口地址
        head: {"Accept": "application/json"}, //可选，请求服务器返回对象数据
        connectTimeout: 15, //连接等待时间，单位为秒
        callTimeout: 30, //整个调用的最长等待秒数
        data: {name: "小明"} //具体属性名和内容由服务端接口规定
    };
    var resp = $http.put(options); //返回 HttpResponse，不是正文字符串
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### patch(opts)

> 同步发起 PATCH 网络请求，并取得 HttpResponse 响应对象。
> 输入：Object 配置对象，按照 HttpOptions 的字段填写；url 是必填地址，head 是字符串请求头对象，超时配置使用秒。
> 输出：HttpResponse，里面包含成功标志、状态码、说明文字和正文读取方法。
> 请求会阻塞调用线程，直到得到响应或发生异常；应在脚本工作线程调用，不要放进界面线程回调。
> data 可填写对象或文字，form 可填写表单对象；两者建议只选一种。没有可用正文时，请求不会发出，返回的成功标志为假。
> 取得成功响应后，只选 str()、string()、json() 或 bytes() 其中一种读取一次，并保存结果。
> 失败时优先查看 getStatusCode() 和 getDesc()；部分请求参数错误会直接抛出异常，可以用 try/catch 处理。
> 示例地址只说明写法，实际执行请换成自己有权访问或操作的接口。

- 参数 : opts {Object} 按 HttpOptions 结构填写的配置对象，至少包含 url
- 返回 : {HttpResponse} 响应结果；通过 isSuccess() 判断网络响应是否成功
- 版本 : 1.2.0


```javascript
try {
    var options = {
        url: "https://example.com/api/resource/1", //替换实际接口地址
        head: {"Accept": "application/json"}, //可选，请求服务器返回对象数据
        connectTimeout: 15, //连接等待时间，单位为秒
        callTimeout: 30, //整个调用的最长等待秒数
        data: {name: "小明"} //具体属性名和内容由服务端接口规定
    };
    var resp = $http.patch(options); //返回 HttpResponse，不是正文字符串
    if (resp.isSuccess()) {
        var text = resp.str(); //只读取一次正文
        log("响应状态码：" + resp.getStatusCode());
        log("响应正文：" + text);
    } else {
        log("请求失败，状态码：" + resp.getStatusCode());
        log("失败说明：" + resp.getDesc());
    }
} catch (error) {
    log("请求参数或正文读取发生异常：" + error);
}
```


### download(url, savePath)

> 在后台下载文件并保存到指定路径。
> 输入：String 网址和 String 完整保存路径。
> 输出：void，不返回文件对象；方法返回并不代表下载已经结束。
> 保存路径要包含文件名，父目录必须已经存在并具有写入权限；已有同名文件会被覆盖。网址和路径为空时会记录提示并直接返回。
> 当前下载器复用首次创建的客户端及其进度监听器；连续或并发下载时，后续下载的进度和完成通知可能仍关联首次监听器，不宜用本例推断多个下载任务能独立通知。
> 示例网址需要换成自己的文件地址；请先确认示例保存目录存在。

- 参数 : url {String} 文件网址，不可为空
- 参数 : savePath {String} 本地完整路径，父目录需存在；同名文件会被覆盖


```javascript
//示例仅发起一次下载；请先准备保存目录并替换文件网址
$http.download(
    "https://example.com/archive.zip", //服务器上的文件地址
    "/sdcard/Download/archive.zip" //有写入权限的完整保存路径
);
log("下载已安排，脚本会继续执行"); //此时不能假设文件已经保存完成
```


### download(url, savePath, completeCallback)

> 在后台下载文件并保存到指定路径。
> 输入：String 网址和 String 完整保存路径，以及下载过程中使用的回调函数。
> 输出：void，不返回文件对象；方法返回并不代表下载已经结束。
> 保存路径要包含文件名，父目录必须已经存在并具有写入权限；已有同名文件会被覆盖。网址和路径为空时会记录提示并直接返回。
> completeCallback 是无参数的 Runnable 回调，用 function () {...} 提供，回调没有返回值。当前实现根据响应流读到末尾的通知触发它，不代表文件流已经完成关闭。
> 当前下载器复用首次创建的客户端及其进度监听器；连续或并发下载时，后续下载的进度和完成通知可能仍关联首次监听器，不宜用本例推断多个下载任务能独立通知。
> 示例网址需要换成自己的文件地址；请先确认示例保存目录存在。

- 参数 : url {String} 文件网址，不可为空
- 参数 : savePath {String} 本地完整路径，父目录需存在；同名文件会被覆盖
- 参数 : completeCallback {Runnable} 无参数、无返回值的响应流结束回调；可传 null


```javascript
//示例仅发起一次下载；请先准备保存目录并替换文件网址
$http.download(
    "https://example.com/archive.zip", //服务器上的文件地址
    "/sdcard/Download/archive.zip", //有写入权限的完整保存路径
    function () { //没有参数；这是读到响应流末尾的通知
        log("已收到响应流结束通知");
    }
);
log("下载已安排，脚本会继续执行"); //此时不能假设文件已经保存完成
```


### download(url, savePath, completeCallback, onFailure)

> 在后台下载文件并保存到指定路径。
> 输入：String 网址和 String 完整保存路径，以及下载过程中使用的回调函数。
> 输出：void，不返回文件对象；方法返回并不代表下载已经结束。
> 保存路径要包含文件名，父目录必须已经存在并具有写入权限；已有同名文件会被覆盖。网址和路径为空时会记录提示并直接返回。
> completeCallback 是无参数的 Runnable 回调，用 function () {...} 提供，回调没有返回值。当前实现根据响应流读到末尾的通知触发它，不代表文件流已经完成关闭。
> onFailure 是 SimpleStringCallback 回调，用 function (message) {...} 接收 String 失败说明，不需要返回值。不要假设每一种配置错误都会进入这个回调。
> 当前下载器复用首次创建的客户端及其进度监听器；连续或并发下载时，后续下载的进度和完成通知可能仍关联首次监听器，不宜用本例推断多个下载任务能独立通知。
> 示例网址需要换成自己的文件地址；请先确认示例保存目录存在。

- 参数 : url {String} 文件网址，不可为空
- 参数 : savePath {String} 本地完整路径，父目录需存在；同名文件会被覆盖
- 参数 : completeCallback {Runnable} 无参数、无返回值的响应流结束回调；可传 null
- 参数 : onFailure {SimpleStringCallback} 接收 String 失败说明、无返回值的回调；可传 null


```javascript
//示例仅发起一次下载；请先准备保存目录并替换文件网址
$http.download(
    "https://example.com/archive.zip", //服务器上的文件地址
    "/sdcard/Download/archive.zip", //有写入权限的完整保存路径
    function () { //没有参数；这是读到响应流末尾的通知
        log("已收到响应流结束通知");
    },
    function (message) { //参数是失败原因的文字
        log("下载失败：" + message);
    }
);
log("下载已安排，脚本会继续执行"); //此时不能假设文件已经保存完成
```


### download(url, savePath, progressListener, completeCallback, onFailure)

> 在后台下载文件并保存到指定路径。
> 输入：String 网址和 String 完整保存路径，以及下载过程中使用的回调函数。
> 输出：void，不返回文件对象；方法返回并不代表下载已经结束。
> 保存路径要包含文件名，父目录必须已经存在并具有写入权限；已有同名文件会被覆盖。网址和路径为空时会记录提示并直接返回。
> completeCallback 是无参数的 Runnable 回调，用 function () {...} 提供，回调没有返回值。当前实现根据响应流读到末尾的通知触发它，不代表文件流已经完成关闭。
> onFailure 是 SimpleStringCallback 回调，用 function (message) {...} 接收 String 失败说明，不需要返回值。不要假设每一种配置错误都会进入这个回调。
> progressListener 是 DownloadProgress 回调，写成 function (current, total, percent) {...}。current、total 是 long 字节数量，percent 是带百分号的 String 文字；函数不需要返回值。
> 服务器没有提供总长度时，不会调用百分比进度回调。各回调可能在后台执行，若需操作界面控件，请通过 $thread.ui 切回界面线程。
> 当前下载器复用首次创建的客户端及其进度监听器；连续或并发下载时，后续下载的进度和完成通知可能仍关联首次监听器，不宜用本例推断多个下载任务能独立通知。
> 示例网址需要换成自己的文件地址；请先确认示例保存目录存在。

- 参数 : url {String} 文件网址，不可为空
- 参数 : savePath {String} 本地完整路径，父目录需存在；同名文件会被覆盖
- 参数 : progressListener {DownloadProgress} 进度回调，接收 long 已读字节、long 总字节、String 百分比；可传 null
- 参数 : completeCallback {Runnable} 无参数、无返回值的响应流结束回调；可传 null
- 参数 : onFailure {SimpleStringCallback} 接收 String 失败说明、无返回值的回调；可传 null


```javascript
//示例仅发起一次下载；请先准备保存目录并替换文件网址
$http.download(
    "https://example.com/archive.zip", //服务器上的文件地址
    "/sdcard/Download/archive.zip", //有写入权限的完整保存路径
    function (current, total, percent) { //每次收到已知总长度的进度时执行
        log("下载进度：" + percent);
        log("已读取字节：" + current + "，总字节：" + total);
    },
    function () { //没有参数；这是读到响应流末尾的通知
        log("已收到响应流结束通知");
    },
    function (message) { //参数是失败原因的文字
        log("下载失败：" + message);
    }
);
log("下载已安排，脚本会继续执行"); //此时不能假设文件已经保存完成
```


### wifiIp()

> 获取当前设备连接的 WiFi 的局域网 IP 地址。
> 
> 返回手机在当前 WiFi 局域网里分到的 IP（例如 "192.168.1.5"）。没连 WiFi 或获取不到时可能返回 null 或空。

- 返回 : {string} 当前 WiFi 的局域网 IP 地址；获取不到时返回 null 或空串


```javascript
//查看本机在 WiFi 下的 IP
var result = $http.wifiIp();
log("本机 WiFi IP：" + result);
```


