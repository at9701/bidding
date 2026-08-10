# ⚔️ 寶物競標所 — 天堂公會競標 & 交易系統

公會專用的寶物競標與交易佈告欄，部署在 GitHub Pages + Google Sheets 後端，零成本、手機可用。

## 功能

- **⚔️ 競標系統**：發起競標、設定底價/每口加價/到期時間、即時出價、倒數計時、結標公告
- **🏪 交易所**：想收 / 想賣佈告欄，可自行下架
- **🔔 瀏覽器通知**：被加價時自動跳通知
- **📱 手機友善**：RWD 設計，加到手機桌面即可使用
- **👥 多人共用**：所有人連同一個 Google Sheet，資料即時同步（每 5 秒）

## 架構

```
GitHub Pages（前端靜態網頁）
        ↕ fetch API
Google Sheet + Apps Script（後端資料庫）
```

---

## 部署教學

### 第一步：建立 Google Sheet 後端

1. 開一個新的 [Google Sheet](https://sheets.new)
2. 上方選單：**擴充功能 → Apps Script**
3. 把預設的程式碼全部刪掉，貼上 `apps-script-code.gs` 的內容
4. 按上方 **▶ 執行**，函式選 `setup`，執行一次
   - 第一次會要求授權，按「審查權限」→ 選你的帳號 → 「進階」→「前往 XXX（不安全）」→ 允許
   - 執行完回到 Sheet 會看到多了 `Auctions`、`Bids`、`Market` 三個分頁
5. 回到 Apps Script，點 **部署 → 新增部署**
   - 類型：**網頁應用程式**
   - 執行身分：**自己**
   - 誰可以存取：**所有人**
   - 按「部署」
6. 複製產生的 **網頁應用程式網址**（格式：`https://script.google.com/macros/s/.../exec`）

### 第二步：部署前端到 GitHub Pages

1. Fork 或 clone 這個 repo
2. 到 repo 的 **Settings → Pages**
   - Source 選 **Deploy from a branch**
   - Branch 選 `main`，資料夾選 `/ (root)`
   - 按 Save
3. 等幾分鐘後就能開 `https://<你的帳號>.github.io/<repo名稱>/`

### 第三步：開始使用

1. 開網頁，貼上第一步複製的 Apps Script 網址
2. 輸入角色名稱
3. 把網址分享給公會成員，大家貼同一個 Apps Script 網址就能一起用了

---

## Apps Script 更新部署

如果修改了 `apps-script-code.gs`：
1. 回到 Apps Script 貼上新程式碼
2. **部署 → 管理部署 → 編輯（鉛筆圖示）→ 版本選「新版本」→ 部署**
3. 網址不變，前端不用改

## 注意事項

- Google Apps Script 回應約 1-3 秒，屬正常現象
- 前端每 5 秒自動同步一次資料
- 同時大量出價有 Lock 機制防衝突，但極端情況仍可能需手動確認
- 資料都存在你的 Google Sheet，可直接在試算表裡查看或手動修正

## License

MIT
