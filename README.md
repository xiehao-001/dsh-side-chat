# Side Chat

`@eduwork/dsh-side-chat` · v0.1.2 · MulanPSL-2.0 AND MIT

Side Chat opens a temporary branch beside the main conversation so you can ask follow-up questions without derailing it. A side chat starts from any user message or finished assistant reply, inherits that point in the history through a standard seed fork, and runs in the native right sidebar with the same chat components.

The branch stays independent after creation: UI-level inherited messages are hidden, so only new side-chat content is shown. Closing the side chat stops generation and archives it through the public Workspace API, where its messages and workspace ownership remain available.

## Highlights

- Starts a side chat from any user message or completed assistant reply, in the native right sidebar.
- Forks with the standard seed fork (`agents.create({ seed })`), so the inherited history is the model context while the UI hides inherited messages.
- Closes through the public `workspaceRegistry.archiveSession` API, keeping message records and workspace ownership instead of deleting backend files.
- Keeps multiple side chats per main session, each pinned to its creation-time history snapshot; switching main sessions restores the matching side chat, messages, draft and annotations.
- Manages create, ownership and close over `/api/eduwork/side-chat` without modifying the Runtime or the UI bundle.
- Pairs with `@eduwork/dsh-annotation >=0.1.1 <0.2.0` to add "ask in side chat" to the selection action bar, including selections in streaming replies.
- Applies a system-prompt boundary and tool interception, so side-chat tools still follow the new session's permissions and the global concurrency rules.

## Install

Install this directory as a local DSH plugin bundle. From a shell:

```bash
dsh plugin --profile web add /absolute/path/to/dsh-side-chat
```

Or add the directory through the **Plugins** panel in DSH (local bundle). Restart the DSH app after installation; plugins are activated from the bundle patch (`cordis.patch.yml`).

## Configuration

No configuration keys: the bundle patch inserts the plugin with defaults.

## Requirements

- DeepSeek Harness `>=0.2.1 <0.3.0`
- Node `>=24.22.1`
- Peer packages: `@deepseek-ai/cordis`, `@deepseek-ai/dsh-session`, `react`

## Notes and limits

- This directory currently contains no `lib/` build output. `NEEDS-BUILD.md` states that the package must be built inside the EduWork source tree and the output copied back before it can be loaded.
- Requires host APIs for sessions, Workspace archiving and the right sidebar; this version is verified on the official DSH 0.2.1-rc.3 Runtime.
- Drafts are not guaranteed to survive a refresh or a forced exit; if an archive request never arrives, the persisted record can remain as an unarchived normal session.
- Closing a side chat does not undo file changes or external actions already performed; an active side chat cannot be promoted to a normal session, and nested forks, subagents, scheduled tasks and long-running background work are not supported. An archived side chat can still be opened as a normal session from the archive.

## 中文文档

[README.zh-CN.md](./README.zh-CN.md)

## License

MulanPSL-2.0 AND MIT — see [LICENSE](./LICENSE) and, where present, [LICENSE-MIT](./LICENSE-MIT). Extracted from the ECNU EduWork distribution (https://github.com/ECNU/EduWork); upstream copyright and license notices are preserved.
