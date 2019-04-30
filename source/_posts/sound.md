---
title: 移动端语音播报问题集合
date: 2017-12-19 14:16:01
tags: [question]
categories: oh my bug
---
突然想到之前一个项目的问题，当时手忙脚乱糊弄地解决了一下。
打卡签到，播放“XXX,签到成功”。
判断一个人的语音提示是否播报完成？或者打断？
<div align=center>
![“封面”](/images/bg/0059.jpeg)
</div>
<!--more-->

# 文本生成语音
```javascript
var speaker = new window.SpeechSynthesisUtterance();
var speakTimer,
    stopTimer;
// 开始播报
function speakText(text) {
    clearTimeout(speakTimer);
    window.speechSynthesis.cancel();
    speakTimer = setTimeout(function () {
        speaker.text = text;
        window.speechSynthesis.speak(speaker);
    }, 200);
}
// 停止播报
function stopSpeak() {
    clearTimeout(stopTimer);
    clearTimeout(speakTimer);
    stopTimer = setTimeout(function () {
        window.speechSynthesis.cancel();
    }, 20);
}
```
## API
### SpeechSynthesis

| 参数|           含义|
| ---|--- |
| paused |           是否暂停|
| pending |          是否处理中|
| speaking |         是否朗读中|
| onvoiceschanged |  声音变化时触发|
| cancel()|          情况待朗读队列|
| getVoices() |      获取浏览器支持的语音包列表|
| pause()  |         暂停|
| resume()  |        重新开始|
| speak()  |        读合成的语音，参数必须|

### SpeechSynthesisUtterance
| 参数|           含义|
| ---|--- |
| lang |           语言|
| pitch |          音高|
| rate |         语速|
| text |  文本|
| voice|          声音|
| volume |      音量|
| onboundary  |          单词或句子边界触发，即分隔处触发|
| onend  |        结束时触发|
| onerror  |        错误时触发|
| onmark |      |
| onpause  |          暂停时触发|
| onresume  |        重新播放时触发|
| onstart  |       开始时触发|