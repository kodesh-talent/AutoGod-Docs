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




### play(path)

> 立刻播放一段音频（播完自动释放资源）。
> 
> 这是最常用的“放提示音”方法：传入音频文件的路径，它会自动创建播放器、开始播放，
> 并且在播放结束后自动把播放器资源回收掉，你不用手动管。
> 
> 支持的路径：存储卡上的真实文件路径，或者 App 自带 assets 里的资源路径（如 "res/mTip.mp3"）。
> 如果找不到文件，会在日志里打印一条“找不到音频资源”的提示，并返回 null。

- 参数 : path {string} 音频文件的路径，可以是存储卡绝对路径，也可以是 assets 资源路径
- 返回 : {MediaPlayer} 正在播放的系统播放器对象；如果文件找不到或准备失败则返回 null
- 版本 : 1.5.2


```javascript
// 播放 App 自带 assets 里的提示音
var player = $media.play("res/mTip.mp3");
// player 是系统播放器对象，播放结束后会被自动释放
// 如果文件不存在，player 会是 null
if (player != null) {
    log("开始播放了");
}
```


### create()

> 创建一个空白的媒体播放器（先不播放，等你自己设置路径后再控制）。
> 
> 和 play() 的区别：play() 是“立刻播”，create() 是“先造一个空播放器给你”。
> 拿到这个播放器对象后，你可以自己用 setPath() 给它指定音频路径，然后调用它的 start()、pause()、stop() 等方法
> 来精确控制什么时候开始、什么时候暂停、什么时候结束。
> 
> 注意：用完后要记得调用播放器的 release() 方法释放资源，否则会占用内存。

- 返回 : {MediaPlayer} 一个全新的、还没设置音频路径的系统播放器对象
- 版本 : 1.5.2


```javascript
// 创建一个空白播放器
var mediaPlayer = $media.create();
// 给播放器设置音频路径并准备好（成功返回 true）
var ok = $media.setPath(mediaPlayer, "/sdcard/Music/bgm.mp3");
if (ok) {
    mediaPlayer.start(); // 开始播放
    // 这里可以做别的事……
    // 播放结束后记得释放资源
    mediaPlayer.release();
}
```


### create(path)

> 创建播放器并立刻帮你设置好音频路径（但不会自动开始播放）。
> 
> 和 play() 的区别：play() 设置完路径会立刻开始播放；这个方法只是“创建好、准备好”，
> 拿到播放器后由你自己决定什么时候调用 start() 开始播放。适合需要先准备、稍后再播的场景。
> 
> 如果文件找不到，会在日志里打印“找不到音频资源”，并返回 null。

- 参数 : path {string} 音频文件的路径，可以是存储卡绝对路径，也可以是 assets 资源路径
- 返回 : {MediaPlayer} 已准备好音频的播放器对象；文件找不到或准备失败则返回 null
- 版本 : 1.5.2


```javascript
// 创建播放器并准备好指定音频（此时还没播放）
var player = $media.create("/sdcard/Music/bgm.mp3");
if (player != null) {
    // 等你想播的时候，自己调用 start()
    player.start();
}
```


### setPath(mediaPlayer, path)

> 给一个已经创建好的播放器设置音频路径，并自动完成“准备”动作。
> 
> 这是 create() 拿到空白播放器之后的配套方法：你把播放器对象和音频路径传进来，
> 它会依次尝试三种来源——存储卡文件、App 私有目录文件、assets 资源——只要找到一个就加载并 prepare 好。
> 准备成功返回 true，之后你就可以调用播放器的 start() 开始播放了。
> 
> 注意：一个播放器对象通常只能设置一次路径；重复给同一个播放器 setPath 可能会抛异常。

- 参数 : mediaPlayer {MediaPlayer} 用 create() 创建出来的播放器对象，不能传 null
- 参数 : path {string} 音频文件路径，支持存储卡路径或 assets 资源路径
- 返回 : {boolean} 设置并准备成功返回 true；找不到文件或加载失败返回 false
- 版本 : 1.5.2


```javascript
// 先创建一个空白播放器
var player = $media.create();
// 给它设置音频路径，成功返回 true
var ok = $media.setPath(player, "/sdcard/Music/bgm.mp3");
if (ok) {
    player.start(); //开始播放
}
```


