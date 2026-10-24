# $tts - 语音阅读

- 更新时间:2026-10-22 10:55:52

> 语音朗读（文字转语音，TTS）对象，脚本里叫 $tts。
> 
> 它能让手机"开口说话"：把一段文字念出来给你听，常用于自动化脚本里做语音提示、播报结果。
> 朗读是异步进行的——调用方法后立刻返回，声音在后台慢慢念，脚本不会卡住等待念完。



```javascript
$tts.read("Hello");  //让手机念出这句话
```




### read(text, options)

> 朗读一段文字（可自定义语速、音调、音量、语言和出声通道）。
> 
> 第二个参数 options 是一个普通 JavaScript 对象，用来定制朗读效果，可填的字段见 TtsOptions：
> rate 语速（1 为正常，越大越快）、pitch 音调（1 为正常）、volume 音量（1 为正常）、
> language 语言（zh 中文、en 英文等）、streamType 出声通道（music、alarm 等）。
> 不传或某个字段不填时，会使用默认值（中文、正常语速音调音量、媒体通道）。

- 参数 : text {string} 要朗读出来的文字内容
- 参数 : options {object} 朗读配置对象，可含 rate/pitch/volume/language/streamType 字段；传 null 则用默认配置
- 版本 : 1.0.0


```javascript
var options = {
    rate: 1.0,      //语速，1 是正常
    pitch: 1.0,     //音调，1 是正常
    volume: 1.0,    //音量，1 是正常
    language: "zh", //用中文朗读
    streamType: "music" //从媒体音乐通道出声
};
$tts.read("你好呀，早安~", options);
```


### read(text)

> 朗读一段文字（使用默认配置）。
> 
> 这是最简单的用法：只给文字，语速、音调、音量、语言、出声通道全部用默认值
> （正常语速音调音量、中文、媒体音乐通道）。需要自定义效果时用带 options 的 read 版本。

- 参数 : text {string} 要朗读出来的文字内容
- 版本 : 1.0.0


```javascript
$tts.read("你好呀，早安~");
```


