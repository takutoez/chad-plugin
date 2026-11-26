# C.H.A.D. for Claude Code

C.H.A.D. shows your iPhone what each of your Claude Code sessions is doing, and sends you a push notification when a session finishes or stops to wait for your answer. Start a task, switch to something else, and come back when your phone tells you it is done.

This plugin connects Claude Code to the C.H.A.D. server (`https://api.chadapp.link/mcp`). It adds one tool, `notify_user`, which Claude calls at the start of a turn ("working") and at the end ("done" or "needs input").

## Requirements

- The C.H.A.D. app on your iPhone.
- In the app, sign in with Apple and turn on the connection with AI apps (Settings → Connect AI).

## Install

```
/plugin marketplace add takutoez/chad-plugin
/plugin install chad@chad-marketplace
```

Then run `/mcp`, choose **chad**, and sign in with the **same Apple ID** you use in the C.H.A.D. app. After that, Claude Code reports each session's status to your phone.

## What is sent

Each call sends a short task name, a one-sentence summary, the status, the agent name ("Claude Code"), and the project (repository or folder) name. Claude is told to keep these short and to leave out secrets and code. No source code, files, or conversation history is sent. The server keeps an update only until the app receives it. See the privacy policy in the app's settings for details.

## Uninstall

```
/plugin uninstall chad@chad-marketplace
```

To stop notifications from every AI app, turn off the connection in the C.H.A.D. app.

---

## 日本語

C.H.A.D. は、Claude Code の各セッションがいま何をしているかを iPhone に出し、作業が終わったときや返事を待って止まったときにプッシュ通知で知らせます。

1. iPhone の C.H.A.D. で「Apple でサインイン」をし、設定の「AI とつなぐ」で連携をオンにする。
2. Claude Code で `/plugin marketplace add takutoez/chad-plugin` → `/plugin install chad@chad-marketplace` を実行する。
3. `/mcp` で **chad** を選び、アプリと**同じ Apple ID** でサインインする。

送るのは、作業名・一言の要約・状態・AI の名前・プロジェクト（リポジトリやフォルダ）の名前だけです。ソースコードやファイル、会話の履歴は送りません。
