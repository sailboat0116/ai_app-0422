# 系統架構設計文件 (ARCHITECTURE)

## 1. 系統總覽 (System Overview)
*   **高階架構描述**：
    本專案採標準的 Client-Server (前端與後端分離) 架構。前端扮演使用者介面 (UI) 的角色，負責呈現視覺化的宮廟與抽籤動畫，並與使用者互動；後端則負責核心業務邏輯的處理，包含隨機抽籤演算法、身分識別、資料存取與驗證。前後端透過 RESTful API 以 JSON 格式進行資料交換。
*   **技術棧 (Tech Stack)**：
    *   **前端 (Frontend)**：`HTML5` + `Vanilla CSS` + `Vanilla JS`。
        *   選擇原因：需求指定使用靜態 HTML，適合打造輕量級且無需複雜狀態管理的抽籤與捐獻介面，載入速度快且部署極度簡單。
    *   **後端 (Backend)**：`Python 3` + `FastAPI`。
        *   選擇原因：需求指定，且 FastAPI 具備極高的執行效能，且內建 Swagger UI，可以大幅降低前端查閱 API 文件的溝通成本。
    *   **資料庫 (Database)**：`SQLite`。
        *   選擇原因：需求指定，且做為單一檔案形式的關聯式資料庫，極度適合此種輕度並發、以存檔為主的專案，無需架設獨立的資料庫伺服器，大幅降低維運複雜度。

## 2. 目錄結構 (Directory Structure)
本專案的根目錄將包含前後端的資料夾結構，如下所示：

```text
ai_app/
├── docs/                     # 各類設計文件 (PRD, ARCHITECTURE, MODELS 等)
├── frontend/                 # 靜態前端資源
│   ├── index.html            # 首頁與主介面
│   ├── css/
│   │   └── style.css         # 樣式定義
│   └── js/
│       └── app.js            # API 呼叫與介面互動邏輯
├── backend/                  # FastAPI 後端主程式
│   ├── main.py               # 程式進入點與 APP 初始化
│   ├── database.py           # SQLite 連線設定與 Session 管理
│   ├── models.py             # SQLAlchemy ORM 資料表模型定義
│   ├── schemas.py            # Pydantic 資料驗證與序列化 Schema
│   └── routers/              # API 路由分類
│       ├── draw.py           # 負責抽籤與歷史紀錄之 API
│       └── donation.py       # 負責香油錢捐獻之 API
├── data/
│   └── temple.db             # SQLite 資料庫實體檔案
└── requirements.txt          # 後端 Python 依賴套件清單
```

*   **模組說明**：前端靜態檔案放置於 `frontend/`，由任何靜態伺服器 (或由 FastAPI 順便 serve) 接管；後端程式集中於 `backend/` 並依照 MVC/Router 模式切割確保擴展性。

## 3. 系統流程與介接 (System Flow & Integration)
*   **前後端互動方式**：
    採用標準 `RESTful API`。前端利用原生的 `fetch()` 發送 HTTP Request (GET, POST)，後端接收後執行對應邏輯，並回傳格式化之 JSON 結構。
*   **核心組件圖/流程說明**：
    1.  **抽籤流程**：
        *   使用者在前端點擊「求籤」 ➔ 前端觸發 `POST /api/draw`，夾帶 `{ "username": "...", "question": "..." }` ➔ FastAPI (routers/draw.py) 收到請求。
        *   FastAPI 隨機產生籤號與解析 ➔ 透過 ORM (models.py) 將紀錄寫入 SQLite ➔ 回傳籤詩 JSON 資料 ➔ 前端渲染結果給使用者。
    2.  **紀錄查詢與捐款流程**：
        *   頁面載入時或點擊「歷史」➔ 前端觸發 `GET /api/history?username=xxx` ➔ FastAPI 查詢 SQLite 並回傳該使用者的清單陣列。
        *   送出捐獻表單 ➔ `POST /api/donation` ➔ FastAPI 寫入 SQLite 後回傳成功代碼 ➔ 前端顯示感謝狀。

## 4. 部署與基礎設施 (Deployment & Infrastructure)
*   **環境需求**：
    *   **開發環境 (Development)**：本機安裝 Python 3.10+，使用 `uvicorn backend.main:app --reload` 啟動後端，並透過 Live Server 執行前端 HTML。
    *   **正式環境 (Production)**：一台基礎的 Linux VM 即可，確保防火牆開放 HTTP/HTTPS Protocals 供前端連線。
*   **部署策略**：
    *   可將後端打包為 Docker Image，指令配置使用 Gunicorn 搭配 Uvicorn worker，確保穩定性。
    *   SQLite 資料庫檔案放置於 `/data`，並於 Docker 中使用 Volume 掛載以確保資料不會因重啟而遺失 (Persistence)。
    *   前端可與 FastAPI 整合由同一 Port Serve 出來，或是另放至 Vercel/Cloudflare Pages 以享有免費的 CDN 加速。
