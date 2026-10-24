# $crypt - 加密算法

- 更新时间:2026-10-22 10:55:46

> 加解密与摘要工具对象，脚本里叫 $crypt。
> 
> 它提供了常用的编码（Base64）、摘要（MD5/SHA）、对称加解密（AES）和非对称签名验签能力。
> 传参和结果的格式（字符串/字节/base64/hex）用 options 对象里的 input/output 控制。



```javascript
var encoded = $crypt.toBase64("hello");
var decoded = $crypt.fromBase64(encoded);
```




### fromBase64(data)

> 把一段 Base64 字符串解码还原成普通文本。

- 参数 : data {string} 要解码的 Base64 字符串
- 返回 : {string} 解码后的原始文本；输入非法时可能返回空
- 版本 : 1.0.0


```javascript
var result = $crypt.fromBase64("sample text");
```


### toBase64(data)

> 把一段字节数组编码成 Base64 字符串。

- 参数 : data {byte[]} 要编码的字节数组
- 返回 : {string} 编码后的 Base64 字符串
- 版本 : 1.0.0


```javascript
var result = $crypt.toBase64([65, 66, 67]);
```


### toBase64(data)

> 把一段普通文本按 UTF-8 编码成 Base64 字符串。

- 参数 : data {string} 要编码的文本
- 返回 : {string} 编码后的 Base64 字符串
- 版本 : 1.0.0


```javascript
var result = $crypt.toBase64("sample text");
```


### toBase64(data, encoding)

> 把一段文本按指定字符集编码成 Base64 字符串。

- 参数 : data {string} 要编码的文本
- 参数 : encoding {string} 字符集，如 UTF-8、GBK
- 返回 : {string} 编码后的 Base64 字符串
- 版本 : 1.0.0


```javascript
var result = $crypt.toBase64("sample text", "UTF-8");
```


### aesKey()

> 随机生成一个 16 位的 AES 密钥。
> 
> AES-128 需要 16 字节密钥，这个方法直接给你一个可用的随机字符串密钥。

- 返回 : {string} 随机生成的 16 位密钥字符串
- 版本 : 1.0.0


```javascript
var result = $crypt.aesKey();
```


### aesJiami(data, key)

> 用 AES 把一段文本加密成 Base64 字符串（AES 加密的便捷方法）。

- 参数 : data {string} 要加密的明文
- 参数 : key {string} 16 位 AES 密钥
- 返回 : {string} 加密后的 Base64 密文；失败返回 null
- 版本 : 1.0.0


```javascript
var result = $crypt.aesJiami("sample text", "0123456789abcdef");
```


### aesJiemi(data, key)

> 用 AES 把 Base64 密文解密还原成文本（AES 解密的便捷方法）。

- 参数 : data {string} 要解密的 Base64 密文
- 参数 : key {string} 16 位 AES 密钥（加密时用的同一个）
- 返回 : {string} 解密后的明文；失败返回 null
- 版本 : 1.0.0


```javascript
var result = $crypt.aesJiemi("sample text", "0123456789abcdef");
```


### md5Key(size)

> 随机生成一个指定长度的字节数组，常用作摘要的"盐"。

- 参数 : size {int} 要生成的随机字节长度
- 返回 : {byte[]} 随机字节数组
- 版本 : 1.0.0


```javascript
var result = $crypt.md5Key(100);
```


### md516(salt, data)

> md5加密

- 参数 : salt {byte[]} 加盐用的随机字节数组（先参与哈希再算正文）
- 参数 : data {string} 要计算摘要的文本
- 返回 : 取 32 位 MD5 中间 16 位（第 9~24 位）的结果；失败返回 null
- 版本 : 1.0.0


```javascript
var result = $crypt.md516([65, 66, 67], "sample text");
```


### md532(salt, data)

> md5加密

- 参数 : salt {byte[]} 加盐用的随机字节数组（先参与哈希再算正文）
- 参数 : data {string} 要计算摘要的文本
- 返回 : 完整的 32 位小写十六进制 MD5 摘要字符串
- 版本 : 1.0.0


```javascript
var result = $crypt.md532([65, 66, 67], "sample text");
```


### digest(message, algorithm, options)

> 摘要

- 参数 : message {File|String|byte[]} 要计算摘要的数据（字符串/字节/文件）
- 参数 : algorithm {string} 摘要算法名，如 MD5、SHA-1、SHA-256
- 参数 : options {object} 可含 input/output/encoding，指定输入输出格式
- 返回 : 按 options 格式返回的摘要结果（默认 hex 字符串）
- 版本 : 1.0.0


```javascript
//MD5加密
var result = $crypt.digest("我是你爸爸","md5",{
    input: "string",  //输入是普通字符串
    output: "hex"     //输出为十六进制
});
log(result);
```


### md5(message, options)

> 摘要

- 参数 : message {File|String|byte[]} 要计算 MD5 的数据
- 参数 : options {object} 可含 input/output/encoding，指定输入输出格式
- 返回 : 按 options 格式返回的 MD5 摘要结果（默认 hex 字符串）
- 版本 : 1.0.0


```javascript
//MD5加密
var result = $crypt.md5("我是加密的内容",{
    input: "string",  //输入是普通字符串
    output: "hex"     //输出为十六进制
});
log(result);//a4f2086496066b767f9667d4737047b7
```


### sign(data, key, algorithm, options)

> 签名

- 参数 : data {File|String|byte[]} 要签名的原文
- 参数 : key {CryptKey} 私钥对象（由 generateKeyPair 获得，用它的 privateKey）
- 参数 : algorithm {string} 签名算法，如 SHA256withRSA、DSA
- 参数 : options {object} 可含 input/output，指定原文与签名结果格式
- 返回 : {object} 数字签名结果，格式由 options.output 决定
- 版本 : 1.0.0


```javascript
//生成密钥对
var keyPair = $crypt.generateKeyPair("DSA", 1024);
log(keyPair)
log("签名:"); //数字签名只能用私钥进行签名
var signData = $crypt.sign("我是被签名的内容", keyPair.privateKey, "DSA", {
    input: "string",   //原文按字符串读入
    output: "base64"   //签名结果输出为 base64
});
log("验证:"); //数字签名只能用公钥进行验证
var verified = $crypt.verify("我是被签名的内容",signData, keyPair.publicKey, "DSA", {
    //输入文本的类型
    input: "string"   //原文按字符串读入
},{
    //输入签名的类型
    input: "base64"   //签名是 base64 字符串
});
log("验证结果:", verified);
```


### verify(msg_data, msg_sign, key, algorithm, optionsObj_data, optionsObj_sign)

> 验证

- 参数 : msg_data {object} 原始待验证的文本
- 参数 : msg_sign {object} 之前生成的签名数据
- 参数 : key {CryptKey} 公钥对象（由 generateKeyPair 获得，用它的 publicKey）
- 参数 : algorithm {string} 签名算法，要和签名时一致
- 参数 : optionsObj_data {object} 原文的输入格式选项（如 input:"string"）
- 参数 : optionsObj_sign {object} 签名的输入格式选项（如 input:"base64"）
- 返回 : 签名合法返回 true，被篡改或不匹配返回 false
- 版本 : 1.0.0


```javascript
var keyPair = $crypt.generateKeyPair("RSA", 2048);
var signature = $crypt.sign("message", keyPair.getPrivateKey(), "SHA256withRSA", { input: "string", output: "base64" });
var verified = $crypt.verify("message", signature, keyPair.getPublicKey(), "SHA256withRSA", { input: "string" }, { input: "base64" });
```


### digests()

> 获得所有摘要算法的名称

- 返回 : {string[]} 所有支持的摘要算法名列表（如 MD5、SHA-1、SHA-256 等）
- 版本 : 1.0.0


```javascript
//获得所有哈希算法的名称
var digests = $crypt.digests();
//每个算法都用一遍
for (var i = 0; i < digests.size(); i ++) {
    var result = $crypt.digest("我是加密的内容", digests.get(i), {
        input: "string",  //输入是普通字符串
        output: "hex"     //输出为十六进制
    });
    log(result);
}
```


### digestFile(path, algorithm, options)

> 摘要文件

- 参数 : path {string} 文件路径
- 参数 : algorithm {string} 摘要算法名，如 SHA-256、MD5
- 参数 : options {object} 可含 output 指定输出格式
- 返回 : {string|byte[]} 整个文件的摘要结果，格式由 options 决定
- 版本 : 1.0.0


```javascript
// 先准备可读取的文件，并把路径改成文件的实际位置。
var options = {output: "hex"}; // 使用十六进制字符串表示摘要。
var result = $crypt.digestFile("/sdcard/Download/sample.txt", "SHA-256", options);
// result 是文件内容的摘要，不是加密后的文件，也不能用来还原原文。
```


### jiami(data, key, algorithm, options)

> 加密

- 参数 : data {object} 要加密的明文（字符串/字节/文件）
- 参数 : key {object} 密钥，可以是字符串、字节数组或 CryptKey 对象
- 参数 : algorithm {string} 加密算法，如 AES
- 参数 : options {object} 可含 input/output 指定输入输出格式
- 返回 : {string|byte[]} 加密结果，格式由 options.output 决定
- 版本 : 1.0.0


```javascript
//对称加密算法
//准备一个长度为16的密钥
var key = "ACSDFGHJUYDLOPSD";
var text = "我是被加密的明文";
log("AES加密");
var result = $crypt.jiami(text,key,"AES",{
 input: "string",   //输入是普通字符串
 output: "base64"    //输出 base64 密文
});
log("加密后：",result)
result = $crypt.jiemi(result,key,"AES",{
 input: "base64",    //输入是 base64 密文
 output: "string"    //输出还原后的字符串
});
log("解密后：",result)
```


### jiami(data, key, algorithm)

> 加密

- 参数 : data {object} 要加密的明文
- 参数 : key {object} 密钥（字符串/字节/CryptKey）
- 参数 : algorithm {string} 加密算法，如 AES
- 返回 : {string|byte[]} 加密结果，默认输入字符串、输出 base64
- 版本 : 1.0.0


```javascript
var result = $crypt.jiami("sample text", "0123456789abcdef", "AES", { input: "string", output: "base64" });
```


### jiemi(data, key, algorithm, options)

> 解密

- 参数 : data {object} 要解密的密文
- 参数 : key {object} 密钥（字符串/字节/CryptKey，要和加密时相同）
- 参数 : algorithm {string} 加密算法，如 AES
- 参数 : options {object} 可含 input/output 指定输入输出格式
- 返回 : {string|byte[]} 解密结果，格式由 options.output 决定
- 版本 : 1.0.0


```javascript
var result = $crypt.jiemi("sample text", "0123456789abcdef", "AES", { input: "string", output: "base64" });
```


### jiemi(data, key, algorithm)

> 解密

- 参数 : data {object} 要解密的密文
- 参数 : key {object} 密钥（要和加密时相同）
- 参数 : algorithm {string} 加密算法，如 AES
- 返回 : {string|byte[]} 解密结果，默认输入 base64、输出字符串
- 版本 : 1.0.0


```javascript
var result = $crypt.jiemi("sample text", "0123456789abcdef", "AES", { input: "string", output: "base64" });
```


### key(data)

> 构建密钥对象

- 参数 : data {string|byte[]} 密钥内容，可以是字符串或字节数组
- 返回 : {CryptKey} 包装好的密钥对象，供加密/解密/签名方法使用
- 版本 : 1.0.0


```javascript
var result = $crypt.key("sample text");
```


### key(data)

> 生成密钥

- 参数 : data {String} 密钥字符串
- 返回 : {CryptKey} 包装好的密钥对象
- 版本 : 1.0.0


```javascript
var result = $crypt.key("sample text");
```


### key(data)

> 生成密钥

- 参数 : data {byte[]} 密钥字节数组
- 返回 : {CryptKey} 包装好的密钥对象
- 版本 : 1.0.0


```javascript
var result = $crypt.key([65, 66, 67]);
```


### keyPair(publicKey, privateKey)

> 构造密钥对

- 参数 : publicKey {byte[] | base64} 公钥内容（字节数组或 base64 字符串）
- 参数 : privateKey {byte[] | base64} 私钥内容（字节数组或 base64 字符串）
- 返回 : {CryptKeyPair} 由这对现成密钥组装成的密钥对对象
- 版本 : 1.0.0


```javascript
var result = $crypt.keyPair("sample text", "sample text");
```


### keyPair(publicKey, privateKey)

> 用现成的公钥、私钥字节数组组装成一个密钥对对象。

- 参数 : publicKey {byte[]} 公钥字节数组
- 参数 : privateKey {byte[]} 私钥字节数组
- 返回 : {CryptKeyPair} 组装好的密钥对对象
- 版本 : 1.0.0


```javascript
var result = $crypt.keyPair([65, 66, 67], [65, 66, 67]);
```


### generateKeyPair(algorithm)

> 生成密钥对

- 参数 : algorithm {string} 非对称算法名，如 RSA、DSA
- 返回 : {CryptKeyPair} 新生成的密钥对（含 publicKey/privateKey）
- 版本 : 1.0.0


```javascript
var result = $crypt.generateKeyPair("SHA-256");
```


### generateKeyPair(algorithm, length)

> 生成密钥对

- 参数 : algorithm {string} 非对称算法名，如 RSA、DSA
- 参数 : length {int} 密钥长度（位数），如 1024、2048；不传默认 256
- 返回 : {CryptKeyPair} 新生成的密钥对（含 publicKey/privateKey）
- 版本 : 1.0.0


```javascript
var result = $crypt.generateKeyPair("SHA-256", 100);
```


