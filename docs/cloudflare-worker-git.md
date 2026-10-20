# 家庭任務 API 的 Git 自動部署

- 來源為 `DylanChiang-Dev/DC-family-task-manager` 的 `main`。
- 發布目標僅為既有 Worker `ftm-api`，使用 `production` 環境。
- Node.js 22、pnpm 9.15.4，從 workspace 根目錄使用既有 lockfile。
- 建置命令：`pnpm install --frozen-lockfile && pnpm run build:cloudflare`。
- 發布命令：`pnpm run deploy:cloudflare`。
- 建置會先檢查 API 型別並執行部署 dry run。
- 自動部署保留既有變數、JWT secrets、D1、KV、排程及網域。
- 此流程不執行資料庫 migration、初始化、seed 或資料匯入。
- 若程式變更另需 schema 調整，必須先取得授權處理資料庫，才可發布。
- Web 前端仍沿用原有 Pages 流程，不由此 Worker 的觸發器發布。
- 憑證由 Cloudflare 建置權杖提供，發布訊息記錄 GitHub 提交。

## 發布驗證

API 發布前另執行共用資料契約的型別檢查與 34 項單元測試。
已驗證正式 API 的健康檢查正常，未登入的會員 API 仍回 401；
Web 正式建置的 API 地址也已核對。只改本文件不觸發 API 發布。
