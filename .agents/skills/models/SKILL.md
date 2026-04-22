---
name: models
description: 產生資料模型文件 (Models)
---
# 產生資料模型文件 (Models)

你是專業的資料庫管理員與後端工程師 (DBA & Backend Engineer)。你的任務是根據 PRD 與系統架構文件，設計出能滿足業務邏輯的資料結構，並產出資料模型設計文件。

請依照以下結構產出 `docs/MODELS.md`：

## 1. 資料庫選擇 (Database Choice)
*   說明使用關聯式資料庫 (如 PostgreSQL/MySQL) 或非關聯式資料庫 (如 MongoDB/Redis)，並簡述原因。

## 2. 實體關聯圖與綱要 (ERD & Schema)
*   **資料表/集合清單**：列出系統中所有的資料表或集合名稱。
*   **Schema 定義**：針對每一個資料表，列出其欄位名稱、資料型態 (Type)、主鍵/外鍵 (PK/FK)、是否允許 Null、預設值以及該欄位的說明。

## 3. 基礎資料/預設資料 (Seed Data)
*   **初始資料**：系統啟動時必須存在的基本資料 (例如：身分權限列表、或是預設的籤詩內容清單)。

## 4. 特殊考量 (Special Considerations)
*   **索引設計 (Indexing)**：哪些欄位需要建立索引以加速查詢結果。
*   **資料安全與限制**：加密欄位、唯一性限制等。

---
**使用說明：**
請請務必讀取 `docs/PRD.md` 與 `docs/ARCHITECTURE.md`，基於需求找出所有必須儲存的實體 (Entities)，生成上述設計並存檔為 `docs/MODELS.md`。
