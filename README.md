<p align="center">
  <img src="assets/logo.png" alt="酒Ann" width="140">
</p>

<h1 align="center">品牌內容引擎 Brand Content Engine</h1>

<p align="center">
  by <b>酒Ann</b> — AI Application &amp; Developer / Online Educator &amp; Customized Creator
</p>

一個**單檔 HTML** 的品牌內容生產工具。下載一個檔案、用瀏覽器打開，就能跑完整條流程：爬自己的網站 → 解析品牌定位 → 分析競品 → 產出內容。

沒有後端、沒有安裝、沒有帳號、沒有依賴套件。

## 快速開始

1. 下載 `brand-content-engine pro.html`
2. 用瀏覽器打開（雙擊即可）
3. 在「00 模型與金鑰」選一家供應商、貼上 API 金鑰
4. 按「測試連線」確認通了，然後往下一步一步跑

想零成本試玩的話，選 **Groq**（有免費額度、速度很快）或 **Ollama**（跑在自己電腦上，完全免費）。

## 隱私

金鑰只存在你自己的瀏覽器 `localStorage`，並且**直接送到模型供應商，不經過任何中介伺服器**——因為這個專案根本沒有伺服器。

不想留存的話，不要勾「在這台電腦記住金鑰」，金鑰就只活在當前分頁。

## 支援的語言模型

目前支援 9 家供應商：

| 供應商 | 建議模型 | 金鑰申請 | 適合誰 |
|---|---|---|---|
| **Anthropic Claude** | `claude-sonnet-5`、`claude-opus-5`、`claude-haiku-4-5-20251001` | console.anthropic.com | 課堂預設 |
| **OpenAI** | `gpt-4o-mini`、`gpt-4o`、`gpt-4.1-mini` | platform.openai.com | 最多人已有帳號 |
| **Google Gemini** | `gemini-2.0-flash`、`gemini-2.5-flash`、`gemini-2.5-pro` | aistudio.google.com | 有免費額度 |
| **DeepSeek** | `deepseek-chat`、`deepseek-reasoner` | platform.deepseek.com | 單價便宜 |
| **Kimi（Moonshot）** | `moonshot-v1-32k`、`moonshot-v1-128k`、`kimi-latest` | platform.moonshot.cn | 長文處理 |
| **智譜 GLM** | `glm-4-plus`、`glm-4-flash`、`glm-4-air` | open.bigmodel.cn | 中國方案 |
| **MiniMax** | `MiniMax-Text-01`、`abab6.5s-chat` | platform.minimax.chat | 中國方案 |
| **Groq** | `llama-3.3-70b-versatile`、`llama-3.1-8b-instant`、`qwen-2.5-32b` | console.groq.com | 速度極快、有免費額度 |
| **Ollama** | `llama3.2`、`qwen2.5:7b`、`gemma3` | 不需要金鑰 | 零 API 費用，跑在本機 |

### 關於 CORS

這是純前端工具，瀏覽器直連 API 需要供應商在回應中放行跨來源請求。**Anthropic、OpenAI、Gemini、Groq 已知可用**；中國幾家（DeepSeek、Kimi、GLM、MiniMax）視其 CORS 政策而定，若被擋下工具會直接告訴你原因。

### 使用 Ollama

先讓本機服務允許瀏覽器連線，否則會被 CORS 擋：

```bash
OLLAMA_ORIGINS=* ollama serve
```

然後拉一個模型：

```bash
ollama pull llama3.2
```

## 新增供應商

供應商都集中在 `PROVIDERS` 這張表裡。大部分服務都相容 OpenAI 的 `/chat/completions` 格式，這種只要加四行就好，不用動 `callLLM`：

```js
newprovider: {
  label:'顯示名稱', kind:'openai',
  url:'https://api.example.com/v1/chat/completions',
  models:['model-a','model-b'],
  note:'給使用者看的一行說明。'
}
```

`kind` 只有三種：`openai`（相容格式，多數）、`anthropic`（Messages API）、`gemini`（generateContent）。不需要金鑰的服務加上 `needsKey:false`。

## 授權

**這不是 open source，是 source-available。** 原始碼公開、可自由閱讀修改，但有一項限制。

- [LICENSE](LICENSE) — Functional Source License 1.1（MIT Future License）
- [ADDITIONAL-GRANT.md](ADDITIONAL-GRANT.md) — 著作權人發布的額外授權，**放寬**教學用途的限制

三句話版本：

| | |
|---|---|
| ✅ **可以** | 自己用、公司內部用、改它、發布你的修改版、**拿去上收費課程或企業內訓** |
| ❌ **不可以** | 把它（含改名換皮的版本）當產品賣、架成 SaaS 收費、做出功能實質相同的競品 |
| ⏳ **兩年後** | 每個版本在釋出滿兩年後自動轉為 MIT 授權，限制全部解除 |

判斷原則：**教學可以收費，軟體本身不可以。**

需要落在禁止範圍內的使用方式，歡迎洽談商用授權。

## 聯絡

**酒Ann** — cpw688@gmail.com

AI 應用開發 / 線上教學 / 客製化開發
