---
title: 视频
date: 2026-6-17 00:01:00
aside: false
---
### ⚡⚡⚡我看过最权威的买瓜⚡⚡⚡
<div style="position: relative; width: 100%; max-width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; background: #000;">
    <iframe 
        src="//player.bilibili.com/player.html?bvid=BV1vwLX6yEM2&page=1&danmaku=0&high_quality=1&autoplay=0" 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;" 
        allowfullscreen>
    </iframe>
</div>
<script>
    // 等待播放器加载完成后尝试调音量
    window.addEventListener('load', function() {
        setTimeout(function() {
            var iframe = document.getElementById('bilibili-player');
            // 注意：这种方式在跨域下可能受限，不一定生效
            iframe.contentWindow.postMessage({ command: 'setVolume', value: 100 }, '*');
        }, 3000);
    });
</script>