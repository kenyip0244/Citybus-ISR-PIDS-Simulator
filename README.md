# Citybus Island Resort PIDS Simulator (城巴小西灣（藍灣半島）旅客資訊顯示屏模擬器)

這是一個基於 HTML、JavaScript 與 Electron 開發的城巴小西灣（藍灣半島）總站旅客資訊顯示屏（PIDS）模擬器。透過直接串接香港政府「資料一線通（DATA.GOV.HK）」的城巴開放數據 API，提供高還原度、低延遲的實時班次資訊。

---

## ✨ 核心特色

* **全網域自動尋址與探索引擎**：系統內建智能掃描機制，首次啟動時會自動讀取城巴全網域路線，動態抓取並校準任何**開出**或**途經**「藍灣半島」的真實 Stop ID，完全無需手動維護路線清單。
* **智能實時狀態追蹤 (全新 GPS 邏輯)**：
  * **動態 GPS 圖示**：系統會自動分析 API 數據。當班次為**「途經路線」（站序 Seq > 1）**且**「已由總站開出」（具備實時 GPS 追蹤，非預定班次）**時，左上角會自動亮起 `GPS.svg` 追蹤圖示。
  * **即將抵達提示**：倒數至 0 分鐘時自動切換為 `Arr`（即將抵達／開出）狀態。
* **精準過濾機制**：嚴格隱藏目的地為「藍灣半島」方向之抵站班次，確保顯示屏畫面乾淨準確。
* **高還原度 UI**：完美復刻實體 PIDS 的深藍底亮黃字配色、優化的幼體路線編號字型、Cityflyer 專屬向量標誌（`Cityflyer_logo.svg`）以及底部官方安全提示跑馬燈。
* **跨平台桌面應用程式**：支援透過 GitHub Actions 及 Electron Forge，自動編譯為 Windows (`.exe`)、macOS (`.dmg` / `.app`) 及 Linux (`.deb` / `.rpm`) 的獨立應用程式。

---

## 🚏 支援路線 (全自動動態掃描)

系統已完全移除靜態路線名單，改用 **全自動路線探索引擎 (Auto-Discovery Engine)**。
系統會在首次啟動時，自動掃描過百條城巴路線的所有停靠站點，自動納入任何以藍灣半島為起訖點，或**當刻途經**藍灣半島的班次。

* **自動顯示：** 任何開出或途經的班次（涵蓋如 8H, 8P, 8X, 788, 789, 770, 118, 606, A12 等所有相關港島、過海及機場路線）。
* **自動過濾：** 嚴格隱藏以「藍灣半島」為終點站的下客方向班次。

---

## 🚀 安裝與執行

### 方法一：線上網頁版 (Live Demo) ✨ 最快速
無需下載安裝任何軟體，點擊下方連結即可直接在電腦、平板或手機瀏覽器中觀看實時運作的顯示屏：
👉 **[前往 Citybus Island Resort PIDS 網頁版](https://kenyip0244.github.io/Citybus-Island-Resort-PIDS-Simulator/)** *(註：請確保網址與您的 GitHub Pages 設定一致)*

### 方法二：下載已編譯的桌面應用程式
請前往本儲存庫的 **[Releases](https://github.com/kenyip0244/Citybus-Island-Resort-PIDS-Simulator/releases)** 頁面，下載適用於您作業系統的最新發布版本（支援 Windows、macOS、Linux）。

### 方法三：本地端開發與編譯
請確保您的電腦已安裝 [Node.js](https://nodejs.org/)。

```bash
# 1. 複製專案原始碼
git clone [https://github.com/kenyip0244/Citybus-Island-Resort-PIDS-Simulator.git](https://github.com/kenyip0244/Citybus-Island-Resort-PIDS-Simulator.git)
cd Citybus-Island-Resort-PIDS-Simulator

# 2. 安裝依賴套件
npm install

# 3. 本地端即時測試運行（以 Electron 視窗開啟）
npm start

# 4. 手動打包桌面應用程式
npm run make

```

*(註：您也可以單純下載專案原始碼後，直接用瀏覽器開啟 `index.html` 執行純網頁版)*

---

## 🖱️ 隱藏操作指南

* **切換全螢幕**：雙擊畫面中央的班次顯示區域即可切換全螢幕模式。
* **強制重置站位與路線快取**：雙擊頂部深藍色標題列（「路線 Route」區域），即可強制清除自動尋址引擎的快取並**重新掃描全城巴路線**（適用於官方站點 ID 或路線發生大變動時）。

---

## 📂 專案檔案結構

```text
Citybus-Island-Resort-PIDS-Simulator/
├── .github/workflows/
│   └── build.yml          # GitHub Actions 跨平台 CI/CD 自動編譯腳本
├── .gitignore             # Git 忽略清單 (排除 node_modules 等編譯檔案)
├── Cityflyer_logo.svg     # 城巴機場快線標誌向量圖
├── GPS.svg                # 實時 GPS 追蹤向量圖示
├── index.html             # PIDS 主介面與即時資料處理核心邏輯
├── main.js                # Electron 主行程入口檔案
├── package.json           # Node.js 專案設定與應用程式資訊
└── README.md              # 專案說明文件

```

---

## ⚠️ 聲明

* 本專案使用的實時班次資料來自香港政府 [資料一線通 (DATA.GOV.HK)](https://data.gov.hk/) 及城巴開放數據 API。
* 本顯示屏為模擬器性質，僅供學術交流與程式開發參考，實際到站時間請以城巴官方應用程式或現場實際情況為準。
