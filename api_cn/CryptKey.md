# 

- 更新时间:2026-10-22 10:55:46

> 脚本中的密钥包装对象 CryptKey，保存字节数组和类型标记。
> 
> 可以从 $crypt.generateKeyPair 返回的密钥对取得公钥或私钥，也可以通过 $crypt.key 包装已有字节数据。
> 包装普通文字不会自动解码公私钥，也不会生成随机密钥。不同算法需要相应格式的数据。
> 所有读取方法返回当前保存值；设置方法不会验证公私钥是否配对。不要直接打印对象，因为文本表示包含密钥内容。



```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    log("类型：" + key.getType());
    var bytes = key.getData();
    log("字节数：" + bytes.length); // 查看结构，不输出内容。
} catch (error) {
    log("密钥处理失败：" + error);
}
```




### const {byte[]} data;

> 密钥原始数据，类型为 byte[]（Java 字节数组），不是普通脚本数组或编码字符串。
> 
> 这是公开字段，直接保存数组引用；修改数组元素会改变当前密钥。不要打印内容。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    var bytes = key.data; // 读取字节数组引用。
    if (bytes != null) {
        log("字节数：" + bytes.length); // 只查看长度。
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### const {String} type;

> 密钥类型标记，类型为 String，可能为 null。
> 
> 非对称密钥通常使用 public 或 private；标记仅指示解析方向，不会自动把字节转换成合法的公钥或私钥。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    log("类型标记：" + key.type);
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### getSecretKey(algorithm)

> 按算法和类型标记把编码数据转换成 Java 密钥对象。
> 
> 输入 algorithm 类型为 String，例如 RSA；返回声明类型为 Object，实际可能为 PublicKey、PrivateKey 或 SecretKeySpec。
> 非对称公钥按 X.509 编码解析，私钥按 PKCS#8 编码解析；错误类型、无效数据或不支持的算法可能抛出异常。
> 实现取斜杠前的算法名称用于密钥解析，不会把签名算法名自动转换成对应的密钥算法；本例使用 RSA。
> 返回对象是底层 Java 密钥，不是 CryptKey 包装对象，可以调用 getAlgorithm() 和 getFormat() 查看描述。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。

- 参数 : algorithm {String} 用于解析密钥的算法名称
- 返回 : {Object} 底层 Java 密钥对象


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    var nativeKey = key.getSecretKey("RSA"); // 用真实公钥数据生成底层对象。
    if (nativeKey != null) {
        log("算法：" + nativeKey.getAlgorithm());
        log("编码格式：" + nativeKey.getFormat());
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### getData()

> 读取密钥数据。输入参数：无；返回类型为 byte[]，可能为 null。
> 
> 返回原数组引用，不复制内容。数组长度用 length 读取；修改元素会影响后续密钥解析。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。

- 返回 : {byte[]} 当前保存的值，可能为 null


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    var bytes = key.getData();
    if (bytes != null) {
        log("字节数：" + bytes.length);
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### setData(data)

> 替换密钥数据。输入 data 类型为 byte[]；输出类型为 void，没有返回值。
> 
> 仅保存数组引用，不复制、不验证密钥格式，也不修改 type。传 null 后转换密钥可能失败。
> 示例从同类型的新公钥取得合法编码数据，并在演示结束后恢复；不要把普通文字当成公钥编码。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。

- 参数 : data {byte[]} 要保存的新值，详见说明


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    var original = key.getData();
    var replacement = $crypt.generateKeyPair("RSA", 2048).getPublicKey();
    try {
        key.setData(replacement.getData()); // 本例仅替换教学对象的公钥数据。
        log("新数据字节数：" + key.getData().length);
    } finally {
        key.setData(original); // 恢复原来的字节数组引用。
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### getType()

> 读取密钥类型标记。输入参数：无；返回类型为 String，可能为 null。
> 
> 生成密钥对时会设置 public 或 private；由普通字符串创建的密钥未必有类型标记。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。

- 返回 : {String} 当前保存的值，可能为 null


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    log("类型标记：" + key.getType());
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### setType(type)

> 设置密钥类型标记。输入 type 类型为 String；输出类型为 void，没有返回值。
> 
> 只保存文字，不改变数据，也不验证格式。把公钥标记改成 private 并不能得到私钥。
> 不要直接打印整个密钥对象；其文本表示包含密钥字节和编码内容。

- 参数 : type {String} 要保存的新值，详见说明


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048); // 创建教学密钥对。
    var key = pair.getPublicKey(); // 本例只操作其中的公钥。
    var original = key.getType();
    try {
        key.setType("public"); // 本例持有公钥，设置与数据相符的标记。
        log(key.getType());
    } finally {
        key.setType(original);
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


