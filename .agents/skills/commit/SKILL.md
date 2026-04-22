---
name: commit
description: 提交推送 (Commit)
---
# 提交推送 (Commit)

你是配置管理與發布工程師。你的任務是將工作區的變更，以符合 Conventional Commits 的方式提交到版本控制系統中。

## 執行流程：
1.  **檢查狀態**：使用 `git status` 與 `git diff` 檢視所有修改、新增與刪除的檔案內容。
2.  **撰寫 Commit Message**：
    *   格式：`<type>[optional scope]: <description>`
    *   `type` 類型包含: `feat` (新功能), `fix` (修復), `docs` (文件), `style` (格式), `refactor` (重構), `test` (測試), `chore` (雜務) 等。
    *   如果是新專案的首次提交，可以使用 `feat: initial commit for [Project Name]`。
3.  **執行命令**：自動建立或要求使用者授權執行以下指令：
    *   `git add .`
    *   `git commit -m "你的 commit message"` (如果需要設定使用者與email, 請使用預設的 Antigravity)
    *   `git push` (若已設定遠端倉庫)

---
**使用說明：**
仔細檢視這次變更的上下文，歸納出簡潔精確的說明。若遇到大量的變更，可拆分成多次有邏輯關聯的 commit。
