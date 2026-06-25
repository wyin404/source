---
title: 音乐
date: 2026-6-17 00:01:00
comments: false
aplayer: true
---
播放器未加載請刷新網頁，加载缓慢耐心等待，可以留意你设备的实时网络吞吐量，极小请退出本页重进,功能开发不完善敬请谅解。
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
</script>