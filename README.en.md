<p align="center">
  <img src="assets/logo.png" alt="酒Ann" width="140">
</p>

<h1 align="center">Brand Content Engine</h1>

<p align="center">
  by <b>酒Ann</b> · AI Application &amp; Developer / Online Educator &amp; Customized Creator
</p>

<p align="center">
  <a href="README.md">繁體中文</a> · <b>English</b>
</p>

A brand content pipeline in **a single HTML file**. Download one file, open it in a browser, and run the whole flow: crawl your own site, analyze your positioning, break down your rivals, produce content.

No backend, no install, no account, no dependencies.

## Quick start

1. Download `brand-content-engine pro.html`
2. Open it in a browser (double click is enough)
3. Under "00 Model & API Key" pick a provider and paste an API key
4. Hit "Test connection", then work down the steps

To try it at zero cost, pick **Groq** (free tier, very fast) or **Ollama** (runs on your own machine, completely free).

## Interface and output language

Two independent controls:

- **Interface language**: the 中 / EN switch at the top right changes every label, button and message. Your choice is remembered in this browser.
- **Output language**: the dropdown in step 00 decides what language the model writes in. You can read the interface in English while generating Traditional Chinese copy, or the other way round.

## Privacy

Your API key lives only in your own browser `localStorage` and goes **straight to the model provider with no intermediary server**, because this project has no server at all.

If you would rather not keep it, leave "Remember key on this computer" unticked and the key will only live in the current tab.

## Supported models

Nine providers:

| Provider | Suggested models | Get a key | Good for |
|---|---|---|---|
| **Anthropic Claude** | `claude-sonnet-5`, `claude-opus-5`, `claude-haiku-4-5-20251001` | console.anthropic.com | Long context, reliable structured output |
| **OpenAI** | `gpt-4o-mini`, `gpt-4o`, `gpt-4.1-mini` | platform.openai.com | Most people already have an account |
| **Google Gemini** | `gemini-2.0-flash`, `gemini-2.5-flash`, `gemini-2.5-pro` | aistudio.google.com | Free tier |
| **DeepSeek** | `deepseek-chat`, `deepseek-reasoner` | platform.deepseek.com | Low cost per token |
| **Kimi (Moonshot)** | `moonshot-v1-32k`, `moonshot-v1-128k`, `kimi-latest` | platform.moonshot.cn | Long documents |
| **Zhipu GLM** | `glm-4-plus`, `glm-4-flash`, `glm-4-air` | open.bigmodel.cn | China based |
| **MiniMax** | `MiniMax-Text-01`, `abab6.5s-chat` | platform.minimax.chat | China based |
| **Groq** | `llama-3.3-70b-versatile`, `llama-3.1-8b-instant`, `qwen-2.5-32b` | console.groq.com | Very fast, free tier |
| **Ollama** | `llama3.2`, `qwen2.5:7b`, `gemma3` | No key needed | No API cost, runs locally |

### About CORS

This is a pure front end tool, so calling an API directly from the browser requires the provider to allow cross origin requests. **Anthropic, OpenAI, Gemini and Groq are known to work.** The China based providers (DeepSeek, Kimi, GLM, MiniMax) depend on their own CORS policy; if one blocks the request the tool will tell you exactly why.

### Using Ollama

Let the local service accept browser connections first, otherwise CORS will block it:

```bash
OLLAMA_ORIGINS=* ollama serve
```

Then pull a model:

```bash
ollama pull llama3.2
```

## Adding a provider

Every provider lives in the `PROVIDERS` table. Most services are compatible with the OpenAI `/chat/completions` shape, and those need four lines with no change to `callLLM`:

```js
newprovider: {
  label:'Display name', kind:'openai',
  url:'https://api.example.com/v1/chat/completions',
  models:['model-a','model-b'],
  note:'One line shown to the user.'
}
```

There are only three values for `kind`: `openai` (compatible shape, most of them), `anthropic` (Messages API) and `gemini` (generateContent). Add `needsKey:false` for services that need no key.

## Adding an interface language

Interface strings are translated through one dictionary keyed by the original Traditional Chinese text, plus a DOM walker that swaps text nodes. Labels rendered from JavaScript template literals are picked up automatically, so there is no need to touch the rendering code. Add a dictionary next to `I18N_EN` and one more button in `.langsw`.

## License

**This is not open source, it is source available.** The code is public and you may read and modify it freely, with one restriction.

- [LICENSE](LICENSE): Functional Source License 1.1 (MIT Future License)
- [ADDITIONAL-GRANT.md](ADDITIONAL-GRANT.md): an additional grant from the copyright holder that **loosens** the restriction for teaching

The short version:

| | |
|---|---|
| ✅ **Allowed** | Personal use, internal company use, modification, publishing your own fork, **using it to run paid courses and corporate training** |
| ❌ **Not allowed** | Selling it (including rebranded versions) as a product, charging for it as a hosted service, building a substantially similar competing product |
| ⏳ **After two years** | Each release converts to the MIT license two years after publication and every restriction falls away |

The rule of thumb: **you may charge for teaching, you may not sell the software itself.**

If your use falls inside the restricted range, commercial licensing is available.

## Contact

**酒Ann**　cpw688@gmail.com

AI application development / online education / custom development
