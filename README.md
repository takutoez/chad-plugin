# C.H.A.D. plugin for Claude Code, Codex, and Antigravity

C.H.A.D. shows your iPhone what each of your AI coding sessions is doing, and sends you a push notification when a session finishes or stops to wait for your answer. Start a task, switch to something else, and come back when your phone tells you it is done.

This plugin connects your coding agent to the C.H.A.D. server (`https://api.chadapp.link/mcp`). It adds one tool, `notify_user`, which the agent calls at the start of a turn ("working") and at the end ("done" or "needs input"). The same repository works as a plugin for Claude Code, Codex, and Google Antigravity.

## Requirements

- The C.H.A.D. app on your iPhone.
- In the app, sign in with Apple and turn on the connection with AI apps (Settings → Connect AI).
- When the agent asks you to sign in to **chad**, use the **same Apple ID** as in the app.

## Claude Code

```
/plugin marketplace add takutoez/chad-plugin
/plugin install chad@chad-marketplace
```

Then run `/mcp`, choose **chad**, and sign in.

## Codex

```
codex plugin marketplace add takutoez/chad-plugin
codex plugin add chad@chad-marketplace
codex mcp login chad
```

In the Codex app, you can also add the marketplace and install **C.H.A.D.** from the plugin directory.

## Antigravity

With the `agy` CLI:

```
agy plugin install https://github.com/takutoez/chad-plugin
```

With the Antigravity app only (no CLI), put this repository in the global plugins folder and restart the app:

```
git clone https://github.com/takutoez/chad-plugin ~/.gemini/config/plugins/chad
```

Then open **Customizations** → **Installed**, and under **MCP Servers** click **Authenticate** next to **chad**. Sign in in the browser, copy the authorization code, paste it into **Enter authorization code**, and click **Submit**. To update later, run `git -C ~/.gemini/config/plugins/chad pull`.

## What is sent

Each call sends a short task name, a one-sentence summary, the status, the agent name (for example "Claude Code"), and the project (repository or folder) name. The agent is told to keep these short and to leave out secrets and code. No source code, files, or conversation history is sent. The server keeps an update only until the app receives it. See the [Privacy Policy](https://chadapp.link/en/privacy) for details.

## Uninstall

- Claude Code: `/plugin uninstall chad@chad-marketplace`
- Codex: `codex plugin remove chad@chad-marketplace`
- Antigravity: `agy plugin uninstall chad`, or delete `~/.gemini/config/plugins/chad` if you cloned it

To stop notifications from every AI app, turn off the connection in the C.H.A.D. app.

## Files

| Path | Used by |
| --- | --- |
| `.claude-plugin/`, `.mcp.json` | Claude Code |
| `.codex-plugin/`, `.agents/plugins/marketplace.json`, `.mcp.json` | Codex |
| `.antigravity-plugin/`, `mcp_config.json`, `rules/AGENTS.md` | Antigravity |
| `assets/` | Codex and Antigravity (logo) |

---

## 日本語

C.H.A.D. は、AI のコーディング（Claude Code・Codex・Antigravity）の各セッションがいま何をしているかを iPhone に出し、作業が終わったときや返事を待って止まったときにプッシュ通知で知らせます。

1. iPhone の C.H.A.D. で「Apple でサインイン」をし、設定の「AI とつなぐ」で連携をオンにする。
2. 使っている AI に、プラグインを入れる。
   - Claude Code: `/plugin marketplace add takutoez/chad-plugin` → `/plugin install chad@chad-marketplace` → `/mcp` で **chad** を選ぶ。
   - Codex: `codex plugin marketplace add takutoez/chad-plugin` → `codex plugin add chad@chad-marketplace` → `codex mcp login chad`。
   - Antigravity: `agy plugin install https://github.com/takutoez/chad-plugin`。CLI が無ければ `git clone https://github.com/takutoez/chad-plugin ~/.gemini/config/plugins/chad` をしてアプリを開き直す。どちらも、そのあと **Customizations** → **Installed** → MCP Servers の **chad** で **Authenticate** を押し、ブラウザに出たコードを貼る。
3. サインインの画面で、アプリと**同じ Apple ID** でサインインする。

送るのは、作業名・一言の要約・状態・AI の名前・プロジェクト（リポジトリやフォルダ）の名前だけです。ソースコードやファイル、会話の履歴は送りません。詳しくは[プライバシーポリシー](https://chadapp.link/privacy)をご覧ください。
