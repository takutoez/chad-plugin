# C.H.A.D. plugin for Claude Code, Codex, and Antigravity

C.H.A.D. shows your iPhone what each of your AI coding sessions is doing, and sends you a push notification when a session finishes or stops to wait for your answer. Start a task, switch to something else, and come back when your phone tells you it is done.

This plugin connects your coding agent to the C.H.A.D. server (`https://api.chadapp.link/mcp`). Updates reach the server in two ways, and both are first-class:

- **The agent itself** calls the `notify_user` tool at the start of a turn ("working") and at the end ("done" or "needs input"), with a short task name and summary.
- **Hooks** (Claude Code and Codex) call the same tool when you send a prompt, when the agent stops, and when it waits for your permission. They fire even when the agent forgets to call the tool or is blocked on a permission prompt. Hooks send no conversation text, only the status, the agent's name, and the folder you are working in.
- **Continue on your phone** (Claude Code). While [Remote Control](https://code.claude.com/docs/en/remote-control) is connected, a hook tells Claude the session's link (`https://claude.ai/code/session_…`) each time you send a prompt, and Claude passes it along with its updates. The app then shows a **Continue in Claude** button that opens the same session in the Claude app. Needs Claude Code 2.1.199 or later.

Hooks use the same MCP connection as the agent, so the server knows which updates come from the same session. When both report the same moment, you get one notification, and the agent's task name and summary fill in the hook's update. The same repository works as a plugin for Claude Code, Codex, and Google Antigravity.

## Requirements

- The C.H.A.D. app on your iPhone.
- In the app, sign in with Apple and turn on the connection with AI apps (Settings → Connect AI).
- When the agent asks you to sign in to **chad**, use the **same Apple ID** as in the app.

## Claude Code

```
/plugin marketplace add takutoez/chad-plugin
/plugin install chad@chad-marketplace
```

Then run `/mcp`, choose **chad**, and sign in. The hooks start working once **chad** is signed in (hooks never start a sign-in themselves).

## Codex

```
codex plugin marketplace add takutoez/chad-plugin
codex plugin add chad@chad-marketplace
codex mcp login chad
```

In the Codex app, you can also add the marketplace and install **C.H.A.D.** from the plugin directory.

To use the hooks, open `/hooks` in the CLI (or **Settings → Hooks** in the app), review the **chad** hooks, and trust them. Hooks need a recent Codex: tested with 0.172. Older versions such as 0.145 print a warning that they can't parse the hooks and fall back to the updates the agent sends itself.

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

Each call sends a short task name, a one-sentence summary, the status, the agent name (for example "Claude Code"), and the project (repository or folder) name. Hook calls send no task name; their summary is the agent's own fixed notice, such as "Claude needs your permission to use Bash". Hooks pass the working folder's path, and the server keeps only its last part (the folder name). The agent is told to keep these short and to leave out secrets and code. With Remote Control connected, Claude Code also sends the session's `claude.ai/code` link, so the app can reopen that session in the Claude app. No source code, files, or conversation history is sent. The server keeps an update only until the app receives it. See the [Privacy Policy](https://chadapp.link/en/privacy) for details.

## Uninstall

- Claude Code: `/plugin uninstall chad@chad-marketplace`
- Codex: `codex plugin remove chad@chad-marketplace`
- Antigravity: `agy plugin uninstall chad`, or delete `~/.gemini/config/plugins/chad` if you cloned it

To stop notifications from every AI app, turn off the connection in the C.H.A.D. app.

## Files

| Path | Used by |
| --- | --- |
| `.claude-plugin/`, `.mcp.json`, `hooks/hooks.json` | Claude Code |
| `.codex-plugin/`, `.agents/plugins/marketplace.json`, `.mcp.json`, `hooks/codex.json` | Codex |
| `.antigravity-plugin/`, `mcp_config.json`, `rules/AGENTS.md` | Antigravity |
| `assets/` | Codex and Antigravity (logo) |

---

## 日本語

C.H.A.D. は、AI のコーディング（Claude Code・Codex・Antigravity）の各セッションがいま何をしているかを iPhone に出し、作業が終わったときや返事を待って止まったときにプッシュ通知で知らせます。

1. iPhone の C.H.A.D. で「Apple でサインイン」をし、設定の「AI とつなぐ」で連携をオンにする。
2. 使っている AI に、プラグインを入れる。Claude Code と Codex では、AI が自分で送る知らせに加えて、フックがプロンプトを送ったとき・止まったとき・許可を待つときに必ず知らせます（同じ場面は 1 回の通知にまとめます。フックは会話の文面を送りません）。
   - Claude Code: `/plugin marketplace add takutoez/chad-plugin` → `/plugin install chad@chad-marketplace` → `/mcp` で **chad** を選ぶ。
   - Codex: `codex plugin marketplace add takutoez/chad-plugin` → `codex plugin add chad@chad-marketplace` → `codex mcp login chad`。フックを使うには、`/hooks`（アプリでは「設定 → Hooks」）で chad のフックを信頼する（0.172 で確認）。
   - Antigravity: `agy plugin install https://github.com/takutoez/chad-plugin`。CLI が無ければ `git clone https://github.com/takutoez/chad-plugin ~/.gemini/config/plugins/chad` をしてアプリを開き直す。どちらも、そのあと **Customizations** → **Installed** → MCP Servers の **chad** で **Authenticate** を押し、ブラウザに出たコードを貼る。
3. サインインの画面で、アプリと**同じ Apple ID** でサインインする。

送るのは、作業名・一言の要約・状態・AI の名前・プロジェクト（リポジトリやフォルダ）の名前です。Claude Code でリモートコントロールがつながっているあいだは、そのセッションのリンク（`https://claude.ai/code/session_…`）も送ります（アプリの「Claude で続きを開く」で、Claude アプリの同じセッションを開くため。Claude Code 2.1.199 以降）。ソースコードやファイル、会話の履歴は送りません。詳しくは[プライバシーポリシー](https://chadapp.link/privacy)をご覧ください。
