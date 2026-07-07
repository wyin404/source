---
title: 酷狗概念版apiUI
date: 2026-07-06 10:00:00
type: page
comments: true
top: true
---

{% raw %}
<style>
/* ===== 只覆盖卡片内部样式，不干扰主题全局 ===== */
.kugo-app{max-width:800px;margin:0 auto;padding:20px 0}
.kugo-app .cards-grid{display:flex;flex-direction:column;gap:24px}
.kugo-app .card{background:var(--card-bg,#ffffff);border-radius:16px;padding:20px 24px;border:1px solid var(--border-color,#e8e8e8);transition:0.25s ease}
.kugo-app .card:hover{border-color:#1e8cf7;box-shadow:0 4px 16px rgba(30,140,247,0.08)}
.kugo-app .card-header{display:flex;align-items:center;gap:10px;font-size:17px;font-weight:600;margin-bottom:16px;color:var(--text-color,#222)}
.kugo-app .card-header .card-icon{font-size:22px}
.kugo-app .card-body{display:flex;flex-direction:column;gap:14px}
.kugo-app .card-body .sub-hint{font-size:13px;color:var(--text-secondary,#888);line-height:1.5;margin-top:8px}
.kugo-app .qr-wrapper{display:flex;flex-direction:column;align-items:center;gap:14px;background:var(--bg-color,#f5f5f5);border-radius:10px;padding:16px 12px 18px;border:1px solid var(--border-color,#e8e8e8)}
.kugo-app .qr-image{width:200px;height:200px;border-radius:10px;background:#f8fafc;display:flex;align-items:center;justify-content:center;border:1px solid #e8e8e8;overflow:hidden;flex-shrink:0}
.kugo-app .qr-image img{width:100%;height:100%;object-fit:contain;padding:8px}
.kugo-app .qr-image .qr-placeholder{color:#999;font-size:13px;text-align:center;padding:8px}
.kugo-app .qr-status-text{font-size:14px;font-weight:500;min-height:24px;text-align:center}
.kugo-app .qr-status-text .success{color:#22c55e}
.kugo-app .qr-status-text .error{color:#ef4444}
.kugo-app .qr-status-text .waiting{color:#f59e0b}
.kugo-app .qr-actions{display:flex;gap:10px;flex-wrap:wrap;justify-content:center}
.kugo-app .btn{padding:7px 20px;border:none;border-radius:30px;font-size:14px;font-weight:500;cursor:pointer;transition:0.25s ease;display:inline-flex;align-items:center;gap:6px;background:#e8e8e8;color:#222}
.kugo-app .btn-primary{background:#1e8cf7;color:white}
.kugo-app .btn-primary:hover{background:#0f6bc4;transform:translateY(-1px);box-shadow:0 4px 12px rgba(30,140,247,0.3)}
.kugo-app .btn-primary:disabled{opacity:0.5;cursor:not-allowed;transform:none;box-shadow:none}
.kugo-app .btn-outline{background:transparent;border:1.5px solid #e8e8e8}
.kugo-app .btn-outline:hover{border-color:#1e8cf7;color:#1e8cf7}
.kugo-app .btn-success{background:#22c55e;color:white}
.kugo-app .btn-success:hover{background:#16a34a;transform:translateY(-1px);box-shadow:0 4px 12px rgba(34,197,94,0.3)}
.kugo-app .btn-sm{padding:4px 14px;font-size:12px}
.kugo-app .vip-info{background:var(--bg-color,#f5f5f5);border-radius:10px;padding:14px 16px;border:1px solid var(--border-color,#e8e8e8);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:10px}
.kugo-app .vip-info .vip-label{font-size:14px;color:#888}
.kugo-app .vip-info .vip-value{font-weight:600;font-size:15px}
.kugo-app .vip-info .vip-value.active{color:#22c55e}
.kugo-app .vip-info .vip-value.inactive{color:#999}
.kugo-app .vip-result-box{background:var(--bg-color,#f5f5f5);border-radius:10px;padding:12px 16px;border:1px solid var(--border-color,#e8e8e8);min-height:44px;font-size:14px;display:flex;align-items:center;gap:8px;flex-wrap:wrap}
.kugo-app .vip-result-box .msg-success{color:#22c55e}
.kugo-app .vip-result-box .msg-error{color:#ef4444}
.kugo-app .vip-result-box .msg-info{color:#1e8cf7}
.kugo-app .search-box{display:flex;gap:10px}
.kugo-app .search-box input{flex:1;padding:8px 16px;border:1.5px solid #e8e8e8;border-radius:30px;font-size:14px;outline:none;transition:0.25s ease;background:white;min-width:0}
.kugo-app .search-box input:focus{border-color:#1e8cf7;box-shadow:0 0 0 3px rgba(30,140,247,0.12)}
.kugo-app .search-results{overflow-y:auto;background:var(--bg-color,#f5f5f5);border-radius:10px;border:1px solid var(--border-color,#e8e8e8);padding:4px 0;max-height:400px}
.kugo-app .search-results::-webkit-scrollbar{width:5px}
.kugo-app .search-results::-webkit-scrollbar-thumb{background:#ddd;border-radius:10px}
.kugo-app .result-item{display:flex;align-items:center;padding:10px 12px;border-bottom:1px solid #f1f3f6;cursor:pointer;transition:0.25s ease;gap:12px}
.kugo-app .result-item:last-child{border-bottom:none}
.kugo-app .result-item:hover{background:#e6f0ff}
.kugo-app .result-item .song-cover{width:48px;height:48px;border-radius:6px;flex-shrink:0;object-fit:cover;background:#f0f2f6}
.kugo-app .result-item .song-info{flex:1;min-width:0}
.kugo-app .result-item .song-name{font-weight:500;font-size:14px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.kugo-app .result-item .song-artist{font-size:12px;color:#888;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.kugo-app .result-item .play-btn{background:#1e8cf7;color:white;border:none;border-radius:50%;width:34px;height:34px;font-size:14px;cursor:pointer;transition:0.25s ease;flex-shrink:0;display:flex;align-items:center;justify-content:center}
.kugo-app .result-item .play-btn:hover{transform:scale(1.08);background:#0f6bc4}
.kugo-app .result-item .play-btn.playing{background:#22c55e}
.kugo-app .result-empty{padding:24px 16px;text-align:center;color:#999;font-size:14px}
.kugo-app .player-wrapper{background:var(--bg-color,#f5f5f5);border-radius:10px;border:1px solid var(--border-color,#e8e8e8);padding:12px 16px;display:flex;flex-direction:column;gap:8px;flex-shrink:0}
.kugo-app .player-wrapper .now-playing{font-size:13px;color:#888;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.kugo-app .player-wrapper audio{width:100%;height:40px;border-radius:8px;outline:none}
.kugo-app .toast-container{position:fixed;bottom:30px;left:50%;transform:translateX(-50%);z-index:999;display:flex;flex-direction:column;align-items:center;gap:8px;pointer-events:none}
.kugo-app .toast{background:#1a2332;color:white;padding:10px 28px;border-radius:30px;font-size:14px;font-weight:500;box-shadow:0 8px 30px rgba(0,0,0,0.2);pointer-events:auto;animation:toastIn 0.3s ease;max-width:90vw;text-align:center}
.kugo-app .toast.toast-success{background:#22c55e}
.kugo-app .toast.toast-error{background:#ef4444}
.kugo-app .toast.toast-warning{background:#f59e0b}
@keyframes toastIn{0%{opacity:0;transform:translateY(20px) scale(0.95)}100%{opacity:1;transform:translateY(0) scale(1)}}
@media (max-width:480px){.kugo-app .qr-image{width:160px;height:160px}.kugo-app .card{padding:16px}.kugo-app .search-box{flex-wrap:wrap}.kugo-app .search-box input{width:100%}.kugo-app .search-box .btn{width:100%;justify-content:center}.kugo-app .result-item .song-cover{width:40px;height:40px}}
</style>

<div class="kugo-app">
  <!-- 注意：这里不再包含头部菜单，直接使用主题的全局头部 -->
  <!-- ===== 三栏垂直卡片 ===== -->
  <div class="cards-grid">
    <!-- 卡片1: 扫码登录 -->
    <section class="card">
      <div class="card-header">
        <span class="card-icon"></span> 扫码登录
      </div>
      <div class="card-body">
        <div class="qr-wrapper">
          <div class="qr-image" id="qrImageContainer">
            <div class="qr-placeholder" id="qrPlaceholder">
              <!-- <span style="font-size:32px;display:block;margin-bottom:6px;">📷</span> -->
              点击下方生成二维码
            </div>
            <img id="qrImage" style="display:none;" alt="二维码" />
          </div>
          <div class="qr-status-text" id="qrStatusText">等待操作</div>
          <div class="qr-actions">
            <button class="btn btn-primary" id="qrGenerateBtn">🔄 生成二维码</button>
            <button class="btn btn-outline btn-sm" id="qrRefreshBtn" style="display:none;">⟳ 刷新</button>
          </div>
        </div>
        <div class="sub-hint"> 使用 <strong>酷狗概念版 App</strong> 扫码</div>
      </div>
    </section>
    <!-- 卡片2: 领取VIP -->
    <section class="card">
      <div class="card-header">
        <!-- <span class="card-icon">👑</span> 领取 VIP -->
      </div>
      <div class="card-body">
        <div class="vip-info">
          <span class="vip-label"> VIP 状态</span>
          <span class="vip-value inactive" id="vipStatusDisplay">未登录</span>
        </div>
        <button class="btn btn-success" id="vipClaimBtn">🎁 领取一天 VIP（概念版）</button>
        <div class="vip-result-box" id="vipResultBox">
          <span style="color:#999;font-size:13px;">点击按钮领取，每日限领一次</span>
        </div>
        <div class="sub-hint">⚠️ 测试接口，需登录</div>
      </div>
    </section>
    <!-- 卡片3: 搜索 & 播放 -->
    <section class="card">
      <div class="card-header">
        <!-- <span class="card-icon">🔍</span> 搜索 &amp; 播放 -->
      </div>
      <div class="card-body">
        <div class="search-box">
          <input type="text" id="searchInput" placeholder="输入歌名 / 歌手..." />
          <button class="btn btn-primary" id="searchBtn">搜索</button>
        </div>
        <div class="search-results" id="searchResults">
          <div class="result-empty">🔎 输入关键词开始搜索</div>
        </div>
        <div class="player-wrapper">
          <div class="now-playing" id="nowPlaying">🎵 未播放</div>
          <audio id="audioPlayer" controls preload="none"></audio>
        </div>
        <div class="sub-hint"> 点击 ▶ 播放</div>
      </div>
    </section>

  </div>
</div>

<!-- Toast 容器 -->
<div class="toast-container" id="toastContainer"></div>

<script>
// ============================================================
// 核心配置：使用相对路径 /api，走 Cloudflare Worker 代理
// ============================================================
var API_BASE = '/api';

// ===== 状态管理 =====
var state = {
  isLoggedIn: false,
  token: '',
  userId: '',
  dfid: '',
  cookieString: '',
  userNickname: '',
  qrKey: '',
  qrPollingTimer: null,
  qrPollingActive: false,
  currentSong: null,
  isPlaying: false
};

// ===== DOM 引用 =====
var $ = function(s) {
  var el = document.querySelector(s);
  return el;
};

var dom = {
  statusDot: $('#statusDot'),
  statusLabel: $('#statusLabel'),
  userNameDisplay: $('#userNameDisplay'),
  logoutBtn: $('#logoutBtn'),
  qrImage: $('#qrImage'),
  qrPlaceholder: $('#qrPlaceholder'),
  qrStatusText: $('#qrStatusText'),
  qrGenerateBtn: $('#qrGenerateBtn'),
  qrRefreshBtn: $('#qrRefreshBtn'),
  vipStatusDisplay: $('#vipStatusDisplay'),
  vipClaimBtn: $('#vipClaimBtn'),
  vipResultBox: $('#vipResultBox'),
  searchInput: $('#searchInput'),
  searchBtn: $('#searchBtn'),
  searchResults: $('#searchResults'),
  audioPlayer: $('#audioPlayer'),
  nowPlaying: $('#nowPlaying')
};

// ===== 工具函数 =====
function getTimestamp() { return Date.now(); }

function buildUrl(path, params) {
  params = params || {};
  var base = window.location.origin + API_BASE;
  var url = new URL(path, base + '/');
  params._t = getTimestamp();
  Object.keys(params).forEach(function(k) {
    if (params[k] !== undefined && params[k] !== null && params[k] !== '') {
      url.searchParams.append(k, params[k]);
    }
  });
  return url.toString();
}

async function apiFetch(path, params, options) {
  params = params || {};
  options = options || {};
  var url = buildUrl(path, params);
  console.log('[API] 请求:', url);
  var resp = await fetch(url, {
    method: options.method || 'GET',
    credentials: 'omit',
    headers: { 'Accept': 'application/json', ...(options.headers || {}) }
  });
  var text = await resp.text();
  console.log('[API] 原始响应:', text);
  try { return JSON.parse(text); } catch(e) {
    throw new Error('响应不是 JSON: ' + text.slice(0, 200));
  }
}

function showToast(msg, type, duration) {
  type = type || 'info';
  duration = duration || 3000;
  var c = document.getElementById('toastContainer');
  var el = document.createElement('div');
  el.className = 'toast toast-' + type;
  el.textContent = msg;
  c.appendChild(el);
  setTimeout(function() {
    el.style.opacity = '0';
    el.style.transform = 'translateY(10px)';
    setTimeout(function() { el.remove(); }, 300);
  }, duration);
}

function generateDfid() {
  return 'dfid_' + Math.random().toString(36).slice(2, 10) + '_' + Date.now().toString(36);
}

function buildCookieString() {
  if (!state.token) return '';
  return 'token=' + state.token + ';userid=' + (state.userId || '') + ';dfid=' + (state.dfid || generateDfid());
}

// ===== 获取歌曲封面 =====
function getSongCover(song) {
  var picId = song.pic_id || song.picId || song.album_pic || song.cover || song.img || '';
  if (picId) {
    if (picId.startsWith('http')) {
      return picId.replace(/^http:/, 'https:');
    }
    return 'https://imge.kugou.com/stdmusic/200/' + picId + '.jpg';
  }
  return '';
}

// ===== 更新登录UI =====
function updateLoginUI() {
  if (state.isLoggedIn && state.token) {
    dom.statusDot.className = 'status-dot online';
    dom.statusLabel.textContent = '已登录';
    dom.userNameDisplay.textContent = state.userNickname || '用户';
    dom.logoutBtn.style.display = 'inline-block';
    dom.vipStatusDisplay.textContent = '已登录';
    dom.vipStatusDisplay.className = 'vip-value active';
  } else {
    dom.statusDot.className = 'status-dot offline';
    dom.statusLabel.textContent = '未登录';
    dom.userNameDisplay.textContent = '';
    dom.logoutBtn.style.display = 'none';
    dom.vipStatusDisplay.textContent = '未登录';
    dom.vipStatusDisplay.className = 'vip-value inactive';
  }
}

// ===== 本地存储 =====
function saveAuth() {
  try {
    localStorage.setItem('kugou_auth', JSON.stringify({
      token: state.token,
      userId: state.userId,
      dfid: state.dfid,
      userNickname: state.userNickname,
      isLoggedIn: state.isLoggedIn
    }));
  } catch(_) {}
}

function loadAuth() {
  try {
    var raw = localStorage.getItem('kugou_auth');
    if (!raw) return false;
    var data = JSON.parse(raw);
    if (data.isLoggedIn && data.token) {
      state.token = data.token;
      state.userId = data.userId || '';
      state.dfid = data.dfid || generateDfid();
      state.userNickname = data.userNickname || '用户';
      state.isLoggedIn = true;
      state.cookieString = buildCookieString();
      updateLoginUI();
      dom.qrStatusText.innerHTML = '✅ 已恢复登录: ' + state.userNickname;
      dom.qrStatusText.className = 'qr-status-text success';
      dom.searchResults.innerHTML = '<div class="result-empty">🔎 已登录，可以开始搜索</div>';
      return true;
    }
  } catch(_) {}
  return false;
}

function clearAuth() {
  try { localStorage.removeItem('kugou_auth'); } catch(_) {}
}

// ===== 二维码登录 =====
async function generateQR() {
  try {
    dom.qrGenerateBtn.disabled = true;
    dom.qrGenerateBtn.textContent = '⏳ 生成中...';
    dom.qrStatusText.textContent = '⏳ 正在获取登录二维码...';
    var keyRes = await apiFetch('/login/qr/key');
    console.log('[QR] 完整响应:', keyRes);
    var qrKey = keyRes?.data?.qrcode;
    var qrimgBase64 = keyRes?.data?.qrcode_img;
    if (!qrKey || !qrimgBase64) {
      throw new Error('接口返回成功，但未解析到 qrcode 或 qrcode_img 字段');
    }
    state.qrKey = qrKey;
    dom.qrImage.src = qrimgBase64;
    dom.qrImage.style.display = 'block';
    dom.qrPlaceholder.style.display = 'none';
    dom.qrRefreshBtn.style.display = 'inline-block';
    dom.qrStatusText.innerHTML = '📲 请使用 <strong>酷狗概念版</strong> 扫码登录';
    dom.qrStatusText.className = 'qr-status-text waiting';
    showToast('✅ 二维码已生成，请扫码', 'success', 2000);
    startPolling(qrKey);
  } catch(err) {
    console.error('[QR] 错误:', err);
    dom.qrStatusText.innerHTML = '❌ ' + err.message;
    dom.qrStatusText.className = 'qr-status-text error';
    showToast('生成二维码失败: ' + err.message, 'error');
    dom.qrImage.style.display = 'none';
    dom.qrPlaceholder.style.display = 'block';
    dom.qrRefreshBtn.style.display = 'none';
  } finally {
    dom.qrGenerateBtn.disabled = false;
    dom.qrGenerateBtn.textContent = '🔄 重新生成';
  }
}

function startPolling(key) {
  if (state.qrPollingActive) {
    clearInterval(state.qrPollingTimer);
    state.qrPollingActive = false;
  }
  state.qrPollingActive = true;
  var attempt = 0;
  var maxAttempts = 120;
  dom.qrStatusText.innerHTML = '⏳ 等待扫码...';
  dom.qrStatusText.className = 'qr-status-text waiting';
  state.qrPollingTimer = setInterval(async function() {
    attempt++;
    if (attempt > maxAttempts) {
      clearInterval(state.qrPollingTimer);
      state.qrPollingActive = false;
      dom.qrStatusText.innerHTML = '⏰ 二维码已过期，请重新生成';
      dom.qrStatusText.className = 'qr-status-text error';
      showToast('二维码已过期，请重新生成', 'warning');
      return;
    }
    try {
      var checkData = await apiFetch('/login/qr/check', { key: key });
      console.log('[Polling] 轮询响应:', checkData);
      var code = null;
      var token = null;
      var userId = null;
      var nickname = null;
      if (checkData.data) {
        if (checkData.data.code !== undefined) {
          code = checkData.data.code;
          token = checkData.data.token || checkData.data.access_token || '';
          userId = checkData.data.userid || checkData.data.uid || '';
          nickname = checkData.data.nickname || checkData.data.username || '';
        } else if (checkData.data.status !== undefined) {
          code = checkData.data.status;
        }
      }
      if (code === null && checkData.code !== undefined) {
        code = checkData.code;
        token = checkData.token || '';
        userId = checkData.userid || '';
        nickname = checkData.nickname || '';
      }
      if (code === null && checkData.status !== undefined) {
        code = checkData.status;
      }
      if (code === null) {
        console.warn('[Polling] 无法提取状态码，完整响应:', checkData);
        return;
      }
      if (code === 0) {
        clearInterval(state.qrPollingTimer);
        state.qrPollingActive = false;
        dom.qrStatusText.innerHTML = '⏰ 二维码已过期，请重新生成';
        dom.qrStatusText.className = 'qr-status-text error';
        showToast('二维码已过期，请重新生成', 'warning');
        return;
      }
      if (code === 1) {
        dom.qrStatusText.innerHTML = '📲 等待扫码...';
        dom.qrStatusText.className = 'qr-status-text waiting';
        dom.statusDot.className = 'status-dot offline';
        dom.statusLabel.textContent = '未登录';
        return;
      }
      if (code === 2) {
        dom.qrStatusText.innerHTML = '✅ 已扫码，请在手机上确认登录';
        dom.qrStatusText.className = 'qr-status-text waiting';
        dom.statusDot.className = 'status-dot scanning';
        dom.statusLabel.textContent = '扫码确认中...';
        return;
      }
      if (code === 4) {
        clearInterval(state.qrPollingTimer);
        state.qrPollingActive = false;
        if (!token) {
          if (checkData.data) {
            token = checkData.data.token || checkData.data.access_token || '';
            userId = checkData.data.userid || checkData.data.uid || '';
            nickname = checkData.data.nickname || checkData.data.username || '';
          }
          if (!token) {
            token = checkData.token || '';
            userId = checkData.userid || '';
            nickname = checkData.nickname || '';
          }
        }
        if (!token) {
          console.error('[Polling] 登录成功但未获取到 token');
          showToast('登录成功但 token 缺失，请重试', 'error');
          dom.qrStatusText.innerHTML = '❌ 登录异常，请重新扫码';
          dom.qrStatusText.className = 'qr-status-text error';
          return;
        }
        state.isLoggedIn = true;
        state.token = token;
        state.userId = userId || '';
        state.dfid = state.dfid || generateDfid();
        state.userNickname = nickname || '用户';
        state.cookieString = buildCookieString();
        dom.qrStatusText.innerHTML = '🎉 登录成功！欢迎 <strong>' + state.userNickname + '</strong>';
        dom.qrStatusText.className = 'qr-status-text success';
        dom.statusDot.className = 'status-dot online';
        dom.statusLabel.textContent = '已登录';
        dom.userNameDisplay.textContent = state.userNickname;
        dom.logoutBtn.style.display = 'inline-block';
        dom.vipStatusDisplay.textContent = '已登录';
        dom.vipStatusDisplay.className = 'vip-value active';
        dom.searchResults.innerHTML = '<div class="result-empty">🔎 已登录，可以开始搜索了</div>';
        showToast('🎉 登录成功！欢迎 ' + state.userNickname, 'success', 3000);
        saveAuth();
        return;
      }
      dom.qrStatusText.innerHTML = '⏳ 状态: ' + code + '，等待中...';
      dom.qrStatusText.className = 'qr-status-text waiting';
    } catch(err) {
      console.error('[Polling] 轮询错误:', err);
    }
  }, 2000);
}

// ===== 退出登录 =====
function logout() {
  if (state.qrPollingActive) {
    clearInterval(state.qrPollingTimer);
    state.qrPollingActive = false;
  }
  state.isLoggedIn = false;
  state.token = '';
  state.userId = '';
  state.dfid = '';
  state.cookieString = '';
  state.userNickname = '';
  state.currentSong = null;
  state.isPlaying = false;
  dom.audioPlayer.pause();
  dom.audioPlayer.src = '';
  dom.nowPlaying.textContent = '🎵 未播放';
  updateLoginUI();
  dom.qrStatusText.innerHTML = '已退出，请重新扫码登录';
  dom.qrStatusText.className = 'qr-status-text';
  dom.qrImage.style.display = 'none';
  dom.qrPlaceholder.style.display = 'block';
  dom.qrRefreshBtn.style.display = 'none';
  dom.searchResults.innerHTML = '<div class="result-empty">🔎 请先登录后再搜索</div>';
  dom.vipResultBox.innerHTML = '<span style="color:#999;font-size:13px;">已退出登录</span>';
  clearAuth();
  showToast('已退出登录', 'info');
}

// ===== 领取VIP =====
async function claimVip() {
  if (!state.isLoggedIn || !state.token) {
    showToast('请先扫码登录', 'warning');
    dom.vipResultBox.innerHTML = '<span class="msg-error">⚠️ 请先登录后再领取 VIP</span>';
    return;
  }
  try {
    dom.vipClaimBtn.disabled = true;
    dom.vipClaimBtn.textContent = '⏳ 领取中...';
    dom.vipResultBox.innerHTML = '<span class="msg-info">⏳ 正在领取...</span>';
    var resp = await apiFetch('/youth/vip', { cookie: buildCookieString() });
    console.log('[VIP] 完整响应:', resp);
    var isSuccess = false;
    var msg = '';
    if (resp.code !== undefined) {
      if (resp.code === 200 || resp.code === 0) isSuccess = true;
    }
    if (!isSuccess && resp.status !== undefined) {
      if (resp.status === 1 || resp.status === 200) isSuccess = true;
    }
    if (!isSuccess && resp.error_code !== undefined && resp.error_code === 0) {
      isSuccess = true;
    }
    if (!isSuccess && resp.data) {
      var d = resp.data;
      if (d.code === 200 || d.code === 0 || d.status === 1 || d.error_code === 0) isSuccess = true;
    }
    msg = resp.msg || resp.message || resp.data?.msg || resp.data?.message || '';
    if (isSuccess) {
      var successMsg = msg || '领取成功！';
      dom.vipResultBox.innerHTML = '<span class="msg-success">✅ ' + successMsg + '</span>';
      showToast('🎁 ' + successMsg, 'success');
    } else {
      var errMsg = msg || resp.errMsg || resp.error || '接口暂不可用';
      dom.vipResultBox.innerHTML = '<span class="msg-error">❌ ' + errMsg + '</span>';
      showToast('领取失败: ' + errMsg, 'error');
    }
  } catch(err) {
    console.error('[VIP] 错误:', err);
    dom.vipResultBox.innerHTML = '<span class="msg-error">❌ 请求失败: ' + err.message + '</span>';
    showToast('领取失败: ' + err.message, 'error');
  } finally {
    dom.vipClaimBtn.disabled = false;
    dom.vipClaimBtn.textContent = '🎁 领取一天 VIP（概念版）';
  }
}

// ===== 搜索（带封面） =====
async function performSearch(keyword) {
  keyword = keyword.trim();
  if (!keyword) { showToast('请输入搜索关键词', 'warning'); return; }
  if (!state.isLoggedIn || !state.token) {
    showToast('请先扫码登录', 'warning');
    dom.searchResults.innerHTML = '<div class="result-empty">🔒 请先登录后再搜索</div>';
    return;
  }
  try {
    dom.searchBtn.disabled = true;
    dom.searchBtn.textContent = '⏳ 搜索中...';
    dom.searchResults.innerHTML = '<div class="result-empty">⏳ 搜索中...</div>';
    var resp = await apiFetch('/search', {
      keywords: keyword,
      page: 1,
      pagesize: 30,
      type: 'song',
      cookie: buildCookieString()
    });
    console.log('[Search] 完整响应:', resp);
    var isSuccess = false;
    var errMsg = '';
    if (resp.code !== undefined) {
      if (resp.code === 200 || resp.code === 0) isSuccess = true;
      else errMsg = resp.msg || resp.message || '';
    }
    if (!isSuccess && resp.status !== undefined) {
      if (resp.status === 1 || resp.status === 200) isSuccess = true;
    }
    if (!isSuccess && resp.error_code !== undefined && resp.error_code === 0) {
      isSuccess = true;
    }
    if (!isSuccess && resp.data) {
      var d = resp.data;
      if (d.code === 200 || d.code === 0 || d.status === 1 || d.error_code === 0) isSuccess = true;
    }
    if (!isSuccess) {
      var failMsg = errMsg || resp.msg || resp.message || '搜索失败';
      dom.searchResults.innerHTML = '<div class="result-empty">❌ ' + failMsg + '</div>';
      showToast('搜索失败: ' + failMsg, 'error');
      return;
    }
    var songs = [];
    if (resp.data) {
      if (resp.data.lists) songs = resp.data.lists;
      else if (resp.data.list) songs = resp.data.list;
      else if (resp.data.songs) songs = resp.data.songs;
      else if (resp.data.result) songs = resp.data.result;
      else if (Array.isArray(resp.data)) songs = resp.data;
    }
    if (!songs || songs.length === 0) {
      if (resp.lists) songs = resp.lists;
      else if (resp.list) songs = resp.list;
      else if (resp.songs) songs = resp.songs;
      else if (resp.result) songs = resp.result;
      else if (Array.isArray(resp)) songs = resp;
    }
    console.log('[Search] 提取到的歌曲列表:', songs);
    if (!songs || songs.length === 0) {
      dom.searchResults.innerHTML = '<div class="result-empty">😕 没有找到相关歌曲</div>';
      return;
    }
    var html = '';
    songs.forEach(function(song, index) {
      var name = song.FileName || song.songname || song.name || song.title || '未知歌曲';
      var artist = song.SingerName || song.singername || song.artist || song.singer || '未知歌手';
      var hash = song.hash || song.Hash || song.FileHash || '';
      var songId = song.songid || song.id || song.SongId || '';
      var playUrl = song.url || song.play_url || song.mp3url || '';
      var identifier = hash || songId || '';
      var cover = getSongCover(song);
      var coverHtml = cover ? '<img class="song-cover" src="' + cover + '" alt="封面" onerror="this.style.display=\'none\'" />' :
                              '<div class="song-cover" style="background:#e8e8e8;display:flex;align-items:center;justify-content:center;font-size:20px;color:#999;">🎵</div>';
      html += '<div class="result-item" data-identifier="' + identifier + '" data-url="' + playUrl + '" data-name="' + name + '" data-artist="' + artist + '">' +
              coverHtml +
              '<div class="song-info"><div class="song-name">' + name + '</div><div class="song-artist">' + artist + '</div></div>' +
              '<button class="play-btn" title="播放">▶</button></div>';
    });
    dom.searchResults.innerHTML = html;
    dom.searchResults.querySelectorAll('.result-item').forEach(function(item) {
      var btn = item.querySelector('.play-btn');
      var url = item.dataset.url;
      var name = item.dataset.name;
      var artist = item.dataset.artist;
      var identifier = item.dataset.identifier;
      btn.addEventListener('click', function(e) {
        e.stopPropagation();
        if (url) {
          playSong(url, name, artist);
        } else if (identifier) {
          fetchSongUrl(identifier, name, artist);
        } else {
          showToast('该歌曲缺少播放标识符', 'warning');
        }
      });
      item.addEventListener('dblclick', function() { btn.click(); });
    });
    showToast('找到 ' + songs.length + ' 首歌曲', 'success', 1500);
  } catch(err) {
    console.error('[Search] 错误:', err);
    dom.searchResults.innerHTML = '<div class="result-empty">❌ 请求失败: ' + err.message + '</div>';
    showToast('搜索失败: ' + err.message, 'error');
  } finally {
    dom.searchBtn.disabled = false;
    dom.searchBtn.textContent = '搜索';
  }
}

// ===== 播放 =====
function playSong(url, name, artist) {
  if (!url) { showToast('播放链接无效', 'error'); return; }
  var player = dom.audioPlayer;
  var display = name + ' - ' + artist;
  if (state.currentSong && state.currentSong.url === url && !player.paused) {
    player.pause();
    dom.nowPlaying.textContent = '⏸️ ' + display;
    state.isPlaying = false;
    updatePlayButtons(false);
    return;
  }
  player.src = url;
  player.load();
  player.play().catch(function(err) {
    console.error('[Play] 播放失败:', err);
    showToast('播放失败: ' + err.message, 'error');
  });
  state.currentSong = { url: url, name: name, artist: artist };
  state.isPlaying = true;
  dom.nowPlaying.textContent = '▶️ ' + display;
  updatePlayButtons(true);
  player.onended = function() {
    state.isPlaying = false;
    dom.nowPlaying.textContent = '🎵 ' + display + ' (已结束)';
    updatePlayButtons(false);
  };
  player.onerror = function(e) {
    console.error('[Play] 播放器错误:', e);
    showToast('播放出错，请尝试其他歌曲', 'error');
    state.isPlaying = false;
    updatePlayButtons(false);
  };
  showToast('🎵 正在播放: ' + display, 'success', 1500);
}

// ===== 获取播放链接 =====
async function fetchSongUrl(identifier, name, artist) {
  try {
    showToast('正在获取播放链接...', 'info', 1500);
    var params = {};
    if (/^\d+$/.test(identifier)) {
      params.id = identifier;
    } else {
      params.hash = identifier;
    }
    var resp = await apiFetch('/song/url', Object.assign({}, params, { cookie: buildCookieString() }));
    console.log('[SongUrl] 主接口响应:', resp);
    var playUrl = null;
    if (resp) {
      if (resp.url && Array.isArray(resp.url) && resp.url.length > 0) {
        playUrl = resp.url[0];
      } else if (resp.backupUrl && Array.isArray(resp.backupUrl) && resp.backupUrl.length > 0) {
        playUrl = resp.backupUrl[0];
      } else if (resp.data && resp.data.url && Array.isArray(resp.data.url) && resp.data.url.length > 0) {
        playUrl = resp.data.url[0];
      } else if (resp.data && resp.data.backupUrl && Array.isArray(resp.data.backupUrl) && resp.data.backupUrl.length > 0) {
        playUrl = resp.data.backupUrl[0];
      } else if (typeof resp.url === 'string' && resp.url.startsWith('http')) {
        playUrl = resp.url;
      }
    }
    if (!playUrl) {
      console.warn('[SongUrl] 主接口未获取到链接，尝试备用接口...');
      var resp2 = await apiFetch('/song/playurl', Object.assign({}, params, { cookie: buildCookieString() }));
      console.log('[SongUrl] 备用接口响应:', resp2);
      if (resp2) {
        if (resp2.url && Array.isArray(resp2.url) && resp2.url.length > 0) {
          playUrl = resp2.url[0];
        } else if (resp2.data && resp2.data.url && Array.isArray(resp2.data.url) && resp2.data.url.length > 0) {
          playUrl = resp2.data.url[0];
        }
      }
    }
    if (playUrl) {
      // 使用 Worker 代理播放
      var proxyUrl = '/audio?url=' + encodeURIComponent(playUrl);
      console.log('[SongUrl] 通过 Worker 代理播放:', proxyUrl);
      await playSong(proxyUrl, name, artist);
    } else {
      console.error('[SongUrl] 所有接口均未返回有效链接');
      showToast('无法获取播放链接，请尝试其他歌曲', 'error');
    }
  } catch(err) {
    console.error('[SongUrl] 错误:', err);
    showToast('获取播放链接失败: ' + err.message, 'error');
  }
}

function updatePlayButtons(isPlaying) {
  dom.searchResults.querySelectorAll('.play-btn').forEach(function(btn) {
    if (isPlaying) {
      btn.classList.add('playing');
      btn.textContent = '⏸';
    } else {
      btn.classList.remove('playing');
      btn.textContent = '▶';
    }
  });
}

// ===== 初始化 =====
function init() {
  var restored = loadAuth();
  if (!restored) {
    updateLoginUI();
    dom.searchResults.innerHTML = '<div class="result-empty">🔒 请先扫码登录</div>';
  } else {
    dom.statusDot.className = 'status-dot online';
    dom.statusLabel.textContent = '已登录';
    dom.userNameDisplay.textContent = state.userNickname || '用户';
    dom.logoutBtn.style.display = 'inline-block';
    dom.vipStatusDisplay.textContent = '已登录';
    dom.vipStatusDisplay.className = 'vip-value active';
  }
  dom.qrGenerateBtn.addEventListener('click', generateQR);
  dom.qrRefreshBtn.addEventListener('click', generateQR);
  dom.logoutBtn.addEventListener('click', logout);
  dom.vipClaimBtn.addEventListener('click', claimVip);
  dom.searchBtn.addEventListener('click', function() { performSearch(dom.searchInput.value); });
  dom.searchInput.addEventListener('keydown', function(e) {
    if (e.key === 'Enter') {
      e.preventDefault();
      performSearch(dom.searchInput.value);
    }
  });
  dom.audioPlayer.addEventListener('play', function() {
    state.isPlaying = true;
    if (state.currentSong) {
      dom.nowPlaying.textContent = '▶️ ' + state.currentSong.name + ' - ' + state.currentSong.artist;
    }
    updatePlayButtons(true);
  });
  dom.audioPlayer.addEventListener('pause', function() {
    state.isPlaying = false;
    if (state.currentSong) {
      dom.nowPlaying.textContent = '⏸️ ' + state.currentSong.name + ' - ' + state.currentSong.artist;
    }
    updatePlayButtons(false);
  });
  dom.audioPlayer.addEventListener('ended', function() {
    state.isPlaying = false;
    updatePlayButtons(false);
  });
}

document.addEventListener('DOMContentLoaded', init);
</script>
{% endraw %}