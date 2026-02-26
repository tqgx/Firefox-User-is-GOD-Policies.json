

# 🦊 Firefox 用戶是神腳本 — User is GOD Policies.json

> **必須搭配 [tete009 的 Firefox 編譯版](https://tete009.pages.dev/) 使用，可以實現極致效果。**
>
> tete009 是日本開發者維護的 Firefox 優化編譯版，使用更激進的編譯器優化（PGO + LTO），比 Mozilla 官方版快 10-30%。搭配這份 policies.json = 硬體級加速 + 軟體級調校，雙管齊下。

---

## ⚡ 懶人包（100 字）

一份 `policies.json` 檔案，230+ 項設定，解決 Firefox 所有日常體驗痛點。三層加速讓頁面秒開、滾動像黃油、標籤頁變聰明。去掉所有遙測廣告垃圾。丟進 Firefox 目錄就生效，不用一條一條改 `about:config`。給 Windows 用戶 Chrome 級的絲滑體驗，同時保留 Firefox 的優勢。


# 下载 →
https://github.com/tqgx/Firefox-User-is-GOD-Policies.json/blob/main/policies.json

---

## 📦 安裝方法（30 秒）

### Windows
<img width="920" height="583" alt="image" src="https://github.com/user-attachments/assets/968ba900-ee2e-41fa-b71b-b0cad42448bb" />

1. 找到你的 Firefox 安裝目錄（通常是 `C:\Program Files\Mozilla Firefox\`）
2. 在裡面建立一個叫 `distribution` 的資料夾
3. 把 `policies.json` 丟進去
4. 重啟 Firefox

```
C:\Program Files\Mozilla Firefox\
└── distribution\
    └── policies.json    ← 就是這個
```

### 驗證是否生效

地址欄輸入 `about:policies`，看到所有設定就代表成功了。

---

## 🛡️ 強烈建議搭配 Ghostery 擴展

**必須從 Ghostery 的 GitHub 下載安裝**，不要從 Firefox 附加元件商店裝。GitHub 版更新更快、沒有商店審核延遲。

📥 **[Ghostery GitHub 下載頁](https://github.com/ghostery/ghostery-extension/releases)**

> 不要在 GitHub 搜「Ghostery」然後隨便下載不明來源的 repo。請認準 Ghostery 官方的組織帳號。

### 為什麼是 Ghostery？

**「Ghostery 不是賣數據的嗎？」**

那是九年前的事了。

沒錯，Ghostery 早期的母公司 Evidon 確實靠賣廣告數據賺錢，有個叫 GhostRank 的功能默認把你遇到的追蹤器資訊打包賣給廣告商。一個「保護你隱私的工具」，母公司靠「賣你的數據」賺錢。就像你僱了一個保鏢，結果保鏢每天晚上把你家的門鎖型號報告給小偷工會。

2018 年 GDPR 生效那年，Ghostery 寄了一封「慶祝隱私法生效」的推廣郵件，結果把幾百個收件人的 email 放在了 CC 而不是 BCC。一家「保護用戶隱私」的公司，在發送「慶祝隱私保護法」的郵件時，洩露了用戶的個人資訊。就像消防局在「消防安全宣導週」上，不小心把消防局燒了。

**但是——2017 年被德國公司 Cliqz 收購之後，一切都變了：**

- GhostRank 砍了
- 代碼開源了
- 數據收集改成 opt-in
- 用上了 MIT 論文級別的 k-Anonymity 匿名技術

現在靠企業版 GDPR 合規工具賺錢。諷刺嗎？當年因為 GDPR 醜聞被罵到臭頭的工具，現在靠 GDPR 合規賺錢。

### 技術上為什麼快？

- **布隆過濾器**：80,000 條規則，微秒級排除 95%，實際只檢查 ~2,000 條
- **Rust/WASM**：記憶體佔用降低 62%
- **TrackerDB**：不只知道「這是追蹤器」，還知道「這是誰的、那個誰還有什麼其他追蹤器」

Brave 花了 7 年追他們 2019 年的設計。Brave 自己也承認了。

**建議組合：Ghostery + uBlock Origin 一起用 = 最強攔截。**

---

## 🌐 額外項：搭配 Hiddify 實現極致網路體驗

**強烈建議搭配 [Hiddify](https://hiddify.com/) 使用**，走 Cloudflare 的網路，可以獲得：

- **MASQUE 協議**：基於 HTTP/3 (QUIC) 封裝流量，極致的混淆能力和連接穩定性
- **虛擬 IPv6 支援**：即使你的裝置或網路環境不支援原生 IPv6，也能獲得 IPv6 能力
- **全球頂級 BGP 對等互連**：直連大量 Tier 1 上游（Orange、TATA、Zayo、Sparkle、Liberty、AT&T、Cloudflare、Telxius、Cogent、Lumen、NTT、DTAG、Arelion、GTT、Vocus、Telstra 等），完全不計頻寬成本，只追求效能

### 為什麼必須用 SOCKS5？

1. **速度最快**：SOCKS5 工作在更底層，不需要解析 HTTP 標頭，延遲更低
2. **協議無關**：HTTP 代理只能代理 HTTP/HTTPS 流量，SOCKS5 什麼都能走
3. **Cloudflare 的懲罰機制**：CF 會辨識 VPN 流量並降速或封鎖，但 SOCKS5 搭配 MASQUE 協議能有效避開這個問題

### 設定方法
<img width="593" height="778" alt="image" src="https://github.com/user-attachments/assets/b812e6a3-cf03-42fa-82dc-b1ba729d1133" />

1. 開啟 Hiddify，記下它給你的本地端口號（比如 `10808`）
2. Firefox → 設定 → 最下面找到「網路設定」→「設定...」
3. 選擇「手動 Proxy 設定」
4. 在 **SOCKS 主機** 填入 `127.0.0.1`，端口填入你的端口號
5. 選擇 **SOCKS v5**
6. 勾選「使用 SOCKS v5 時代理 DNS」

```
┌─────────────────────────────┐
│  SOCKS 主機: 127.0.0.1      │
│  端口:       10808           │
│  ☑ SOCKS v5                 │
│  ☑ 使用 SOCKS v5 時代理 DNS  │
└─────────────────────────────┘
```

---

## 🔍 這份腳本到底做了什麼？

### 一句話：系統性地消除上百個微小摩擦

不是加了什麼神奇功能，而是把鞋子裡 50 粒沙子倒出來。每個動作少等 0.1 秒 × 一天 500 個動作 = 省 50 秒的煩躁感。用戶說不出哪裡好了，但就是覺得「順」。

### 三層加速疊加

| 層級 | 做了什麼 | 比喻 |
|------|----------|------|
| 🔧 底層：硬體直通 | WebRender 全開、GPU 進程、dmabuf、VAAPI 硬解、圖層加速 | GPU 直接畫頁面，不走 CPU |
| 🌐 中層：網路管線 | 1800 連接、HTTP/2+3、TCP FastOpen、DNS 快取 1 萬條 24 小時、prefetch 全開、2GB 磁碟快取 + 1GB 記憶體快取 | 你還沒點，它已經在下載了 |
| 👁️ 表層：感知速度 | 首次繪製延遲歸零、msdPhysics 彈簧物理滾動、標籤預熱、新標籤預載入 | 眼睛看到的一切都是瞬間出現 |

**三層同時生效 = 數據來得快 + 渲染得快 + 顯示得早 = 秒開一切**

---
Firefox 自動更新關掉，更新請求指向本機（雙保險）。**但擴展更新保持開啟**——uBlock Origin 的過濾規則需要即時更新。如果你用 tete009 版本，更新本來就是手動的，這裡只是保險。

### 2. 遙測封堵（7 層，35+ 條）

Mozilla 的數據收集管道非常複雜，有主開關、有獨立管道、有實驗系統。一條 `DisableTelemetry` 關不乾淨，必須 7 層封堵：

| 層 | 封堵什麼 | 條數 |
|----|----------|------|
| 1 | 主開關 `DisableTelemetry` + Studies + Feedback | 3 |
| 2 | Normandy 遠端實驗系統（2017 年 Mr. Robot 事件的元兇） | 7 |
| 3 | 新標籤頁獨立遙測管道 | 4 |
| 4 | 贊助內容 + Discovery Stream | 6 |
| 5 | 安全 UI 互動記錄（連點鎖頭圖標都記錄） | 4 |
| 6 | Coverage Ping（大部分教程都漏的獨立探測） | 2 |
| 7 | 私有歸因、區域檢測、`<a ping>` 標籤等 | 6 |

**結果：Firefox 不會向 Mozilla 或任何第三方發送任何使用數據。零。**

### 3. 功能精簡

| 關掉的功能 | 為什麼 |
|------------|--------|
| Pocket | 佔 UI 空間、發網路請求、你真的用過嗎？ |
| Firefox Screenshots | Windows 有 Win+Shift+S，根本不需要 |
| Firefox Accounts / Sync | 不需要雲端同步 |
| Translate / Visual Search | 會向伺服器發送頁面內容 |
| AI 全家桶 | Chatbot 側邊欄、連結預覽、智慧分組——全是雲端 AI，關閉並鎖定 |
| 側邊欄新設計 | 佔水平空間、包含 AI 入口 |

### 4. GPU 與渲染加速

```
WebRender 全開 → 整個頁面當作 3D 場景渲染，充分利用 GPU
GPU 進程獨立 → GPU 驅動崩潰不影響瀏覽器
dmabuf → Linux 零拷貝 GPU 記憶體共享
Canvas 加速 → Google Maps、圖表、HTML5 遊戲全部 GPU 渲染
```

**為什麼不開 `webgl.force-enabled`？** 有些低端顯卡強制開 WebGL 會崩潰。WebGL 在支援的硬體上會自動啟用，不需要強制。

### 5. JavaScript 引擎

IonMonkey JIT、Baseline JIT、WebAssembly、增量 GC、並行 GC——全部顯式鎖定為開啟。不是因為默認關了，是防止任何東西意外關掉它們。

### 6. 媒體與影片

- **GPU 硬解影片**：YouTube 4K CPU 使用率 80% → 15%
- **AV1 編解碼器**：YouTube 越來越多用 AV1，更高品質更省頻寬
- **媒體快取 512MB**：影片回拉不用重新下載
- **PiP 完整 4 件套**：開啟 → 跳過教程 → 顯示字幕 → 切標籤自動彈出

### 7. 網路管線

| 優化 | 效果 |
|------|------|
| 全局連接 900 → 1800 | 20 個標籤同時載入不排隊 |
| HTTP/2 + HTTP/3 (QUIC) | 一個連接並行傳輸 + 0-RTT 連接建立 |
| TCP Fast Open | 首次握手就帶數據 |
| DNS 快取 400 → 10,000 條，60 秒 → 24 小時 | 訪問過的網站不再 DNS 查詢 |
| Prefetch + Predictor + Preconnect | 你還沒點，它已經在下載了 |
| 關閉 RCWN（Race Cache With Network） | 有快取就直接用，不浪費流量 |
| 關閉後台標籤限速 | 後台下載不被降速 |

### 8. 緩存策略

| 類型 | 默認 | 調校後 |
|------|------|--------|
| 磁碟快取 | ~256MB | **2GB** |
| 記憶體快取 | ~256MB | **1GB** |
| 圖片解碼 | 16KB/次 | **128KB/次**（8 倍） |
| 圖片表面快取 | ~100MB | **256MB** |
| 媒體快取 | ~12MB | **512MB** |

用記憶體和磁碟換速度。現代電腦最少 8GB RAM、256GB SSD，不需要省。

### 9. 標籤頁行為

這是日常體驗影響最大的部分。每條都對應一個「你每天都碰到但不知道能改」的痛點：

| 痛點 | 解決 |
|------|------|
| 新標籤跑到最右邊 | 緊挨在當前標籤右邊 |
| 點書籤覆蓋當前頁面 | 書籤在新標籤打開 |
| Ctrl+點擊搶走焦點 | 新標籤在後台打開 |
| 關掉最後一個標籤整個瀏覽器消失 | 保留空窗口 |
| 關標籤要精確點 × 按鈕 | 雙擊標籤即關閉 |
| 關掉標籤後跳到右邊隨機標籤 | 跳回打開它的那個標籤 |
| 手滑關掉 15 個標籤沒提示 | 關閉多標籤前警告 |
| 標籤太多分不清 | 鼠標懸停顯示縮略圖 |
| 切換標籤有延遲 | 鼠標懸停就開始預渲染 |
| Ctrl+Tab 從左到右切 | 按最近使用順序（像 Alt+Tab） |
| Firefox View 佔空間 | 去掉 |
| 網站強制開新窗口 | 全部攔截為新標籤 |

### 10. 地址欄

| 功能 | 效果 |
|------|------|
| 搜索後顯示搜索詞 | 不再看到 `google.com/search?q=xxx&oq=xxx` |
| 隱藏 `https://` 但不隱藏 `http://` | 99% 網站是 HTTPS 不用看，但 HTTP 要提醒你 |
| 複製 URL 自動解碼 | 中文不會變成 `%E4%B8%AD%E6%96%87` |
| 點擊全選 | 一點就能直接輸入新網址 |
| 下拉建議 12 條 | 默認 10 條太少 |

### 11. 滾動手感（物理引擎）

Firefox 有個隱藏的 **質量-彈簧-阻尼物理引擎** (`msdPhysics`)：

```
起步彈簧常數 400（有力，一撥就走）
持續彈簧常數 200（順暢，不要太彈）
減速彈簧常數 100（柔和，像黃油滑到盡頭）
```

加上彈性回彈（滾到底會像手機一樣彈一下）、3 倍滾動速度、200ms 短動畫。

**從「機械齒輪」變成「黃油滑軌」。**

### 12. 會話恢復

| 功能 | 效果 |
|------|------|
| `restore_on_demand: true` | **最重要的一條。** 恢復時只載入當前標籤，其他點到才載入。20 個標籤不會同時載入卡死 30 秒 |
| 固定標籤也按需載入 | 否則固定標籤會繞過 restore_on_demand |
| 會話保存間隔 60 秒 | 默認 15 秒太頻繁，減少磁碟 I/O |

### 13. 廣告推廣屏蔽

VPN 推廣、"More from Mozilla"、購物網站 Fakespot 檢查器、歡迎頁（4 層保險封死）、更新後 "What's New" 頁面、UI 教程導覽——全部滅掉。

### 14. UI 密度與視覺

- 緊湊模式（Proton 之後被隱藏了，工具欄高度減少 20%+）
- 啟動即最大化
- Windows 11 風格細滾動條（11px，自動隱藏）
- 強制暗色主題（包括閱讀模式）
- 書籤欄常駐
- 允許 `userChrome.css` 自定義

### 15. 鍵盤與剪貼板

| 痛點 | 解決 |
|------|------|
| Backspace 不能後退（Firefox 86+ 禁用了） | 恢復 |
| 按 Alt 不小心彈出菜單欄 | 禁用 Alt 激活菜單 |
| 銀行網站不讓粘貼密碼 | 禁用網站的剪貼板監聽 |
| 粘貼長文本被截斷 | 不截斷 |
| 隨便按鍵觸發「邊打字邊查找」 | 禁用 |

> ⚠️ `clipboardevents.enabled: false` 會讓 Google Docs、Notion、Figma 的複製粘貼異常。如果你用這些 Web App，在 `about:config` 裡改回 `true`。

### 16. 雜項

- Ctrl+F 高亮所有匹配項（不只高亮當前一個）
- 所有文本框都拼寫檢查（不只大文本框）
- 複製的 URL 自動清除 `?utm_source=...&fbclid=...` 追蹤參數
- 每個網站記住獨立縮放（小字網站 120%，下次自動 120%）
- 新標籤頁顯示 2 行 16 個常用網站
- 安全對話框按鈕沒有 1 秒延遲
- 列印保留背景色/背景圖、PDF 連結可點擊
- 進 `about:config` 不用點「接受風險」
- Linux 用系統原生文件選擇器（不用 Firefox 自己的醜版本）

### 17. 安全相關（不用擔心）

| 設定 | 說明 |
|------|------|
| Safe Browsing 關閉 | Google 的惡意網站黑名單。如果你是普通用戶，改回 `true` 完全沒問題 |
| OCSP 關閉 | 證書吊銷檢查，有時候很慢（200-500ms）。現代瀏覽器轉向本地 CRLite |
| 彈窗攔截關閉 | 如果你不是在做特殊測試，建議改成 `true` |

---

## ⚠️ 已知限制

| 問題 | 說明 | 解決 |
|------|------|------|
| `cookiebanners.service.mode` | Firefox 135 (2025-01) 移除了此功能，設定無效 | 裝 [I still don't care about cookies](https://addons.mozilla.org/firefox/addon/istilldontcareaboutcookies/) |
| `clipboardevents.enabled: false` | Google Docs / Notion 複製粘貼可能異常 | 改回 `true` |
| `DisableBuiltinPDFViewer: true` | PDF 不能在瀏覽器內開 | 改成 `false` |
| `DisableDeveloperTools: true` | F12 沒反應 | 開發者改成 `false` |

---

## 📊 覆蓋率

```
性能/渲染/GPU      ████████████████████ 100%
網路/緩存           ████████████████████ 100%
遙測封堵            ████████████████████ 100%
標籤頁行為          ████████████████████ 100%
地址欄              ████████████████████ 100%
滾動手感            ████████████████████ 100%
畫中畫              ████████████████████ 100%
UI/視覺             ████████████████████ 100%
會話恢復            ████████████████████ 100%
230+ 項設定          ████████████████████ 99%+
```

---

## 授權

MIT License — 隨便用。

---

> 我們做的不是加了什麼神奇功能，而是系統性地消除了上百個微小摩擦。就像把鞋子裡 50 粒沙子倒出來。
> 
> 搭配 [tete009 Firefox](https://tete009.pages.dev/) + [Ghostery (GitHub)](https://github.com/nicosResworwordev) + [Hiddify](https://hiddify.com/) = 極致體驗。
