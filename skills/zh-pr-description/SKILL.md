---
name: zh-pr-description
description: >-
  撰寫結構化中文 PR 說明（變更摘要、主要改動、測試方式、注意事項）。
  在用戶說「幫我寫 PR 說明」或要建立/更新 Pull Request 時使用。
---

# 中文 PR 說明（zh-pr-description）

## 觸發時機

- 用戶說：「幫我寫 PR 說明」「產生 PR 描述」「填一下 pull request」
- 用戶要建立 PR，需總結當前 branch 相對於 base branch 的改動

## 前置步驟

1. 確認 base branch（通常 `main` 或 `master`）。
2. 閱讀 `git log` / `git diff <base>...HEAD`，理解改動目的與影響範圍。
3. 語系與用戶一致（預設繁體；用戶用簡體則用簡體）。

## 輸出結構（必須包含以下四節）

```markdown
## 變更摘要

<1–3 句話：解決什麼問題、對用戶/系統的影響>

## 主要改動

- <改動點 1>
- <改動點 2>
- <可選：破壞性變更、遷移步驟>

## 測試方式

- [ ] <如何驗證核心路徑>
- [ ] <邊界或回歸項>
- [ ] <所需環境、帳號、設定>

## 注意事項

- <風險、效能、安全、資料遷移；無則寫「無特殊注意事項」>
- <reviewer 需關注的檔案或決策點>
```

> 簡體用戶可將「測試方式」標題寫為「测试方式」，其餘結構相同。

## 輸出範例

```markdown
## 變更摘要

為結帳流程新增 Stripe webhook 處理，確保付款成功後訂單狀態即時更新。

## 主要改動

- 新增 `POST /webhooks/stripe` 與簽章驗證
- 訂單服務加入 `markPaid` 冪等更新
- 補上 webhook 單元測試與 fixture

## 測試方式

- [ ] 本地用 Stripe CLI 轉發 `checkout.session.completed` 事件
- [ ] 確認重複事件不會重複寫入訂單狀態
- [ ] 執行 `npm test -- webhooks`

## 注意事項

- 部署前需在 Stripe Dashboard 設定 `STRIPE_WEBHOOK_SECRET`
- 無資料庫 schema 變更
```

## 注意

- 用戶未要求時，不執行 `git push` 或 `gh pr create`。
- 若 repo 已有 PR 模板，在其結構上填入中文內容，並保留必要欄位。
