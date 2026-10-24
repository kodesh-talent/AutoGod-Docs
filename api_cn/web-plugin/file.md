# $file - 文件管理

- 更新时间:2026-10-22 10:55:48



### pack(projectPath)

> 打包项目。
> 
> 传入项目目录路径，会打开打包配置页面，把这个项目打包成可发布的安装包。

- 参数 : projectPath {String} 项目目录的完整路径
- 版本 : 1.8.6


```javascript
//打包指定项目
$file.pack("/sdcard/my_project");
```


### check(projectPath)

> 检查项目配置文件是否正确。
> 
> 它会检查项目目录里的 project.json 是否存在、格式是否正确、启动脚本和路径是否真实存在。
> 全部没问题时返回字符串 "yes"，否则返回一句中文错误说明。

- 参数 : projectPath {String} 项目目录的完整路径
- 返回 : {String} 正确返回 "yes"，否则返回错误说明文字
- 版本 : 1.8.6


```javascript
//检查项目配置是否正确
var result = $file.check("/sdcard/my_project");
if (result === "yes") {
    $log.alert("配置文件正确");
} else {
    $log.alert("配置错误：" + result);
}
```


### edit(codePath)

> 打开应用自带的代码编辑器，并载入指定的代码文件。

- 参数 : codePath {String} 要打开的代码文件完整路径
- 版本 : 1.8.6


```javascript
//打开编辑 main.js
$file.edit("/sdcard/my_project/main.js");
```


### read(filePath)

> 读取一个文本文件的全部内容。

- 参数 : filePath {String} 要读取的文件完整路径
- 返回 : {String} 文件里的文本内容
- 版本 : 1.8.6


```javascript
//读取 main.js 的内容
var text = $file.read("/sdcard/my_project/main.js");
log("文件内容：" + text);
```


### write(content, path)

> 把内容写入文件（覆盖式：原来的内容会被清空替换）。

- 参数 : content {String} 要写入的文字内容
- 参数 : path {String} 目标文件完整路径
- 版本 : 1.8.6


```javascript
//把一段文字写进 note.txt
$file.write("第一行内容", "/sdcard/note.txt");
```


### relPath(projectFolder, relativePath)

> 把一个相对路径换算成基于项目目录的绝对路径。

- 参数 : projectFolder {String} 项目目录路径
- 参数 : relativePath {String} 相对路径，例如 "../res"
- 返回 : {String} 换算后的绝对路径
- 版本 : 1.8.6


```javascript
//项目在 /sdcard/my_project，相对路径 "../res" 会换算成真实绝对路径
var abs = $file.relPath("/sdcard/my_project", "../res");
log("换算后的绝对路径：" + abs);
```


### append(content, path)

> 把内容追加到文件末尾（不会覆盖原有内容）。

- 参数 : content {String} 要追加的文字内容
- 参数 : path {String} 目标文件完整路径
- 版本 : 1.8.6


```javascript
//往 note.txt 末尾再追加一行
$file.append("追加的一行", "/sdcard/note.txt");
```


### del(path)

> 删除文件或文件夹。
> 
> 删文件就直接删掉；删文件夹时会连同里面所有文件一起删掉，请谨慎使用。

- 参数 : path {String} 要删除的文件或文件夹完整路径
- 版本 : 1.8.6


```javascript
//删除一个临时文件
$file.del("/sdcard/temp.txt");
```


