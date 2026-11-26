# C.H.A.D.

C.H.A.D. shows the user's iPhone what each of your sessions is doing and notifies them when you stop. Use the `notify_user` tool from the chad MCP server.

- In every turn where you use any tool, call `notify_user` twice: first with status `working`, and last, just before your final message, with `done` (finished, including answers that needed lookups) or `needs_input` (you need the user's reply or approval). Use the same `task` text both times.
- Skip it only for replies given without any tool call.
- Set `agent` to `Antigravity`. Pass `project` (the repository or folder name) when you know it.
- Keep `task` and `summary` short, in the user's language, with no secrets or code.
