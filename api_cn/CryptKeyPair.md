# 

- 更新时间:2026-10-22 10:55:46

> 公钥和私钥的容器，脚本类型名为 CryptKeyPair。
> 
> 通过 $crypt.generateKeyPair 生成后，用 getPublicKey() 和 getPrivateKey() 取出 CryptKey 对象。
> 容器只保存两份引用，不会在更换成员时自动校验它们是否配对。生成失败可能抛出异常。
> 不要把整个容器写入日志；toString() 会连同私钥内容一起输出。



```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var publicKey = pair.getPublicKey();
    var privateKey = pair.getPrivateKey();
    log("公钥类型：" + publicKey.getType());
    log("私钥类型：" + privateKey.getType()); // 只打印类型标记。
} catch (error) {
    log("密钥处理失败：" + error);
}
```




### const {CryptKey} publicKey;

> 保存密钥对中的公钥对象。
> 
> 对象类型为 CryptKey，包含原始密钥字节和类型标记。
> 这是私有字段，脚本应调用 getPublicKey()，不要直接访问 pair.publicKey。
> 不要直接打印密钥对象；其文本表示会包含原始密钥内容，私钥尤其不应写入日志。


```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var key = pair.getPublicKey(); // 取得关联的 CryptKey 对象。
    if (key != null) {
        log("类型标记：" + key.getType());
        var bytes = key.getData(); // Java 字节数组，勿打印数组内容。
        if (bytes != null) {
            log("编码字节数：" + bytes.length);
        }
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### const {CryptKey} privateKey;

> 保存密钥对中的私钥对象。
> 
> 对象类型为 CryptKey，包含原始密钥字节和类型标记。
> 这是私有字段，脚本应调用 getPrivateKey()，不要直接访问 pair.privateKey。
> 不要直接打印密钥对象；其文本表示会包含原始密钥内容，私钥尤其不应写入日志。


```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var key = pair.getPrivateKey(); // 取得关联的 CryptKey 对象。
    if (key != null) {
        log("类型标记：" + key.getType());
        var bytes = key.getData(); // Java 字节数组，勿打印数组内容。
        if (bytes != null) {
            log("编码字节数：" + bytes.length);
        }
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### getPublicKey()

> 读取密钥对中的公钥对象。
> 
> 对象类型为 CryptKey，包含原始密钥字节和类型标记。
> 输入参数：无；返回类型为 CryptKey。返回的是原对象引用，不是副本，修改它也会影响当前密钥对。
> 通过设置方法可以把它改成 null，因此复用外部传来的密钥对时需要检查空值。
> 不要直接打印密钥对象；其文本表示会包含原始密钥内容，私钥尤其不应写入日志。

- 返回 : {CryptKey} 当前公钥对象引用，可能为 null


```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var key = pair.getPublicKey(); // 取得关联的 CryptKey 对象。
    if (key != null) {
        log("类型标记：" + key.getType());
        var bytes = key.getData(); // Java 字节数组，勿打印数组内容。
        if (bytes != null) {
            log("编码字节数：" + bytes.length);
        }
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### setPublicKey(publicKey)

> 设置密钥对中的公钥对象。
> 
> 对象类型为 CryptKey，包含原始密钥字节和类型标记。
> 输入 publicKey 类型为 CryptKey；输出类型为 void，没有返回值。
> 只替换此对象引用，允许传入 null；不检查类型或密钥是否与另一把配对，也不会自动更新另一把密钥。
> 下面先保存原引用，再把同一套新生成的公私钥一起换入，避免只换一半导致配对失效。
> 不要直接打印密钥对象；其文本表示会包含原始密钥内容，私钥尤其不应写入日志。

- 参数 : publicKey {CryptKey} 替换用的公钥对象，可为 null


```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var originalPublic = pair.getPublicKey();
    var originalPrivate = pair.getPrivateKey();
    var replacement = $crypt.generateKeyPair("RSA", 2048);
    try {
        pair.setPublicKey(replacement.getPublicKey()); // 设置本方法对应的一把密钥。
        pair.setPrivateKey(replacement.getPrivateKey()); // 同时更换另一把，保持成对。
        var key = pair.getPublicKey();
        if (key != null) {
            log("类型标记：" + key.getType()); // 只查看标记，不输出密钥字节。
        }
    } finally {
        pair.setPublicKey(originalPublic); // 演示结束，恢复原密钥对。
        pair.setPrivateKey(originalPrivate);
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### getPrivateKey()

> 读取密钥对中的私钥对象。
> 
> 对象类型为 CryptKey，包含原始密钥字节和类型标记。
> 输入参数：无；返回类型为 CryptKey。返回的是原对象引用，不是副本，修改它也会影响当前密钥对。
> 通过设置方法可以把它改成 null，因此复用外部传来的密钥对时需要检查空值。
> 不要直接打印密钥对象；其文本表示会包含原始密钥内容，私钥尤其不应写入日志。

- 返回 : {CryptKey} 当前私钥对象引用，可能为 null


```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var key = pair.getPrivateKey(); // 取得关联的 CryptKey 对象。
    if (key != null) {
        log("类型标记：" + key.getType());
        var bytes = key.getData(); // Java 字节数组，勿打印数组内容。
        if (bytes != null) {
            log("编码字节数：" + bytes.length);
        }
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


### setPrivateKey(privateKey)

> 设置密钥对中的私钥对象。
> 
> 对象类型为 CryptKey，包含原始密钥字节和类型标记。
> 输入 privateKey 类型为 CryptKey；输出类型为 void，没有返回值。
> 只替换此对象引用，允许传入 null；不检查类型或密钥是否与另一把配对，也不会自动更新另一把密钥。
> 下面先保存原引用，再把同一套新生成的公私钥一起换入，避免只换一半导致配对失效。
> 不要直接打印密钥对象；其文本表示会包含原始密钥内容，私钥尤其不应写入日志。

- 参数 : privateKey {CryptKey} 替换用的私钥对象，可为 null


```javascript
try {
    // 创建一对教学用密钥；长度显式填写，不依赖默认值。
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var originalPublic = pair.getPublicKey();
    var originalPrivate = pair.getPrivateKey();
    var replacement = $crypt.generateKeyPair("RSA", 2048);
    try {
        pair.setPrivateKey(replacement.getPrivateKey()); // 设置本方法对应的一把密钥。
        pair.setPublicKey(replacement.getPublicKey()); // 同时更换另一把，保持成对。
        var key = pair.getPrivateKey();
        if (key != null) {
            log("类型标记：" + key.getType()); // 只查看标记，不输出密钥字节。
        }
    } finally {
        pair.setPublicKey(originalPublic); // 演示结束，恢复原密钥对。
        pair.setPrivateKey(originalPrivate);
    }
} catch (error) {
    log("密钥处理失败：" + error);
}
```


