# $storage - 应用内存储

- 更新时间:2026-10-22 10:55:51

> 应用内的小数据存储（$storage），用来长期保存脚本的设置和少量数据。
> 
> 它像一个“字典”：用一个名字（key）存进去一个值，以后再按这个名字取出来。
> 适合保存开关、账号、上次的选择这类小数据；不适合存图片或大文件。
> 卸载应用后数据会随应用一起被清除。先调 create() 建一个命名空间再用。



```javascript
var store = $storage.create("settings");   //建一个叫 settings 的存储
store.put("theme", "dark");                 //存一个字符串
var theme = store.get("theme", "light");   //读出来，没有就返回 light
log(theme);
```




### create(namespace)

> 建一个指定名字的存储对象（命名空间）。
> 
> 名字随便起，不同名字的数据互不干扰；只要两次用同一个名字，就能读到同一份数据。
> 传 null 会返回默认的那个存储对象。

- 参数 : namespace {string} 命名空间的名字
- 返回 : {AgStorage} 新的存储对象
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");   //命名空间的名称随意
store.put("theme", "dark");
log(store.get("theme", "light"));
```


### get(key, defaultValue)

> 按名字读取一个值，读不到就返回你给的默认值。
> 
> 返回的是 Object 类型，实际类型要看当初存进去的是什么。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {Object} 读不到时返回的默认值
- 返回 : {Object} 读到的值，或默认值
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
var v = store.get("theme", "浅色");   //没有 theme 就返回“浅色”
log(v);
```


### get(key)

> 按名字读取一个值，读不到就返回 null。
> 
> 想给默认值请用带两个参数的 get。

- 参数 : key {string} 要读的名字
- 返回 : {Object} 读到的值，读不到返回 null
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.put("我的字符串", "存进去的数据");
log(store.get("我的字符串"));
```


### put(key, value)

> 存一个字符串到指定名字下。
> 
> 同名再存会覆盖旧值。只要命名空间名字一致，下次运行还能读到。

- 参数 : key {string} 名字
- 参数 : value {string} 要存的字符串
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.put("我的字符串", "我是被存进去的数据");
log(store.get("我的字符串"));
```


### getStr(key)

> 按名字读一个字符串，读不到返回空字符串 ""。
> 
> 它就是 getString(String) 的简写，没存过时返回空串而不是 null。

- 参数 : key {string} 要读的名字
- 返回 : {string} 读到的字符串，没有则为 ""
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.put("我的字符串", "存进去的数据");
log(store.getStr("我的字符串"));
```


### getString(key)

> 按名字读一个字符串，读不到返回空字符串 ""。
> 
> 和 getStr(String) 是同一回事。

- 参数 : key {string} 要读的名字
- 返回 : {string} 读到的字符串，没有则为 ""
- 版本 : 1.5.4


```javascript
var store = $storage.create("settings");
store.put("我的字符串", "存进去的数据");
log(store.getString("我的字符串"));
```


### getStr(key, defaultValue)

> 按名字读一个字符串，读不到就返回你给的默认值。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {string} 读不到时返回的默认值
- 返回 : {string} 读到的字符串，或默认值
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
log(store.getStr("我的字符串", "默认数据"));
```


### getString(key, defaultValue)

> 按名字读一个字符串，读不到就返回你给的默认值。
> 
> 和 getStr(key, def) 是同一回事。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {string} 读不到时返回的默认值
- 返回 : {string} 读到的字符串，或默认值
- 版本 : 1.5.4


```javascript
var store = $storage.create("settings");
log(store.getString("我的字符串", "默认数据"));
```


### putStr(key, value)

> 存一个字符串到指定名字下。
> 
> 和 putString 是同一回事。同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {string} 要存的字符串
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putStr("我的字符串", "我是内容");
log(store.getStr("我的字符串"));   //我是内容
```


### putString(key, value)

> 存一个字符串到指定名字下。
> 
> 和 putStr 是同一回事。同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {string} 要存的字符串
- 版本 : 1.5.4


```javascript
var store = $storage.create("settings");
store.putString("我的字符串", "我是内容");
log(store.getString("我的字符串"));   //我是内容
```


### getInt(key, defaultValue)

> 按名字读一个整数，读不到就返回你给的默认值。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {int} 读不到时返回的默认整数
- 返回 : {int} 读到的整数，或默认值
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
log(store.getInt("我的整数", 20));   //没有就返回 20
```


### getInt(key)

> 按名字读一个整数，读不到就返回 0。

- 参数 : key {string} 要读的名字
- 返回 : {int} 读到的整数，没有则为 0
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putInt("我的整数", 100);
log(store.getInt("我的整数"));   //100；没有则是 0
```


### putInt(key, value)

> 存一个整数到指定名字下。
> 
> 同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {int} 要存的整数
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putInt("我的整数", 100);
log(store.getInt("我的整数"));   //100
```


### getBool(key, defaultValue)

> 按名字读一个布尔值（true/false），读不到就返回你给的默认值。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {boolean} 读不到时返回的默认值
- 返回 : {boolean} 读到的 true 或 false
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
log(store.getBool("我的开关", false));   //没有则返回 false
log(store.getBool("我的开关", true));    //没有则返回 true
```


### getBoolean(key, defaultValue)

> 按名字读一个布尔值，读不到就返回你给的默认值。
> 
> 和 getBool(key, def) 是同一回事。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {boolean} 读不到时返回的默认值
- 返回 : {boolean} 读到的 true 或 false
- 版本 : 1.5.4


```javascript
var store = $storage.create("settings");
log(store.getBoolean("我的开关", true));
```


### getBool(key)

> 按名字读一个布尔值，读不到就返回 false。
> 
> 它内部走的是 getBoolean(key)。

- 参数 : key {string} 要读的名字
- 返回 : {boolean} 读到的值，没有则为 false
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putBool("我的开关", true);
log(store.getBool("我的开关"));   //true
```


### getBoolean(key)

> 按名字读一个布尔值，读不到就返回 false。

- 参数 : key {string} 要读的名字
- 返回 : {boolean} 读到的值，没有则为 false
- 版本 : 1.5.4


```javascript
var store = $storage.create("settings");
store.putBoolean("我的开关", true);
log(store.getBoolean("我的开关"));   //true
```


### putBool(key, value)

> 存一个布尔值到指定名字下。
> 
> 和 putBoolean 是同一回事。同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {boolean} 要存的 true 或 false
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putBool("我的开关", true);
log(store.getBool("我的开关"));   //true
```


### putBoolean(key, value)

> 存一个布尔值到指定名字下。
> 
> 和 putBool 是同一回事。同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {boolean} 要存的 true 或 false
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putBoolean("我的开关", true);
log(store.getBoolean("我的开关"));   //true
```


### getFloat(key, defaultValue)

> 按名字读一个小数，读不到就返回你给的默认值。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {float} 读不到时返回的默认小数
- 返回 : {float} 读到的小数，或默认值
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
log(store.getFloat("我的小数", 0));
```


### getFloat(key)

> 按名字读一个小数，读不到就返回 0。

- 参数 : key {string} 要读的名字
- 返回 : {float} 读到的小数，没有则为 0
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putFloat("我的小数", 3.14);
log(store.getFloat("我的小数"));   //3.14
```


### putFloat(key, value)

> 存一个小数到指定名字下。
> 
> 同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {float} 要存的小数
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putFloat("我的小数", 3.1415926);
log(store.getFloat("我的小数"));
```


### getLong(key, defaultValue)

> 按名字读一个长整数，读不到就返回你给的默认值。
> 
> 长整数能存很大的数（比如时间戳、大数字）。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {long} 读不到时返回的默认长整数
- 返回 : {long} 读到的长整数，或默认值
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
log(store.getLong("我的长整数", 100));
```


### getLong(key)

> 按名字读一个长整数，读不到就返回 0。

- 参数 : key {string} 要读的名字
- 返回 : {long} 读到的长整数，没有则为 0
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putLong("我的长整数", 5201314);
log(store.getLong("我的长整数"));
```


### putLong(key, value)

> 存一个长整数到指定名字下。
> 
> 同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {long} 要存的长整数
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putLong("我的长整数", 5201314);
log(store.getLong("我的长整数", 100));   //5201314
```


### getStrSet(key, defaultValue)

> 按名字读一个字符串列表，读不到就返回默认值。
> 
> 返回的是一个数组，可以用下标取里面的元素。

- 参数 : key {string} 要读的名字
- 参数 : defaultValue {array} 读不到时返回的默认字符串数组
- 返回 : {array} 字符串数组
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
var list = store.getStrSet("我的集合", []);
log(list[0]);
```


### getStrSet(key)

> 按名字读一个字符串列表，读不到就返回空数组。

- 参数 : key {string} 要读的名字
- 返回 : {array} 字符串数组，没有则为空数组
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putStrSet("我的集合", ["数据1", "数据2", "数据3"]);
log(store.getStrSet("我的集合"));
```


### putStrSet(key, value)

> 存一个字符串列表到指定名字下。
> 
> 传入一个数组。同名再存会覆盖旧值。

- 参数 : key {string} 名字
- 参数 : value {array} 要存的字符串数组
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putStrSet("我的集合", ["数据1", "数据2", "数据3"]);
log(store.getStrSet("我的集合", []));
```


### getAll()

> 一次性取出本命名空间里存的全部数据。
> 
> 返回一个对象，里面每个属性就是一条“名字→值”。

- 返回 : {object} 全部数据组成的对象
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.put("theme", "dark");
store.putInt("音量", 5);
log(store.getAll());
```


### has(key)

> 判断本命名空间里有没有存过指定名字的数据。
> 
> 有就返回 true，没有返回 false。

- 参数 : key {string} 要检查的名字
- 返回 : {boolean} 存过返回 true，否则 false
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putInt("我的整数", 100);
log(store.has("我的整数"));    //true
log(store.has("别的名字"));    //false
```


### clear()

> 清空本命名空间里存的所有数据。
> 
> 这一步会把本命名空间里所有“名字→值”全部删掉，谨慎使用。

- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putInt("我的整数", 100);
store.clear();
log(store.getInt("我的整数", -1));   //-1，已被清空
```


### del(key)

> 删除指定名字的那一条数据。
> 
> 只删这一条，其它数据保留。删完再读就会拿到默认值。

- 参数 : key {string} 要删除的名字
- 版本 : 1.0.0


```javascript
var store = $storage.create("settings");
store.putInt("我的整数", 100);
store.del("我的整数");
log(store.getInt("我的整数", -1));   //-1，已被删除
```


