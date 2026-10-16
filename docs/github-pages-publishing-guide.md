# GitHub Pages 發佈操作指南

這份指南記錄「2026 綠領建築師培訓課程」學習網站與心得簡報的發佈方式，方便日後自行更新、重新發佈與排除問題。

## 發佈成果

- 學習網站：https://sn907635.github.io/green-building-learning-2026/
- 心得簡報：https://sn907635.github.io/green-building-learning-2026/slides.html
- GitHub 儲存庫：https://github.com/sn907635/green-building-learning-2026

這個網站是公開網站，任何人取得網址都可以瀏覽。請只放適合公開的內容。

## 為什麼使用 GitHub Pages

網站目前由 HTML、CSS 與 JavaScript 組成，不需要伺服器、資料庫或編譯步驟。GitHub Pages 可以直接託管這類靜態網站；網站原始檔與版本紀錄也能放在同一個 GitHub 儲存庫，方便日後人工修改和追蹤變更。

## 為什麼使用 GitHub Actions 發佈

儲存庫已設定一個 GitHub Actions 工作流程。每次將變更提交到 `main` 分支，工作流程就會把網站檔案送到 GitHub Pages。這樣可以重複使用相同流程，並在 Actions 頁面查看每次發佈是否成功。

目前網站沒有套件安裝、編譯或打包步驟。工作流程會直接把儲存庫根目錄的檔案上傳，再部署到 Pages。

## 檔案各自的用途

| 檔案或資料夾 | 用途 |
| --- | --- |
| `index.html` | 學習網站首頁，包含主題學習內容與自我檢核 |
| `slides.html` | 學習心得網頁簡報 |
| `.github/workflows/deploy-pages.yml` | 自動發佈流程設定 |
| `docs/github-pages-publishing-guide.md` | 本操作指南 |

首頁檔案必須命名為 `index.html`，並放在儲存庫根目錄，GitHub Pages 才能以網站根網址開啟首頁。簡報放在根目錄，所以網址最後加上 `/slides.html`。

## 第一次設定或重新確認 Pages

1. 開啟儲存庫：https://github.com/sn907635/green-building-learning-2026
2. 選擇 **Settings**。
3. 左側選擇 **Pages**。
4. 在 **Build and deployment** 區段，將 **Source** 設為 **GitHub Actions**。
5. 儲存設定（若畫面有顯示儲存按鈕）。

選擇 GitHub Actions，是因為此儲存庫已用 `.github/workflows/deploy-pages.yml` 定義部署步驟。若 Pages 尚未啟用或來源未設為 Actions，工作流程在設定 Pages 的步驟可能會因找不到 Pages 網站而失敗。這次初次部署也曾遇到此狀況；改好來源後重新執行便成功。

## 日後更新網站

### 用 GitHub 網頁編輯

1. 到儲存庫首頁，開啟要修改的檔案，例如 `index.html` 或 `slides.html`。
2. 點選鉛筆圖示進入編輯。
3. 完成修改後，按 **Commit changes**。
4. 確認變更提交到 `main` 分支。
5. 儲存庫收到提交後，Actions 會自動啟動發佈。

如果需要新增網頁，把檔案放在儲存庫根目錄或適當子資料夾，並使用相對路徑連結。例如根目錄新增 `resources.html`，網址會是 `https://sn907635.github.io/green-building-learning-2026/resources.html`。

### 用本機 Git 編輯

如果已經把儲存庫下載到電腦，可在本機修改檔案，再提交並推送到 `main`。推送後同樣會自動發佈。日常操作概念如下：

```text
修改網站檔案
→ 提交變更到 main
→ 推送到 GitHub
→ GitHub Actions 執行部署
→ 到公開網址確認結果
```

若使用 GitHub Desktop，可在程式中選取變更、填寫提交摘要並按 **Commit to main**，再按 **Push origin**。

## 查看發佈是否完成

1. 在儲存庫上方選擇 **Actions**。
2. 開啟最新的 **Deploy learning site to GitHub Pages** 執行紀錄。
3. 確認工作流程及 **Deploy** 工作顯示綠色成功狀態。
4. 成功後開啟學習網站和心得簡報網址檢查內容。
5. 如果剛完成部署但仍看到舊內容，等候一兩分鐘後重新整理頁面；必要時可使用瀏覽器強制重新載入。

工作流程也支援手動啟動：在 **Actions** 選擇 **Deploy learning site to GitHub Pages**，再按 **Run workflow**，選擇 `main` 後執行。通常只有在需要重新部署或驗證設定時才需要這麼做。

## 常見問題

### Actions 顯示 Configure Pages 失敗，訊息提到找不到 Pages 網站

回到 **Settings → Pages**，確認 **Source** 已設為 **GitHub Actions**。設定完成後，從 Actions 的失敗執行紀錄選擇 **Re-run jobs**，或手動啟動工作流程。

### 工作流程成功，但網站沒有更新

先等一兩分鐘再重新載入。接著確認修改已提交到 `main`，並檢查 Pages 網址與檔名是否正確。首頁網址使用根目錄的 `index.html`；心得簡報使用 `/slides.html`。

### 網址顯示 404

確認儲存庫仍存在、Pages 已啟用，且檔案已提交至 `main`。確認檔名大小寫與網址一致；例如 `slides.html` 與 `Slides.html` 是不同名稱。

### Actions 執行失敗

進入該次執行紀錄，打開紅色失敗的步驟查看錯誤訊息。修正設定或檔案問題後，再重新執行。不要只是不斷重跑同一個仍未修正的失敗工作。

## 公開內容與安全

此儲存庫與網站設定為公開。請勿將密碼、存取權杖、私人聯絡資料或不適合公開的個人資訊提交至儲存庫。GitHub Pages 適合公開展示靜態內容；若日後要加入需要登入、儲存個人資料或伺服器處理的功能，應另外設計合適的服務。

## 官方說明

- [設定 GitHub Pages 的發佈來源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [建立 GitHub Pages 網站](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
