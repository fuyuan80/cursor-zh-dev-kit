---
name: zh-commit-message
description: >-
  根據 git diff 或變更說明，產生符合 Conventional Commits 規範的中文 commit message。
  使用前請確認已 git add 要提交的檔案。
---
# 中文 Commit Message 產生器

## 使用方式
在 Cursor Agent 輸入：
- 「幫我寫 commit」
- 「產生提交訊息」

## 輸出格式
<type>(<scope>): <中文描述>

<選填：詳細說明>

## 範例輸出
feat(auth): 新增使用者 Google 登入功能
fix(payment): 修正付款回呼未驗證簽名的問題
docs(readme): 更新安裝說明與環境需求
