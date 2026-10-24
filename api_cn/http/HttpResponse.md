# HttpResponse - 网络请求响应体

- 更新时间:2026-10-22 10:55:49

> 网络请求的响应结果对象（用 $http.get / $http.post 等请求后返回）。
> 
> 当你向一个网址发起请求后，服务器会回给你一段内容。这个对象就是把“服务器的回应”打包好交给你：
> 有没有成功、状态码是多少、回的文字是什么、回的内容能不能直接当 JSON 读，都在这里面。
> 
> 新手提示：拿到响应后先看 isSuccess() 是否成功，再用 str() 读回的文字，或用 json() 把回的 JSON 转成对象。
> 常见状态码：200 表示成功，404 表示页面不存在，500 表示服务器出错。



```javascript
//向一个网址发起 GET 请求，得到响应对象
var resp = $http.get("https://example.com/");
//先判断这次请求是否成功
if (resp.isSuccess()) {
    log("状态码：" + resp.getStatusCode());   //例如 200
    log("返回内容：" + resp.str());            //读取回的文字
} else {
    log("请求失败：" + resp.getDesc());
}
```




### const {Response} response;

> 内部保存的底层网络响应，默认是 null。
> 属性类型：Response。这是私有字段，不应在脚本中直接写 resp.response。请使用公开的状态查询和正文读取方法。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
if (resp.isSuccess()) {
    log("状态码：" + resp.getStatusCode());
    var text = resp.str(); //通过公开方法读取，不访问私有字段
    log("正文：" + text);
} else {
    log("请求未成功：" + resp.getDesc());
}
```


### const {String} desc;

> 请求过程的说明文字，默认是 null。
> 属性类型：String。网络异常或非成功状态通常会写入失败说明；成功请求也可能保持 null，不要把没有说明当成失败。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.desc); //读取结果字段，不要给它赋值冒充请求成功
```


### const {boolean} success;

> 本次请求是否取得成功状态的响应，默认是假值 false。
> 属性类型：boolean。true 表示网络响应状态在成功范围内，并不证明接口业务成功，也不保证正文一定是可解析的对象。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.success); //读取结果字段，不要给它赋值冒充请求成功
if (resp.success) {
    var text = resp.str(); //成功后选择一种方式读取正文
    log("正文：" + text);
} else {
    log("失败原因：" + resp.desc);
}
```


### const {int} statusCode;

> 响应状态码，默认是零。
> 属性类型：int。当前请求实现中，成功响应会同时填入 statusCode、status、code；非成功状态只填入 statusCode，另外两个可能仍为零。排查失败时优先读取 getStatusCode()。零表示没有记录到状态码，并非服务器返回成功。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.statusCode); //读取结果字段，不要给它赋值冒充请求成功
```


### const {int} status;

> 简写状态码字段，默认是零。
> 属性类型：int。当前请求实现中，成功响应会同时填入 statusCode、status、code；非成功状态只填入 statusCode，另外两个可能仍为零。排查失败时优先读取 getStatusCode()。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.status); //读取结果字段，不要给它赋值冒充请求成功
log("排查错误时的状态码：" + resp.getStatusCode()); //失败时以此项为准
```


### const {int} code;

> 另一种简写状态码字段，默认是零。
> 属性类型：int。当前请求实现中，成功响应会同时填入 statusCode、status、code；非成功状态只填入 statusCode，另外两个可能仍为零。排查失败时优先读取 getStatusCode()。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.code); //读取结果字段，不要给它赋值冒充请求成功
log("排查错误时的状态码：" + resp.getStatusCode()); //失败时以此项为准
```


### const {String} statusMessage;

> 服务器返回的状态说明文字，默认是 null。
> 属性类型：String。当前请求实现中，成功响应会同时填入 statusMessage 和 msg；非成功状态只填入 statusMessage，msg 可能仍为空。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.statusMessage); //读取结果字段，不要给它赋值冒充请求成功
```


### const {String} msg;

> 状态说明文字的简写字段，默认是 null。
> 属性类型：String。当前请求实现中，成功响应会同时填入 statusMessage 和 msg；非成功状态只填入 statusMessage，msg 可能仍为空。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.msg); //读取结果字段，不要给它赋值冒充请求成功
log("完整状态说明：" + resp.getStatusMessage()); //失败时优先读取此项
```


### const {String} method;

> 本次请求采用的方法名称，默认是 null。
> 属性类型：String。当前 $http 调用通常记录小写的 get、post、put、patch 或 delete；请求配置尚未解析时可能没有值。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.method); //读取结果字段，不要给它赋值冒充请求成功
```


### const {String} url;

> 本次配置的请求地址，默认是 null。
> 属性类型：String。记录的是配置中传入的地址，不一定是补全协议或重定向后的最终地址。
> 这是请求返回的结果字段，通常只读取；手动修改只改变这个对象，不会重新请求服务器，也不会自动同步其他字段。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
log("字段值：" + resp.url); //读取结果字段，不要给它赋值冒充请求成功
```


### const {String} str;

> 帮助提示字段，类型为 String 字符串。
> 字段内容只是提醒你调用同名方法，不是服务器返回的正文；不要修改它。
> 读取实际内容时需要方法名后的圆括号。正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
if (resp.isSuccess()) {
    var text = resp.str(); //带圆括号才是读取正文的方法
    log("正文：" + text);
}
```


### const {String} string;

> 帮助提示字段，类型为 String 字符串。
> 字段内容只是提醒你调用同名方法，不是服务器返回的正文；不要修改它。
> 读取实际内容时需要方法名后的圆括号。正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
if (resp.isSuccess()) {
    var text = resp.string(); //带圆括号才是读取正文的方法
    log("正文：" + text);
}
```


### const {String} json;

> 帮助提示字段，类型为 String 字符串。
> 字段内容只是提醒你调用同名方法，不是服务器返回的正文；不要修改它。
> 读取实际内容时需要方法名后的圆括号。正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/api/user"); //换成返回对象结构的接口
if (resp.isSuccess()) {
    var data = resp.json(); //调用方法，不读取同名提示字段
    if (data != null) {
        log("名字：" + data.get("name")); //返回的是映射表，用键名取值
    }
}
```


### const {String} bytes;

> 帮助提示字段，类型为 String 字符串。
> 字段内容只是提醒你调用同名方法，不是服务器返回的正文；不要修改它。
> 读取实际内容时需要方法名后的圆括号。正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
if (resp.isSuccess()) {
    var data = resp.bytes(); //调用方法，得到字节数组或 null
    if (data != null) {
        log("字节数：" + data.length); //先检查不为空再读取长度
    }
}
```


### getStatusCode()

> 响应状态码，默认是零。
> 输入：无参数。输出：int，读取 statusCode 字段的当前值。
> 当前请求实现中，成功响应会同时填入 statusCode、status、code；非成功状态只填入 statusCode，另外两个可能仍为零。排查失败时优先读取 getStatusCode()。零表示没有记录到状态码，并非服务器返回成功。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {int} 响应状态码，默认是零。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getStatusCode(); //调用无参数方法读取结果
log("读取结果：" + value);
```


### getStatusMessage()

> 服务器返回的状态说明文字，默认是 null。
> 输入：无参数。输出：String，读取 statusMessage 字段的当前值。
> 当前请求实现中，成功响应会同时填入 statusMessage 和 msg；非成功状态只填入 statusMessage，msg 可能仍为空。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 服务器返回的状态说明文字，默认是 null。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getStatusMessage(); //调用无参数方法读取结果
log("读取结果：" + value);
```


### str()

> 把服务器的响应正文读取为文字。
> 输入：无参数。输出：String 字符串；没有保存底层响应或响应体时返回 null，空正文也可能返回空字符串。
> 正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 读取时发生输入输出异常会抛出运行异常；请求失败时，本实现没有保存失败响应体，因此不能靠此方法读取错误页。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 正文文字；未保存响应或没有响应体时为 null


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
if (resp.isSuccess()) {
    try {
        var text = resp.str(); //只调用一次，保留返回值
        if (text != null) {
            log("正文：" + text);
            log("再次使用已保存的文字：" + text); //不再次读取响应体
        }
    } catch (error) {
        log("读取正文失败：" + error);
    }
} else {
    log("请求失败：" + resp.getDesc());
}
```


### string()

> 把服务器的响应正文读取为文字。
> 输入：无参数。输出：String 字符串；没有保存底层响应或响应体时返回 null，空正文也可能返回空字符串。
> 正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 读取时发生输入输出异常会抛出运行异常；请求失败时，本实现没有保存失败响应体，因此不能靠此方法读取错误页。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 正文文字；未保存响应或没有响应体时为 null


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
if (resp.isSuccess()) {
    try {
        var text = resp.string(); //只调用一次，保留返回值
        if (text != null) {
            log("正文：" + text);
            log("再次使用已保存的文字：" + text); //不再次读取响应体
        }
    } catch (error) {
        log("读取正文失败：" + error);
    }
} else {
    log("请求失败：" + resp.getDesc());
}
```


### json()

> 将响应正文解析为按名称取值的映射表。
> 输入：无参数。输出：Map 映射表；它是宿主映射对象，示例用 get("键名") 读取其中的值。
> 服务端需要返回对象结构，例如包含 name 属性的对象；数组、普通网页、空内容或无法解析的内容可能得到 null。
> 正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 读取正文时的输入输出异常会抛出运行异常；解析失败返回 null。不要先调用 str() 再调用本方法。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {Map} 解析得到的映射表；内容为空或不能解析为映射表时为 null


```javascript
var resp = $http.get("https://example.com/api/user"); //换成返回对象结构的实际接口
if (resp.isSuccess()) {
    try {
        var data = resp.json(); //直接解析，只消费一次正文
        if (data != null) {
            var name = data.get("name"); //假设接口提供 name；没有该键时得到 null
            log("名字：" + name);
        } else {
            log("正文不是可解析的对象，或正文为空");
        }
    } catch (error) {
        log("读取正文时发生异常：" + error);
    }
} else {
    log("请求失败：" + resp.getDesc());
}
```


### bytes()

> 将响应正文一次性读入字节数组，适合读取图片等二进制内容。
> 输入：无参数。输出：byte[] 字节数组；没有保存底层响应或响应体时返回 null。
> 正文只允许选一种方式读取一次：str()、string()、json()、bytes() 共用同一个响应体，读取后会消耗并关闭它。需要重复使用时，请保存第一次读取的结果。
> 数组的 length 是字节数量，不是图片宽度或字符个数。所有内容会读进内存，大文件可使用 $http.download 保存。
> 读取时发生输入输出异常会抛出运行异常。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {byte[]} 正文的字节数组；没有底层响应或响应体时为 null


```javascript
var resp = $http.get("https://example.com/pic.png"); //换成实际图片地址
if (resp.isSuccess()) {
    try {
        var data = resp.bytes(); //正文只读一次
        if (data != null) {
            log("下载字节数：" + data.length); //不为空时才能访问长度
            if (data.length > 0) {
                log("第一个字节的无符号值：" + (data[0] & 255)); //将有符号字节转成零到二百五十五
            }
        }
    } catch (error) {
        log("读取字节失败：" + error);
    }
} else {
    log("请求失败：" + resp.getDesc());
}
```


### getDesc()

> 请求过程的说明文字，默认是 null。
> 输入：无参数。输出：String，读取 desc 字段的当前值。
> 网络异常或非成功状态通常会写入失败说明；成功请求也可能保持 null，不要把没有说明当成失败。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 请求过程的说明文字，默认是 null。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getDesc(); //调用无参数方法读取结果
log("读取结果：" + value);
```


### isSuccess()

> 本次请求是否取得成功状态的响应，默认是假值 false。
> 输入：无参数。输出：boolean，读取 success 字段的当前值。
> true 表示网络响应状态在成功范围内，并不证明接口业务成功，也不保证正文一定是可解析的对象。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {boolean} 本次请求是否取得成功状态的响应，默认是假值 false。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.isSuccess(); //调用无参数方法读取结果
log("读取结果：" + value);
if (value) {
    var text = resp.str(); //取得成功响应后，将正文保存下来
    log("正文：" + text);
} else {
    log("状态码：" + resp.getStatusCode());
    log("失败说明：" + resp.getDesc());
}
```


### getMethod()

> 本次请求采用的方法名称，默认是 null。
> 输入：无参数。输出：String，读取 method 字段的当前值。
> 当前 $http 调用通常记录小写的 get、post、put、patch 或 delete；请求配置尚未解析时可能没有值。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 本次请求采用的方法名称，默认是 null。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getMethod(); //调用无参数方法读取结果
log("读取结果：" + value);
```


### getUrl()

> 本次配置的请求地址，默认是 null。
> 输入：无参数。输出：String，读取 url 字段的当前值。
> 记录的是配置中传入的地址，不一定是补全协议或重定向后的最终地址。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 本次配置的请求地址，默认是 null。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getUrl(); //调用无参数方法读取结果
log("读取结果：" + value);
```


### getStatus()

> 简写状态码字段，默认是零。
> 输入：无参数。输出：int，读取 status 字段的当前值。
> 当前请求实现中，成功响应会同时填入 statusCode、status、code；非成功状态只填入 statusCode，另外两个可能仍为零。排查失败时优先读取 getStatusCode()。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {int} 简写状态码字段，默认是零。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getStatus(); //调用无参数方法读取结果
log("读取结果：" + value);
```


### getMsg()

> 状态说明文字的简写字段，默认是 null。
> 输入：无参数。输出：String，读取 msg 字段的当前值。
> 当前请求实现中，成功响应会同时填入 statusMessage 和 msg；非成功状态只填入 statusMessage，msg 可能仍为空。
> 示例地址只用于说明写法；实际运行时请换成自己的接口地址。
> 请求会等待服务器回应，请在脚本工作线程调用，不要放进界面线程回调。

- 返回 : {String} 状态说明文字的简写字段，默认是 null。


```javascript
var resp = $http.get("https://example.com/"); //换成实际请求地址
var value = resp.getMsg(); //调用无参数方法读取结果
log("读取结果：" + value);
```


