# $media - 媒体播放

- 更新时间:2026-10-22 10:55:49

> 媒体播放对象（脚本里写作 $media），用来播放手机里的音频文件，比如 mp3 提示音、背景音乐等。
> 
> 它内部用安卓系统的 MediaPlayer 播放器来干活：你只需要告诉它音频文件在哪个路径，
> 它就能帮你把声音播出来。支持三种来源：
> <ul>
>     <li>手机存储卡上的真实文件路径，例如 "/sdcard/Music/notice.mp3"；</li>
>     <li>App 自带的 assets 资源里的文件，例如 "res/mTip.mp3"；</li>
>     <li>通过 create() 拿到一个空白播放器后，自己再 setPath 设置路径、自己控制播放节奏。</li>
> </ul>
> 文件路径或资源地址必须有效；播放可能受音频焦点、设备静音和系统后台策略影响。
> 
> 新手提示：如果只是想“立刻播一段提示音”，用 play() 最省事，它会自动开始播放、播完自动回收；
> 如果想“先准备好、稍后再控制什么时候播”，就用 create() 拿到播放器对象，再自己调用它的方法。



```javascript
// 直接播放存储卡上的一段提示音，最简单的用法
$media.play("/sdcard/Music/notice.mp3");
```




### 播放(路径)

> 播放音频（中文方法名版本，作用和 play 完全一样）。
> 
> 直接播放音频，播放结束之后我将自动回收音频资源。
> 
> 这是 play() 的中文别名，参数和返回值都一模一样，只是方法名写成了中文，方便习惯中文的用户调用。

- 参数 : 路径 {字符串} 音频文件的路径，可以是存储卡绝对路径，也可以是 assets 资源路径
- 返回 : {MediaPlayer} 正在播放的系统播放器对象；如果文件找不到或准备失败则返回 null
- 版本 : 1.7.0


```javascript
// 用中文方法名播放一段提示音
var player = $media.播放("/sdcard/Music/notice.mp3");
if (player != null) {
    log("播放中");
}
```


### 创建()

> 创建媒体播放器（中文方法名版本，作用和 create 完全一样）。
> 
> 这是 create() 的中文别名：创建一个空白播放器，拿到后再自己用 设置路径() 指定音频，
> 然后自己控制播放、暂停、停止。用完记得 release() 释放资源。

- 返回 : {MediaPlayer} 一个全新的、还没设置音频路径的系统播放器对象
- 版本 : 1.7.0


```javascript
// 创建一个空白播放器
var mediaPlayer = $media.创建();
// 设置音频路径
var ok = $media.设置路径(mediaPlayer, "res/bgm.mp3");
if (ok) {
    mediaPlayer.start(); //开始播放
}
```


### 创建(路径)

> 创建媒体播放器并设置音频路径（中文方法名版本，作用和 create(path) 完全一样）。
> 
> 这是 create(String) 的中文别名：创建好播放器并准备好音频，但不会自动开始播放，
> 由你自己调用 start() 决定何时播放。

- 参数 : 路径 {字符串} 音频文件的路径，可以是存储卡绝对路径，也可以是 assets 资源路径
- 返回 : {MediaPlayer} 已准备好音频的播放器对象；文件找不到或准备失败则返回 null
- 版本 : 1.7.0


```javascript
// 创建播放器并准备好音频
var player = $media.创建("/sdcard/Music/bgm.mp3");
if (player != null) {
    player.start(); //自己决定什么时候开始播
}
```


### 设置路径(mediaPlayer, 路径)

> 为媒体播放器设置音频路径（中文方法名版本，作用和 setPath 完全一样）。
> 
> 这是 setPath() 的中文别名：给一个已创建好的播放器指定音频路径并准备好。
> 如果此函数被重复调用，可能会抛出异常。

- 参数 : mediaPlayer {MediaPlayer} 用 创建() 创建出来的播放器对象，不能传 null
- 参数 : 路径 {字符串} 音频文件路径，支持存储卡路径或 assets 资源路径
- 返回 : {布尔值} 设置并准备成功返回 true；找不到文件或加载失败返回 false
- 版本 : 1.7.0


```javascript
// 先创建一个空白播放器
var player = $media.创建();
// 给它设置音频路径
var ok = $media.设置路径(player, "/sdcard/Music/bgm.mp3");
if (ok) {
    player.start(); //开始播放
}
```


