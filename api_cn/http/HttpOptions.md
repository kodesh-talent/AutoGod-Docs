# 

- 更新时间:2026-10-22 10:55:49

> 网络请求的配置说明，供 $http 的请求方法读取。
> 在脚本中使用普通对象填写配置，不要直接访问本类的私有字段。
> url 必填；其余未填写的项目使用默认值。请求正文使用 data 或 form；超时参数的单位统一为秒。
> 示例地址只展示配置写法，实际运行请替换成自己的服务器地址。



```javascript
var options = { //先准备配置对象
    url: "https://example.com/", //请求地址
    connectTimeout: 15, //建立连接最多等待十五秒
    callTimeout: 30 //整个调用最多等待三十秒
};
var resp = $http.get(options); //同步请求，等待结果
if (resp.isSuccess()) {
    var text = resp.str(); //只读取一次正文，再重复使用保存的文字
    log("正文：" + text);
} else {
    log("请求失败：" + resp.getDesc());
}
```




### const {String} url;

> 请求地址，必填。默认值为 null。
> 配置值类型：String。请传入完整的网络地址。省略协议时当前实现会补 http://，但示例建议明确写出所需协议。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/" //换成实际网址
};
var resp = $http.get(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Map<String,String>} head;

> 请求头，默认是空映射表。
> 配置值类型：Map<String, String>。脚本中写成对象：属性名是请求头名称，属性值用字符串。值为 null 的项会跳过；鉴权内容请替换成自己的有效值。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    head: {"Accept": "application/json"} //告诉服务器希望取得对象数据
};
var resp = $http.get(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Object} data;

> 请求正文，默认是 null。
> 配置值类型：Object。普通对象通常会序列化为对象数据；字符串会依次判断为标记文本、存在的文件路径、对象数据字符串或普通文字。存在的文件路径会按名为 file 的文件表单项上传。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 当前 get 和 delete 不发送这里构建的正文；post、put、patch 需要可用的请求正文。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    data: {name: "小明", age: 18} //向服务器提交对象数据
};
var resp = $http.post(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Object} form;

> 表单正文，默认是 null。
> 配置值类型：Object。脚本中传入键值对象。不含文件时使用普通表单；值为存在的文件路径时会构建含文件的表单。路径不存在会按普通文字提交，不代表文件上传成功。有效 form 会覆盖 data 生成的正文，建议二者只填一个。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 当前 get 和 delete 不发送这里构建的正文；post、put、patch 需要可用的请求正文。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    form: {name: "小明", age: "18"} //普通表单字段，按接口要求填写
};
var resp = $http.post(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {String} type;

> 正文构建方式，默认是 "string"。
> 配置值类型：String。"byte" 表示把文本按 UTF-8 编码为字节后构建正文；不是指定服务器返回类型，也不是将响应自动转换成字节数组。其他值在当前分支中按字符串处理，建议只使用 "string" 或 "byte"。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    type: "byte", //本次将文本按字节构建请求正文
    data: "这是一段待发送的文字" //仍由内容决定正文媒体类型
};
var resp = $http.post(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Integer} connectTimeout;

> 连接超时，默认 30 秒。
> 配置值类型：Integer。限制建立连接时的等待时间。单位是秒，不是毫秒；传非负整数，零表示不设置这一项超时限制。不要填 null 或负数。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    connectTimeout: 15 //这项最多等待十五秒
};
var resp = $http.get(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Integer} readTimeout;

> 读取超时，默认 30 秒。
> 配置值类型：Integer。限制读取数据时的等待，并不等同于整个请求的总时长。单位是秒，不是毫秒；传非负整数，零表示不设置这一项超时限制。不要填 null 或负数。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    readTimeout: 15 //这项最多等待十五秒
};
var resp = $http.get(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Integer} writeTimeout;

> 写入超时，默认 30 秒。
> 配置值类型：Integer。限制向服务器写出数据时的等待，并不等同于整个请求的总时长。单位是秒，不是毫秒；传非负整数，零表示不设置这一项超时限制。不要填 null 或负数。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    writeTimeout: 15 //这项最多等待十五秒
};
var resp = $http.get(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### const {Integer} callTimeout;

> 整个调用超时，默认 60 秒。
> 配置值类型：Integer。限制整个请求调用的总用时，包括连接、发送和读取等阶段。单位是秒，不是毫秒；传非负整数，零表示不设置这一项超时限制。不要填 null 或负数。
> 这是配置对象的键名，在普通脚本对象中填写；不是让脚本直接读写同名私有字段。
> 示例网址和接口字段需要按实际服务修改；网络请求应在脚本工作线程执行。


```javascript
var options = {
    url: "https://example.com/api", //实际使用时替换接口地址
    callTimeout: 15 //这项最多等待十五秒
};
var resp = $http.get(options); //提交配置，取得 HttpResponse 响应对象
if (resp.isSuccess()) {
    var text = resp.str(); //选一种正文读取方式，只读取一次
    log("响应正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


