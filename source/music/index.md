---
title: 音乐
date: 2026-6-17 00:01:00
comments: false
aplayer: true
aside: false
---
播放器未加載請刷新網頁，加载缓慢耐心等待，可以留意你设备的实时网络吞吐量，极小请退出本页重进,功能开发不完善敬请谅解。
### <p align=center>可以找我点歌我会尽量找无损资源更新的</p>
在此推荐个人用的免费简洁的音乐软件“酷狗概念版”手机apk去浏览器搜3.0~4.0版本不要去官网下最新版他吃相特别难看。pc端GitHub有大佬自制的应用可以调用概念版api[点击前往仓库主页](https://github.com/MoeKoeMusic/MoeKoeMusic)（访问前打开你的steam++！）里面还有插件可以用，我没研究你们找到或者开发了有趣的功能记得踢我一脚😘
<style>
/* 让每个播放器之间有点间距 */
.aplayer-container {
    margin-bottom: 20px;
}
</style>

<!-- 每个播放器一个容器 -->
<div id="player1" class="aplayer-container"></div>
<div id="player2" class="aplayer-container"></div>
<div id="player3" class="aplayer-container"></div>
<div id="player4" class="aplayer-container"></div>

<!-- 引入 APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>

<script>
const ap1 = new APlayer({
    container: document.getElementById('player1'),
    audio: {
        name: '折草为媒',
        artist: '池锦鲤',
        url: '/music/池锦鲤 - 折草为媒_MQ.mp3',
    }
});
const ap2 = new APlayer({
    container: document.getElementById('player2'),
    audio: {
        name: 'Travelers__encore',
        artist: 'Andrew Prahlow',
        url: "/music/Andrew Prahlow - Travelers' encore_HQ.mp3"
    }
});
const ap3 = new APlayer({
    container: document.getElementById('player3'),
    audio: {
        name: '潮鸣',
        artist: '折戸伸治',
        url: "/music/折戸伸治 - 潮鳴り (潮鸣).flac"
    }
});
const ap4 = new APlayer({
    container: document.getElementById('player4'),
    audio: {
        name: '没那么简单',
        artist: '黄小琥',
        url: "/music/没那么简单.mp3"
    }
});
</script>