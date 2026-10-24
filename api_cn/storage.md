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




### 创建(命名空间)

> 建一个指定名字的存储对象（中文写法）。
> 
> 其实不建也行，因为默认就有一个命名空间，但建议还是自己建一个，免得和别的脚本数据混在一起。
> 和 create 完全一样。

- 参数 : 命名空间 {string} 命名空间的名字
- 返回 : {AgStorage} 新的存储对象
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");   //命名空间的名称随意
store.放入("主题", "深色");
log(store.获取("主题", "浅色"));
```


### 获取(关键字, 默认值)

> 按名字读取一个值，读不到就返回默认值（中文写法）。
> 
> 和 get 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {Object} 读不到时返回的默认值
- 返回 : {Object} 读到的值，或默认值
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
log(store.获取("我的字符串", "我是默认值"));
```


### 获取(关键字)

> 按名字读取一个值，读不到就返回 null（中文写法）。
> 
> 和 get 单参数版完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {Object} 读到的值，读不到返回 null
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入("我的字符串", "存进去的数据");
log(store.获取("我的字符串"));
```


### 放入(关键字, 数据)

> 存一个字符串到指定名字下（中文写法）。
> 
> 和 put(String,String) 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {string} 要存的字符串
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入("我的字符串", "我是被存进去的数据");
log(store.获取("我的字符串"));
```


### 获取字符串(关键字)

> 按名字读一个字符串，读不到返回空字符串（中文写法）。
> 
> 和 getStr(String) 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {string} 读到的字符串，没有则为 ""
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入("我的字符串", "存进去的数据");
log(store.获取字符串("我的字符串"));
```


### 获取字符串(关键字, 默认值)

> 按名字读一个字符串，读不到就返回默认值（中文写法）。
> 
> 和 getString(key, def) 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {string} 读不到时返回的默认值
- 返回 : {string} 读到的字符串，或默认值
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入("我的字符串", "存进去的数据");
log(store.获取字符串("我的字符串", "默认数据"));
```


### 放入字符串(关键字, 数据)

> 存一个字符串到指定名字下（中文写法）。
> 
> 和 putString 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {string} 要存的字符串
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入字符串("我的字符串", "我是内容");
log(store.获取字符串("我的字符串"));   //我是内容
```


### 获取整数(关键字, 默认值)

> 按名字读一个整数，读不到就返回默认值（中文写法）。
> 
> 和 getInt 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {int} 读不到时返回的默认整数
- 返回 : {int} 读到的整数，或默认值
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
log(store.获取整数("我的整数", 20));
```


### 获取整数(关键字)

> 按名字读一个整数，读不到就返回 0（中文写法）。
> 
> 和 getInt 单参数版完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {int} 读到的整数，没有则为 0
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入整数("我的整数", 100);
log(store.获取整数("我的整数"));
```


### 放入整数(关键字, 数据)

> 存一个整数到指定名字下（中文写法）。
> 
> 和 putInt 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {int} 要存的整数
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入整数("我的整数", 100);
log(store.获取整数("我的整数"));   //100
```


### 获取布尔值(关键字, 默认值)

> 按名字读一个布尔值，读不到就返回默认值（中文写法）。
> 
> 和 getBoolean 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {boolean} 读不到时返回的默认值
- 返回 : {boolean} 读到的 true 或 false
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入布尔值("我的开关", true);
log(store.获取布尔值("我的开关", false));
```


### 获取布尔值(关键字)

> 按名字读一个布尔值，读不到就返回 false（中文写法）。
> 
> 和 getBoolean 单参数版完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {boolean} 读到的值，没有则为 false
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入布尔值("我的开关", true);
log(store.获取布尔值("我的开关"));
```


### 放入布尔值(关键字, 数据)

> 存一个布尔值到指定名字下（中文写法）。
> 
> 和 putBoolean 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {boolean} 要存的 true 或 false
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入布尔值("我的开关", true);
log(store.获取布尔值("我的开关"));
```


### 获取小数(关键字, 默认值)

> 按名字读一个小数，读不到就返回默认值（中文写法）。
> 
> 和 getFloat 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {float} 读不到时返回的默认小数
- 返回 : {float} 读到的小数，或默认值
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
log(store.获取小数("我的小数", 0));
```


### 获取小数(关键字)

> 按名字读一个小数，读不到就返回 0（中文写法）。
> 
> 和 getFloat 单参数版完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {float} 读到的小数，没有则为 0
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入小数("我的小数", 3.1415926);
log(store.获取小数("我的小数"));
```


### 放入小数(关键字, 数据)

> 存一个小数到指定名字下（中文写法）。
> 
> 和 putFloat 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {float} 要存的小数
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入小数("我的小数", 3.1415926);
log(store.获取小数("我的小数", 0));
```


### 获取长整数(关键字, 默认值)

> 按名字读一个长整数，读不到就返回默认值（中文写法）。
> 
> 和 getLong 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {long} 读不到时返回的默认长整数
- 返回 : {long} 读到的长整数，或默认值
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
log(store.获取长整数("我的长整数", 100));
```


### 获取长整数(关键字)

> 按名字读一个长整数，读不到就返回 0（中文写法）。
> 
> 和 getLong 单参数版完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {long} 读到的长整数，没有则为 0
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入长整数("我的长整数", 5201314);
log(store.获取长整数("我的长整数"));
```


### 放入长整数(关键字, 数据)

> 存一个长整数到指定名字下（中文写法）。
> 
> 和 putLong 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {long} 要存的长整数
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入长整数("我的长整数", 5201314);
log(store.获取长整数("我的长整数", 100));   //5201314
```


### 获取字符串集合(关键字, 默认值)

> 按名字读一个字符串列表，读不到就返回默认值（中文写法）。
> 
> 和 getStrSet 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 参数 : 默认值 {array} 读不到时返回的默认字符串数组
- 返回 : {array} 字符串数组
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入字符串集合("我的集合", ["数据1", "数据2", "数据3"]);
log(store.获取字符串集合("我的集合", []));
```


### 获取字符串集合(关键字)

> 按名字读一个字符串列表，读不到就返回空数组（中文写法）。
> 
> 和 getStrSet 单参数版完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要读的名字
- 返回 : {array} 字符串数组，没有则为空数组
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入字符串集合("我的集合", ["数据1", "数据2", "数据3"]);
log(store.获取字符串集合("我的集合"));
```


### 放入字符串集合(关键字, 数据)

> 存一个字符串列表到指定名字下（中文写法）。
> 
> 和 putStrSet 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 名字
- 参数 : 数据 {array} 要存的字符串数组
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入字符串集合("我的集合", ["数据1", "数据2", "数据3"]);
log(store.获取字符串集合("我的集合", []));
```


### 获取全部()

> 一次性取出本命名空间里存的全部数据（中文写法）。
> 
> 和 getAll 完全一样，只是方法名是中文。

- 返回 : {object} 全部数据组成的对象
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入("主题", "深色");
log(store.获取全部());
```


### 有(关键字)

> 判断本命名空间里有没有存过指定名字的数据（中文写法）。
> 
> 和 has 完全一样，只是方法名是中文。

- 参数 : 关键字 {string} 要检查的名字
- 返回 : {boolean} 存过返回 true，否则 false
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入整数("我的整数", 100);
log(store.有("我的整数"));    //true
log(store.有("别的名字"));    //false
```


### 清空()

> 清空本命名空间里存的所有数据（中文写法）。
> 
> 和 clear 完全一样，只是方法名是中文。会删掉本命名空间全部数据，谨慎使用。

- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入整数("我的整数", 100);
store.清空();
log(store.获取整数("我的整数", -1));
```


### 删除(关键字)

> 删除指定名字的那一条数据（中文写法）。
> 
> 和 del 完全一样，只是方法名是中文。只删这一条。

- 参数 : 关键字 {string} 要删除的名字
- 版本 : 1.7.0


```javascript
var store = $storage.create("settings");
store.放入整数("我的整数", 100);
store.删除("我的整数");
log(store.获取整数("我的整数", -1));
```


