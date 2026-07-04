---
title: 音乐
date: 2026-6-17 00:01:00
comments: false
aplayer: true
aside: true
---
### <p align=center>可以找我点歌我会尽量找无损资源更新的</p>
在此推荐个人用的免费简洁的音乐软件“酷狗概念版”手机apk去浏览器搜3.0~4.0版本不要去官网下最新版他吃相特别难看。pc端GitHub有大佬自制的应用调用概念版api[点击前往仓库主页](https://github.com/MoeKoeMusic/MoeKoeMusic)什么你说想要下面音乐的源文件，它们就在我GitHub命名最规范的那个仓库的music文件夹里自己去拿吧！
<style>
/* 让每个播放器之间有点间距 */
.aplayer-container {
    margin-bottom: 20px;
}
</style>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>

**纯音乐**
<div id="player1" class="aplayer-container"></div>
<script>
const ap1 = new APlayer({
    container: document.getElementById('player1'),
    audio: [
    {
        name: '折草为媒',
        artist: '池锦鲤',
        url: '/music/池锦鲤 - 折草为媒_MQ.mp3',
    },
    {
        name: 'Travelers__encore',
        artist: 'Andrew Prahlow',
        url: "/music/Andrew Prahlow - Travelers' encore_HQ.mp3"
    },
    {
        name: '潮鸣',
        artist: '折戸伸治',
        url: "/music/折戸伸治 - 潮鳴り (潮鸣).flac"
    }
    ]
});
</script>

<!-- **日文** -->
<!-- <div id="player2" class="aplayer-container"></div>
<script>
const ap2 = new APlayer({
    container: document.getElementById('player2'),
    audio: {
        name: '潮鸣',
        artist: '折戸伸治',
        url: "/music/折戸伸治 - 潮鳴り (潮鸣).flac"
    }
});
</script> -->

**中文**
<div id="player3" class="aplayer-container"></div>
<script>
const ap3 = new APlayer({
    container: document.getElementById('player3'),
    audio: {
        name: '没那么简单',
        artist: '黄小琥',
        url: "/music/没那么简单.mp3"
    }
});
</script>