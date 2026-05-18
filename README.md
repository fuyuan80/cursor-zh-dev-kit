# 中文開發者套件（zh-dev-kit）

> **简体说明**：面向繁体与简体中文开发者的 Cursor 插件，包含沟通规则、Git 提交、PR 说明与代码审查技能。

面向繁體與簡體中文開發者的 [Cursor Plugin](https://cursor.com/docs/plugins)，打包 Rules 與 Skills，讓 Agent 預設以**繁體中文**溝通（偵測到簡體輸入時自動切換），並遵循 Conventional Commits、PR 與 Code Review 工作流。

## 目錄結構

```text
cursor-zh-dev-kit/
├── .cursor-plugin/
│   └── plugin.json
├── rules/
│   ├── zh-communication.mdc
│   ├── git-commit-zh.mdc
│   └── code-comments-zh.mdc
├── skills/
│   ├── zh-commit-message/
│   ├── zh-pr-description/
│   └── zh-code-review/
├── mcp.json
└── README.md
```

## 安裝方式

### 方式一：Marketplace（推薦）

插件發布至 [Cursor Marketplace](https://cursor.com/marketplace) 後，在 Cursor 對話框輸入：

```text
/add-plugin zh-dev-kit
```

亦可開啟 Marketplace 面板搜尋「中文開發者套件」或 `zh-dev-kit` 安裝。

> `/add-plugin` 僅適用於已上架的 Marketplace 插件。本機開發或未上架時，請用下方本機安裝。

### 方式二：本機插件目錄

將本倉庫放到 Cursor 可載入的插件路徑，或於開發時以 plugin 根目錄作為工作區，依 [Plugins 文件](https://cursor.com/docs/plugins) 載入。

### 方式三：複製到專案

| 來源 | 複製至專案 |
|------|------------|
| `rules/` | `.cursor/rules/` |
| `skills/` | `.cursor/skills/` |
| `mcp.json` | 合併至專案或使用者 MCP 設定 |

## 內容一覽

| 類型 | 名稱 | 說明 |
|------|------|------|
| Rule | `zh-communication` | 預設繁體；用戶簡體時改簡體；術語保留英文 |
| Rule | `git-commit-zh` | type 英文 + 中文描述（Conventional Commits） |
| Rule | `code-comments-zh` | 複雜邏輯、公開 API、TODO/FIXME 中文註解 |
| Skill | `zh-commit-message` | 依 diff 產生中文 commit message |
| Skill | `zh-pr-description` | 產生結構化 PR 說明 |
| Skill | `zh-code-review` | 結構化程式碼審查（✅ / ⚠️ / ❌） |

## Skill 使用範例

在 Cursor Agent 對話中直接下指令即可觸發對應 Skill（Agent 會依描述自動選用）。

### zh-commit-message

```text
幫我寫 commit
```

```text
產生提交訊息，我剛 git add 了登入相關的檔案
```

預期輸出範例：

```text
feat(auth): 新增使用者登入功能
```

### zh-pr-description

```text
幫我寫 PR 說明
```

```text
幫我寫 PR 說明，這個 branch 是 fix/payment-callback，base 是 main
```

預期輸出包含：`## 變更摘要`、`## 主要改動`、`## 測試方式`、`## 注意事項`。

### zh-code-review

```text
幫我 review 這段程式碼
```

```text
幫我 review 這段程式碼：src/webhook.ts
```

預期輸出包含：`## ✅ 優點`、`## ⚠️ 建議改善`、`## ❌ 需要修正`。

## MCP 設定

根目錄 `mcp.json` 預設為空，可自行加入 MCP 伺服器，例如：

```json
{
  "mcpServers": {
    "example": {
      "command": "npx",
      "args": ["-y", "some-mcp-package"],
      "env": {
        "API_KEY": "${YOUR_API_KEY}"
      }
    }
  }
}
```

修改後重新載入 MCP。詳見 [MCP 文件](https://cursor.com/docs/mcp)。

## 自訂與發布

1. 新增 Rule：於 `rules/` 建立 `.mdc` 並設定 frontmatter。
2. 新增 Skill：於 `skills/<name>/SKILL.md` 定義 `name` 與 `description`。
3. 更新 `.cursor-plugin/plugin.json` 的 `version` 與說明。
4. 推送到公開 Git 後，至 [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish) 提交審核。

## 授權

MIT
