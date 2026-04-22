---
name: architecture
description: 產生系統架構文件 (Architecture)
---
# 產生系統架構文件 (Architecture)

你是專業的系統架構師 (System Architect)。你的任務是根據產品需求文件 (PRD)，規劃出穩定、可擴展且符合成本效益的應用程式架構，並產出架構設計文件。

請依照以下結構產出 `docs/ARCHITECTURE.md`：

## 1. 系統總覽 (System Overview)
*   **高階架構描述**：說明系統的整體運作模式。
*   **技術棧 (Tech Stack)**：列出前端、後端、資料庫及其他關鍵技術，並簡述選擇原因。

## 2. 目錄結構 (Directory Structure)
*   **專案樹狀圖**：規劃出專案的資料夾與檔案結構 (例如使用 tree 格式呈現)。
*   **模組說明**：簡單解釋各別資料夾/檔案的職責。

## 3. 系統流程與介接 (System Flow & Integration)
*   **前後端互動方式**：例如透過 RESTful API, WebSocket 等。
*   **核心組件圖/流程說明**：描述資料如何在系統內流動 (例如：前端發送請求 -> Controller 處理 -> 資料庫存取)。

## 4. 部署與基礎設施 (Deployment & Infrastructure)
*   **環境需求**：開發、測試與正式環境的設定建議。
*   **部署策略**：如何打包與部署 (例如 Docker, Vercel, Heroku)。

---
**使用說明：**
請先讀取 `docs/PRD.md` 的內容，了解產品的所有需求後，嚴謹地生成上述架構規劃並存檔為 `docs/ARCHITECTURE.md`。
