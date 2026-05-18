---
name: zh-commit-message
description: >-
  讀取 git diff 並產生 Conventional Commits 格式的中文提交訊息。
  在用戶說「幫我寫 commit」「產生提交訊息」或要總結 staged 變更時使用。
---

# 中文提交訊息（zh-commit-message）

## 觸發時機

- 用戶說：「幫我寫 commit」「產生提交訊息」「寫一下 commit message」
- 用戶已執行或即將執行 `git add`，需要符合團隊規範的訊息

## 步驟

1. **讀取變更**：執行或請用戶提供 `git diff --staged`（無 staged 時用 `git diff` 並說明範圍）。
2. **分析變更類型**：判斷主要意圖對應的 `type`（`feat` / `fix` / `docs` / `refactor` / `perf` / `test` / `chore` / `ci` 等）。
3. **撰寫訊息**：`type` 與可選 `scope` 用**英文**；冒號後描述用**中文**（與用戶繁簡語系一致）。
4. **檢查**：單一主題、祈使語氣、必要時加正文說明破壞性變更。

## 輸出格式

```text
<type>(<scope>): <中文描述>

<可選正文>
```

## 輸出範例

**僅標題：**

```text
feat: 新增使用者登入功能
```

```text
fix(payment): 修正金流回調錯誤
```

**含正文：**

```text
feat(auth): 新增 OAuth 第三方登入

支援 Google 與 GitHub；未設定 CLIENT_ID 時啟動拋錯。
```

```text
refactor: 抽離訂單狀態機至獨立模組

不變更對外 API；單元測試已更新。
```

## 注意

- 用戶未要求時，**只輸出文案**，不執行 `git commit`。
- 變更含多個無關主題時，建議拆成多次提交並分別給出 message。
