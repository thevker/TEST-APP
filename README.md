# ⚽ 智能量化足球預測系統 ver 1.0

工具: https://thevker.github.io/FootBall-AI/

> 一套結合**機率模型、市場定價（賠率）與極致風控**的自動化足球分析工具。用數學邏輯取代人為情緒，適用於足球賽前數據分析與策略驗證。

![Version](https://img.shields.io/badge/version-1.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![HTML](https://img.shields.io/badge/HTML-5-orange)
![CSS](https://img.shields.io/badge/CSS-3-blue)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow)

---

## 📸 預覽

> 三合一系統：**條款同意頁 + 智能預測計算器 + 猜賽果挑戰**

- 🌙 直接深淺色主題切換
- 🌐 繁中 /使用 簡中 / 英文
- 📊 實時讀取 Google Sheets 歷史數據
- 🎮 遊戲化猜賽果 + Tier 等級系統
- 📱 響應式設計（手機 / 平板 / 電腦）

---

## ✨ 功能特色

### 🧮 智能預測計算器
- 輸入 **6 個數據**（主/和/客勝率 + 主/和/客賠）
- 經 **6 層公式判斷** 輸出建議：**買主 / 買和 / 買客 / 不出手**
- 自動計算 **期望值 EV-1**
- 顯示該層策略邏輯說明

### 🎮 猜賽果挑戰
- 隨機生成合理賠率（模擬真實市場）
- 每注固定 **$100**
- **⏭️ 跳過功能**：預設 2 次，每玩 10 場 +1 次
- **Tier 等級系統**（10 場後顯示）：
  - 🟣 **EX**（≥70%）：紫色幻彩漸變
  - 🟡 **S / S+ / S-**（62.5-70%）：金色發光
  - 🔵 **A 系列**：藍色
  - 🟡 **C 系列**：黃色
  - 🔴 **D 系列**：紅色
  - ⚪ **E 系列**：灰色
- 賽事描述：💥 史詩級大爆冷 / 💰 高賠和局 / ✅ 正常賽果 …

### 📊 歷史數據統計
- 實時讀取 Google Sheets 數據
- 每 **15 秒** 自動同步
- 顯示：總盈虧 / 命中數 / 總成本 / 出手數 / ROI / 命中率

### 🎨 UI/UX
- 🌙 / ☀️ **深淺色主題**（localStorage 記憶）
- 🌐 **三語言**：繁中 / 簡中 / 英文
- 滾動時頂部按鈕自動淡出
- 玻璃擬態（Glassmorphism）設計

---

## 🚀 快速開始

### 方法 1：單檔案

下載 `index.html`，用瀏覽器打開即可。

```bash
git clone https://github.com/你的用戶名/quant-football-predictor.git
cd quant-football-predictor
# 用瀏覽器打開 index.html
```

### 方法 2：本地伺服器

```bash
# Python
python -m http.server 8000

# Node.js
npx serve
```

然後瀏覽 `http://localhost:8000`

### 方法 3：部署到 GitHub Pages

1. 將 `index.html` 推到 GitHub repo
2. 進入 **Settings → Pages**
3. Source 選 `main` branch
4. 網址：`https://你的用戶名.github.io/quant-football-predictor/`

---

## 📐 核心公式（6 層判斷）

| 層 | 條件 | 結果 |
|---|---|---|
| 1 | `\|A−C\| ≤ 6` | **D**（買和）|
| 2 | `A≥42` 且 `1.55≤D<2.05` 且 `D≠F` | **H**（買主）|
| 3 | `A≥40` 且 `2.10<D≤2.45` 且 `D≠F` | **D**（買和）|
| 4 | `C>A` 且 `F>D` 且 `F<5.50` | **H**（買主）|
| 5 | `C>A` 且 `1.85≤F≤2.15` | **A**（買客）|
| 6 | 兜底賠率博弈 | 見下 |

**兜底層：**
```
D>F：A≥30 且 D≥6.00 → D；否則 H
F>D：F≥7.50 → skip；否則 A
D=F：按勝率比較
```

**欄位定義：**
| 欄 | 內容 |
|---|---|
| A | 主勝率 |
| B | 和勝率 |
| C | 客勝率 |
| D | 主賠（×100）|
| E | 和賠（×100）|
| F | 客賠（×100）|

---

## 📁 檔案結構

```
quant-football-predictor/
├── index.html          # 完整單檔案應用
├── README.md           # 本文件
├── LICENSE             # MIT License
└── screenshots/
    ├── dark-mode.png
    ├── light-mode.png
    └── tier-example.png
```

---

## 🛠️ 技術棧

| 技術 | 用途 |
|---|---|
| **HTML5** | 頁面結構 |
| **CSS3** | 樣式、動畫、主題變數 |
| **Vanilla JavaScript** | 邏輯、狀態管理 |
| **Google Sheets API** | 實時讀取歷史數據 |
| **localStorage** | 主題偏好記憶 |
| **CSS Keyframes** | Tier 動畫（脈衝、幻彩、彈跳）|

**零依賴** — 唔需要 npm、webpack、任何框架。

---

## 🔧 自訂

### 修改 Google Sheets 數據源

搵到 `index.html` 內：

```javascript
const SHEET_ID = '你的_GOOGLE_SHEET_ID';
const SHEET_NAME = '工作表1';
```

改成你嘅 Sheet ID 同工作表名稱。

### 修改 Tier 分佈

搵到 `function getTier(rate)`：

```javascript
function getTier(rate) {
  if (rate >= 70)   return { tier: 'EX', descKey: 'tierEX' };
  if (rate >= 67.5) return { tier: 'S+', descKey: 'tierS' };
  // ...
}
```

### 修改跳過次數

搵到 `function getMaxSkips()`：

```javascript
function getMaxSkips() {
  return 2 + Math.floor(gameState.played / 10);
  //      ↑ 預設次數    ↑ 每 N 場 +1 次
}
```

---

## 📋 使用流程

```
1. 開啟網頁
   ↓
2. 閱讀條款（滾到底）→ 按「我已閱讀並同意」
   ↓
3. 進入主頁面
   ├─ 頂部：歷史數據統計（自動同步）
   ├─ 中間：智能預測計算器
   └─ 底部：猜賽果挑戰
   ↓
4. 輸入 6 個數據 → 按「計算結果」→ 得出建議
   ↓
5. 玩猜賽果累積 Tier 等級
```

---

## ⚠️ 風險聲明

| 提醒 | 說明 |
|---|---|
| ⚠️ **歷史不等於未來** | 回測表現不代表未來必贏 |
| ⚠️ **樣本量關鍵** | 少於 30 場數字不可信 |
| ⚠️ **勿過度擬合** | 頻繁調參數會失效 |
| ⚠️ **固定注碼** | 唔好因短期黑單加注 |
| ⚠️ **娛樂為主** | 數據分析嘅樂趣，非賺錢捷徑 |

> 本系統及所有相關數據、圖表與分析結果，**僅供學術研究、數據分析及個人興趣之用**，不構成任何形式的投資建議或博彩邀約。
>
> 博彩涉及風險，請嚴格控制注碼，切勿沉迷賭博。

---

## 🤝 貢獻

歡迎提交 Issue 或 Pull Request：

1. Fork 呢個 repo
2. 建立 feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit 你嘅改動 (`git commit -m 'Add some AmazingFeature'`)
4. Push 到 branch (`git push origin feature/AmazingFeature`)
5. 開啟 Pull Request

---

## 📄 License

本項目基於 **MIT License** 開源 — 詳見 [LICENSE](LICENSE) 檔案。

---

## 👤 作者

**thevker**
- GitHub: [@thevker](https://github.com/thevker)
- Email: your.email@example.com

---

## ⭐ Star History

如果呢個項目對你有幫助，請俾個 ⭐ Star 支持一下！

---

## 📌 免責聲明

```
本軟件按「現狀」提供，不附帶任何明示或暗示的保證。
作者不對使用本軟件所產生嘅任何直接或間接損失負責。
使用前請仔細閱讀系統內嘅「使用守則與風險聲明」。
```

---

<div align="center">

**⚽ 理性參與，享受數據分析嘅樂趣 ⚽**

Made with ❤️ by [thevker]

</div>
