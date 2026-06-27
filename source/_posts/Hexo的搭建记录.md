---
title: Hexo的搭建记录
date: 2026-06-17 15:56:05
tags:
  - 技术
  - 开源
cover: cover.png
sticky: 100
---
###### 只将自己研究的部分开源了
# 起因是找资源发现一位up将资源存在个人博客
觉着新奇就想自己来试试然后就一发不可收拾
up的blog[莱姆Lime](https://sudachi.top)个人认为非常精美，甚至不敢相信是用hexo框架搭建的，而其GitHub主页[LimeBlogs](https://github.com/LimeBlogs)个性签还写道“业余爱好者，非码农”也足以看出其技术之深了

## 第一位恩师“枸杞加水"
通过up的视频正式入门搭建Hexo,这位up的主页我也添加到[友链](/link/)了我会记住他的

## 第二位恩师“--Fomalhaut”
他的视频将一系列的教程打包成套非常详细，可以说本站大部分的开发都由其指导，当然他的主页也在[友链](/link/)

## 之后的开发涉及一些计算机语言，对众的视频也难以支撑我解决一些细小问题
我直接就掏出我的deepseek，用的时候很难不笑出声，本地编写保存报错，直接把报错信息复制粘贴，拿到解决代码再复制粘贴。。
当然在部署评论时我也会独自钻研产品说明一些问题也可以通过说明书解决，虽然大多还是复制粘贴。。
通过部署评论我也学习了一些域名相关领域的知识（本来不想买域名，想直接裸奔网站的奈何部署评论的服务器域名被墙了只能买了）了解了cf‘cloudflare’的伟大，域名的投资性，ipv6等等受益匪浅2026年6月17日

## 主题美化，加装时钟
本来我还纳闷为什么butterfly主题自带时钟在yaml里调用不起来，后来再找别的第三方插件时钟时才发现butterfly主题的活跃度太低，一些开发者早就停止支持调用他们搭建的时钟（就是网址404），做到这里我也是真后悔用这个主题了。然后我就和deepseek一拍即合，让祂帮我写了一个时钟，这里我了解到了一个网页内容的开发需要用到css、javascript、html、yaml等多种语言，也是畏惧了好吧。祂的努力成果在此奉上。

**一：配置inject，通过其注入html**

用到yaml
```yaml

inject:
  head:
    - <link rel="stylesheet" href="/css/clock.css">
  bottom:
    - <script src="/js/clock.js"></script>
```
**二：配置时钟**

1、编写样式相当于ui界面用到css注*保存至根目录/css文件夹下
```css

/* 时钟卡片样式 */
#clock-card {
  margin: 0 12px 15px;
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-radius: 12px;
  padding: 20px 18px 18px;
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.15);
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

#clock-card:hover {
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.10);
  transform: translateY(-2px);
}

#clock-date {
  font-size: 13px;
  letter-spacing: 2px;
  font-weight: 300;
  opacity: 0.8;
  margin-bottom: 6px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}

#clock-time {
  font-size: 38px;
  font-weight: 700;
  font-family: "Courier New", Consolas, monospace;
  letter-spacing: 4px;
  line-height: 1.3;
  text-shadow: 0 0 30px rgba(255, 255, 255, 0.15);
}

/* 暗色模式适配 */
[data-theme="dark"] #clock-card {
  background: rgba(30, 30, 40, 0.5);
  border-color: rgba(255, 255, 255, 0.06);
}

[data-theme="dark"] #clock-date {
  color: #b0b0b0;
}

[data-theme="dark"] #clock-time {
  color: #f0f0f0;
}
```
2、编写时钟规则用到javascript注*保存至根目录/js文件夹下
```js

(function() {
  'use strict';

  // ---------- 创建HTML容器（使用更安全的方式） ----------
  var container = document.createElement('div');
  // 用 classList.add 替代 className 赋值，避免空值问题
  container.classList.add('card-widget');
  container.id = 'clock-card';

  // 创建内部结构
  var content = document.createElement('div');
  content.className = 'card-content';

  var display = document.createElement('div');
  display.id = 'clock-display';

  var dateEl = document.createElement('div');
  dateEl.id = 'clock-date';
  var timeEl = document.createElement('div');
  timeEl.id = 'clock-time';

  display.appendChild(dateEl);
  display.appendChild(timeEl);
  content.appendChild(display);
  container.appendChild(content);

  // ---------- 插入到侧边栏 ----------
  function insertClock() {
    var sidebar = document.querySelector('.aside-content');
    if (sidebar) {
      // 插入到第一个子元素之前
      sidebar.insertBefore(container, sidebar.firstChild);
      return true;
    }
    return false;
  }

  if (!insertClock()) {
    // 如果侧边栏还没加载，等DOM加载完再试
    document.addEventListener('DOMContentLoaded', function() {
      if (!insertClock()) {
        // 实在找不到侧边栏，就追加到 body（兜底）
        document.body.appendChild(container);
      }
    });
  }

  // ---------- 时钟更新逻辑 ----------
  var dateDisplay = document.getElementById('clock-date');
  var timeDisplay = document.getElementById('clock-time');
  var weekDays = ['日', '一', '二', '三', '四', '五', '六'];

  function updateClock() {
    if (!dateDisplay || !timeDisplay) return;
    var now = new Date();
    var year = now.getFullYear();
    var month = String(now.getMonth() + 1).padStart(2, '0');
    var day = String(now.getDate()).padStart(2, '0');
    var week = weekDays[now.getDay()];
    var hours = String(now.getHours()).padStart(2, '0');
    var minutes = String(now.getMinutes()).padStart(2, '0');
    var seconds = String(now.getSeconds()).padStart(2, '0');

    dateDisplay.textContent = year + '-' + month + '-' + day + ' 星期' + week;
    timeDisplay.textContent = hours + ':' + minutes + ':' + seconds;
  }

  // 初始更新
  updateClock();
  // 每秒更新
  setInterval(updateClock, 1000);

})();
```
**三：编写HTML容器，相当于写放的位置，本来应该和第一步和一起的，但在yaml文件里写html一直报错**

用到HTML注*保存至根目录/_data文件夹下
```html

<div id="clock-card" class="card-widget">
  <div class="card-content">
    <div id="clock-display">
      <div id="clock-date"></div>
      <div id="clock-time"></div>
    </div>
  </div>
</div>
```
这还是我跟祂掰扯半天才实践出的可行方案，美中不足，不，应该是美中有大不足，运行网站控制台还有一条报错，引导看上去是别的插件冲突了但我怎么删也删不掉，我会永远记着这个报错的✋😭🤚
当然美化不止这点，跟着--Fomalhaut我搞定了背景一图，板块动效，字体更换等等。。我也会继续建设本站的，等基础搞完了还有优化，数据迁移等着呢🤣2026年6月18日

## 还是美化加装毛玻璃效果还是代码奉上
css部分
```css

/* ===== 文章卡片 ===== */
.recent-post-item {
  background: rgba(255, 255, 255, 0.25) !important;
  backdrop-filter: blur(8px) !important;
  -webkit-backdrop-filter: blur(8px) !important;
  border: 1px solid rgba(255, 255, 255, 0.15) !important; /* 加个细边框更精致 */
}

/* ===== 侧边栏所有卡片 ===== */
.card-widget {
  background: rgba(255, 255, 255, 0.25) !important;
  backdrop-filter: blur(8px) !important;
  -webkit-backdrop-filter: blur(8px) !important;
  border: 1px solid rgba(255, 255, 255, 0.15) !important;
}

/* ===== （可选）文章封面图区域 ===== */
.recent-post-item .post_cover {
  background: transparent !important; /* 让封面图不遮挡毛玻璃效果 */
}

/* ===== （可选）文章标题和摘要文字颜色调深一点，保证可读性 ===== */
.recent-post-item .recent-post-info .article-title,
.recent-post-item .recent-post-info .article-meta-wrap,
.recent-post-item .recent-post-info .content {
  color: #333 !important; /* 深色文字，浅色背景时用 */
}

/* 如果是深色背景，用白色文字 */
/* .recent-post-item .recent-post-info .article-title {
  color: #fff !important;
} */
```
yaml部分这个简单就是让主题识别配置文件
```yaml
inject:
  head:
    - <link rel="stylesheet" href="/css/glass.css">
```
还有一些功能的调整，qq链接按钮（虽然整的就是依托），邮箱404修复，时钟位置大小调整，一些小动画调整。
越往后写越觉得我改的就是一座屎山，有的动画没删源码直接用css覆盖，新建的源文件得着一个文件夹就乱放，没用的图片找不到在哪删不掉，有用的文件失手说删就删，我还把404界面头图给404了真给自己逗笑了😋

## 大制作右下角设置加了个切换字体按钮

rt

![](/images/1.png)过程👇

**一、编写样式，极简版（其实是不想费劲加底了）**
```css
/* 声明自定义字体用,默认字体不用这段 */
@font-face {
    font-family: '圆滑';
    src: url(/font/你的字体);
    font-weight: 900 !important;
}
/* 字体切换面板 */
#font-panel {
  position: absolute;
  bottom: 60px;
  right: 0;
  background: var(--card-bg);
  border-radius: 12px;
  padding: 12px 16px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  min-width: 140px;
  z-index: 100;
  border: 1px solid var(--border-color);
}

#font-panel .font-option {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 14px;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.2s;
  gap: 20px;
}

#font-panel .font-option:hover {
  background: var(--grey-2);
}

#font-panel .font-option.active {
  background: var(--theme-color);
  color: #3c83ce;
}

#font-panel .font-option .font-sample {
  font-size: 18px;
}

.font-option[data-font="default"] .font-sample {
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
}

.font-option[data-font="serif"] .font-sample {
  font-family: '圆滑', serif;/* 默认字体换成font-family: Georgia, “Times New Roman", Times, serif; */
}
```
这是一个默认字体一个本地字体的样式，想两个字体都是系统自带的看注释，但说实话没人想费半天劲就为了搞两个默认字体吧

**二、修改主题模板**

这个文件在node_modules/hexo-theme-butterfly/layout/includes/rightside.pug
```pug

#rightside
  #rightside-config-hide
    if hideArray.length
      +rightsideItem(hideArray)
    
    // ===== 字体切换 =====
    .rightside-item
      a#font-toggle-btn(title='字体切换')
        i.fas.fa-font
    
    #font-panel(style='display:none')
      // 默认字体
      .font-option(data-font='default' onclick='setFont("default")')
        span 默认字体
        span.font-sample Aa
      // 自定义字体（替换原来的衬线字体）
      .font-option(data-font='custom' onclick='setFont("custom")')
        span 我的字体  // 改成想要的名称想要默认就写和上面一样的
        span.font-sample Aa

  #rightside-config-show
    if needCogBtn
      button#rightside-config(type="button" title=_p("rightside.setting"))
        i.fas.fa-cog(class=theme.rightside_config_animation ? 'fa-spin' : '')

    if showArray.length
      +rightsideItem(showArray)

    button#go-up(type="button" title=_p("rightside.back_to_top"))
      span.scroll-percent
      i.fas.fa-arrow-up
```
**三、写JavaScript逻辑**

文件插进之前的魔改js也行，新建一个也行，建议新建，弄不好直接删文件就行
```js

// ===== 字体切换功能（两种字体） =====
(function() {
  'use strict';

  // 1. 获取保存的字体偏好
  let currentFont = localStorage.getItem('butterfly_font') || 'default';

  // 2. 字体映射表
  const fontMap = {
    default: 'system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", sans-serif',
    custom: "'圆滑',serif"//这里用默认的话写serif: 'Georgia, "Times NewRoman", Times,serif'
  };

  // 3. 应用字体到页面
  function applyFont(fontValue) {
    // 设置 CSS 变量
    document.documentElement.style.setProperty('--font-family', fontMap[fontValue] || fontMap.default);
    
    // 如果主题使用 body 直接设置，也加上
    document.body.style.fontFamily = fontMap[fontValue] || fontMap.default;
    
    // 保存到本地
    localStorage.setItem('butterfly_font', fontValue);
    currentFont = fontValue;

    // 更新面板选中状态
    document.querySelectorAll('.font-option').forEach(function(el) {
      if (el.dataset.font === fontValue) {
        el.classList.add('active');
      } else {
        el.classList.remove('active');
      }
    });
  }

  // 4. 切换面板显示/隐藏
  function toggleFontPanel() {
    var panel = document.getElementById('font-panel');
    if (panel) {
      var isHidden = panel.style.display === 'none' || panel.style.display === '';
      panel.style.display = isHidden ? 'block' : 'none';
    }
  }

  // 5. 设置字体（全局函数，供 onclick 调用）
  window.setFont = function(fontValue) {
    applyFont(fontValue);
    // 选择后自动关闭面板
    var panel = document.getElementById('font-panel');
    if (panel) {
      panel.style.display = 'none';
    }
  };

  // 6. 绑定按钮点击事件
  document.addEventListener('DOMContentLoaded', function() {
    var btn = document.getElementById('font-toggle-btn');
    if (btn) {
      btn.addEventListener('click', function(e) {
        e.preventDefault();
        e.stopPropagation();
        toggleFontPanel();
      });
    }

    // 点击面板外部关闭
    document.addEventListener('click', function(e) {
      var panel = document.getElementById('font-panel');
      var btn = document.getElementById('font-toggle-btn');
      if (panel && panel.style.display === 'block') {
        if (!panel.contains(e.target) && !btn.contains(e.target)) {
          panel.style.display = 'none';
        }
      }
    });

    // 初始化字体
    applyFont(currentFont);
  });

})();
```

**四、检查新文件是否注入到主题文件**
```yaml

inject:
  head:
    - <link rel="stylesheet" href="/css/custom.css"> # 新文件相对位置如果是插入到旧文件就不用管
  bottom:
    - <script src="/js/change.js"></script> # 同上
```
然后你就惊喜的发现按钮生效了，重申上文为一默认一自定义字体，也推荐这样，想两个都是自带字体看注释（不建议，我注释的可能不准）

就这样吧以后也不打算在这里写那些代码了，已经够长了，但还会分享经历的🌹2026年6月18日

## 功能开发加装音乐播放并建造图片＆文件的存放仓库通过cdn调用优化加载速度
我不是很喜欢音乐放主页或黏到网页底部，所以只开发了音乐界面的播放器（贼费劲，开始看butterfly的官贴直接调用内置的css和js，但他是所有界面都生效，也可能是我没找到管这个开关，然后就自己用inject注入，只在music页面插入，本地测试，然后网页就各种报错，排查了好几项，个把小时最后发现是调用内置打开后忘关了，和自己注入的冲突🤣，有惊无险。
然后是图床和文件床？从网上找教程，建仓上传然后用~~jsdelivrCDN~~vercel调用，图片放的太散，看到哪个再顺手上传哪个吧，希望加载速度会有所提升（压力太大我老爷手机都加载不出来了😭😭😭）2026年6月19日

## 一些杂项更新
加装hexo-hide-posts插件，hexo-blog-encrypt插件，实现了帖子的隐藏与加密。禁用了pjax功能，修复了时钟、音乐播放器加载必须需刷新页面才能显示，代价是加载速度拖慢。禁用了首页文章头图鼠标悬停放大动画，我不喜欢。还有就是不打算再用cdn了太慢，好容易才找到一个国内免费的edgeone page结果需要icp备案，这不符合我免费建站的初衷😋果断放弃，打算把文件放到博客本地文件夹。把loading动画改为自定义gif，终于不是居中的小蓝条了😋😋😋现在的效果↓↓↓![](/images/loading.gif)2026年6月21日

## 一些杂项更新
修复加载页白屏，优化加载页加载速度（doge。加了一个置顶图片轮播图，效果来自公众号“前端也能这么有趣”。公众号里还有挺多有趣的前端效果抽空再看看。修复手机端菜单全白，现在子菜单背景黑色和主菜单白色冲突已经是最好的效果了，因为涉及到pc端背景。做到这里已经有点倦了，试着减缓搭建强度，但我就怕缓着缓着我直接把这玩意忘了直接弃坑😜2026年6月24日

## 一些杂项更新
修复首页文章预览卡片撑不满父容器的问题，以及调整了父容器宽度，手机端现在看预览卡片应该和信息卡片宽度一致。找了一些好康的放在图册😋。建立专门仓库用于备份并将源文件推送至其中。修复了一些其他的已知问题并吃了份蛋炒饭🥰2026年6月25日

## 一些杂项更新
加载页加了个渐变进度条，想用莱姆用的那个的但死活找不到，我用的这个效果来自up'写代码的浩'的[视频](https://www.bilibili.com/video/BV1zy4y1o7cn/?spm_id_from=333.1387.top_right_bar_window_history.content.click&vd_source=96733384bf15585ec8491a7b7afc7799)感觉效果和莱姆的大差不差。更新了一批好康的图片。添加了hexo-neat插件压缩整理配置文件，优化速度。修复了一些其他已知问题并吃了份凉菜😋2026年6月26日

## 加了一些逆天玩意、更新
菜单栏列表里多了一个神秘游戏选项，我不多说自己[去体验](/game/)，哦对了记得带一把糯米再点进去😋。移除了一些用不到侧边栏页面的侧边栏，强迫症把字体切换按钮加了个底,附带白天黑夜颜色切换。修复了一些其他已知问题并吃了份螺狮粉😘2026年6月27日