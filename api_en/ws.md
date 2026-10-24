# $ws - 双工通信:WebSocket

- 更新时间:2026-10-22 10:55:52

> 按地址发起双向长连接，返回 Ws 包装对象。
> 输入：String 服务器地址，使用 ws:// 或 wss:// 开头，不能为 null 或无效网址；参数错误可能直接抛出异常。
> 输出：Ws，用它注册监听、发送消息和关闭连接。返回对象不代表已经连接成功，实际结果通过网络事件通知。
> 当前实现先发起连接，再保存并返回包装对象；极早的事件可能在对象保存或自定义监听注册之前发生，之后不会补发。
> 各监听只保存一个函数，重复注册会替换旧函数；默认监听输出日志，传 null 停用对应监听。
> 回调的连接参数是 okhttp3.WebSocket，响应是 okhttp3.Response，并非 Ws 或 HttpResponse；底层方法仍使用英文名。
> 示例立即注册失败、消息和打开监听；示例网址只说明格式，需换成自己的服务地址。



```javascript
var socket = $ws.create("wss://example.com/socket"); //发起连接，尚不能认为已经连上
socket.onFail(function (error, response, raw) { //连接失败或异常中断时执行
    log("失败原因：" + error.getMessage()); //这是宿主异常对象
    if (response != null) { //连接失败时可能没有响应
        log("握手响应状态：" + response.code());
    }
});
socket.onMsgStr(function (text, raw) { //收到文字消息时执行
    log("收到文字：" + text); //内容由服务器约定，不保证是对象数据
});
socket.onMsgByte(function (data) { //收到二进制消息时执行
    log("字节数量：" + data.size()); //ByteString 用方法读取长度
    var bytes = data.toByteArray(); //转换成 byte[]
    if (bytes.length > 0) {
        log("首字节：" + (bytes[0] & 255)); //转为无符号数值
    }
});
socket.onClosing(function (code, reason, raw) { //收到关闭请求时执行
    log("对方请求关闭：" + code + "，" + reason);
    raw.close(1000, "收到关闭通知"); //回应关闭，最终结果等待关闭完成事件
});
socket.onClosed(function (code, reason, raw) { //正常关闭完成时执行
    log("正常关闭已完成：" + code);
    log("关闭原因：" + reason); //不要再向已关闭连接发消息
});
socket.onOpen(function (response, raw) { //握手成功时执行
    log("握手状态码：" + response.code()); //底层响应的方法
    var accepted = raw.send("你好服务器"); //使用本次事件提供的底层连接
    log("是否进入队列：" + accepted); //不等于服务器已经处理
});
```




### create(url)

> 按地址发起双向长连接，返回 Ws 包装对象。
> 输入：String 服务器地址，使用 ws:// 或 wss:// 开头，不能为 null 或无效网址；参数错误可能直接抛出异常。
> 输出：Ws，用它注册监听、发送消息和关闭连接。返回对象不代表已经连接成功，实际结果通过网络事件通知。
> 当前实现先发起连接，再保存并返回包装对象；极早的事件可能在对象保存或自定义监听注册之前发生，之后不会补发。
> 各监听只保存一个函数，重复注册会替换旧函数；默认监听输出日志，传 null 停用对应监听。
> 回调的连接参数是 okhttp3.WebSocket，响应是 okhttp3.Response，并非 Ws 或 HttpResponse；底层方法仍使用英文名。
> 示例立即注册失败、消息和打开监听；示例网址只说明格式，需换成自己的服务地址。

- 参数 : url {String} 有效的长连接服务器网址，例如 ws:// 或 wss:// 开头的地址
- 返回 : {Ws} 刚创建的包装对象；实际连接状态通过回调得知


```javascript
var socket = $ws.create("wss://example.com/socket"); //发起连接，尚不能认为已经连上
socket.onFail(function (error, response, raw) { //连接失败或异常中断时执行
    log("失败原因：" + error.getMessage()); //这是宿主异常对象
    if (response != null) { //连接失败时可能没有响应
        log("握手响应状态：" + response.code());
    }
});
socket.onMsgStr(function (text, raw) { //收到文字消息时执行
    log("收到文字：" + text); //内容由服务器约定，不保证是对象数据
});
socket.onMsgByte(function (data) { //收到二进制消息时执行
    log("字节数量：" + data.size()); //ByteString 用方法读取长度
    var bytes = data.toByteArray(); //转换成 byte[]
    if (bytes.length > 0) {
        log("首字节：" + (bytes[0] & 255)); //转为无符号数值
    }
});
socket.onClosing(function (code, reason, raw) { //收到关闭请求时执行
    log("对方请求关闭：" + code + "，" + reason);
    raw.close(1000, "收到关闭通知"); //回应关闭，最终结果等待关闭完成事件
});
socket.onClosed(function (code, reason, raw) { //正常关闭完成时执行
    log("正常关闭已完成：" + code);
    log("关闭原因：" + reason); //不要再向已关闭连接发消息
});
socket.onOpen(function (response, raw) { //握手成功时执行
    log("握手状态码：" + response.code()); //底层响应的方法
    var accepted = raw.send("你好服务器"); //使用本次事件提供的底层连接
    log("是否进入队列：" + accepted); //不等于服务器已经处理
});
```


