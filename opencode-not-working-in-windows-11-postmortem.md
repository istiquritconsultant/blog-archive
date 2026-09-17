# OpenCode Not Working in Windows 11 — CLI + Desktop Postmortem

> [!NOTE]
> **OpenCode Not Working in Windows 11** — both the CLI and the Desktop app failed to start a session, at the same time, after five custom subagent files were added with the wrong config shape. This doc covers the exact error text, root cause, fix, and verification.

**Status:** Resolved · **Severity:** High (both entry points down) · **Fix size:** 5 files, 1 line each

## Table of Contents

- [Environment](#environment)
- [Symptom](#symptom)
- [Error Text](#error-text)
- [Root Cause](#root-cause)
- [Why Both Apps Failed Together](#why-both-apps-failed-together)
- [Fix](#fix)
- [Verification](#verification)
- [Related Finding](#related-finding)
- [Takeaways](#takeaways)

## Environment

| Component | Value |
|---|---|
| OS | Windows 11 Pro Insider Preview, build 10.0.26300, 64-bit |
| OpenCode CLI | v1.18.23 (global npm install) |
| OpenCode Desktop | v1.18.25 |
| Node.js | v26.7.0 |

## Symptom

Both `opencode` (CLI) and OpenCode Desktop fail to start a session immediately, on every launch attempt — not a slow load, a hard stop.

## Error Text

**CLI:**

```text
Configuration is invalid at C:\Users\istiqur\.config\opencode\agents\blog-writer.md
↳ Expected object | undefined, got ["Read","Write","Edit","Grep","Glob"] tools
```

**Desktop (`renderer.log`):**

```text
[2026-08-30 14:11:29.555] [error]  Failed to load sessions Error: ConfigInvalidError
[2026-08-30 14:11:36.928] [error]  Failed to finish bootstrap instance Error: ConfigInvalidError
```

> [!TIP]
> When a GUI app and a CLI tool share a core, reproduce the failure in the CLI first — it's often far more descriptive. Here, the CLI named the exact file and field; the Desktop app's log named neither.

## Root Cause

Five subagent files under `~/.config/opencode/agents/` declared `tools:` as a YAML **list**:

```yaml
tools:
  - Read
  - Write
  - Edit
```

[OpenCode's config schema](https://opencode.ai/docs/config/) requires `tools` as a YAML **map**:

```yaml
tools:
  read: true
  write: true
  edit: true
```

Both are valid YAML independently. [Per the YAML 1.2.2 spec](https://yaml.org/spec/1.2.2/), a sequence and a mapping are distinct node types — the file parses cleanly and only fails once a stricter schema inspects its shape.

```
blog-writer.md      -> Read, Write, Edit, Grep, Glob
blog-seo.md          -> Read, Grep, Glob
blog-reviewer.md     -> Read, Grep, Glob
blog-researcher.md   -> WebSearch, WebFetch, Read, Grep, Glob
blog-translator.md   -> Read, Write, Edit, Glob, Grep
```

All five files carried the identical defect — a batch-import mismatch, not an isolated typo.

## Why Both Apps Failed Together

CLI and Desktop are separate installers with independent version numbers, but they share:

- one config root: `~/.config/opencode/`
- one local sidecar server, spawned by both at startup:

```text
[info]  spawning sidecar { url: 'http://127.0.0.1:11956' }
[info]  server ready { url: 'http://127.0.0.1:11956' }
```

The sidecar itself started cleanly (`main.log` shows no errors) in both cases. The failure occurs specifically when the app asks the running server to enumerate the agents directory. Config errors introduced through either surface will therefore break both.

## Video Walkthrough

https://www.youtube.com/watch?v=jZcRgkG01Gg

## Fix

```diff
 tools:
-  - Read
-  - Write
-  - Edit
+  Read: true
+  Write: true
+  Edit: true
```

Applied identically across all five files. Frontmatter only — no reinstall, no cache clear, no plugin reset.

## Verification

```bash
$ opencode
# → TUI launches cleanly
# → 0 matches for "invalid" / "error" in captured output
```

| Check | Before | After |
|---|---|---|
| CLI startup | Fatal error | Clean launch |
| Desktop `renderer.log` | 6 errors | 0 |
| Desktop `main.log` | No errors | No errors |
| Bootstrap | Failed | Succeeded |

> [!WARNING]
> The first Desktop log folder checked post-fix still showed old errors — it was a session created *before* the fix was saved. Always compare a log session's own start timestamp against the fix's file-modification time before concluding a fix failed.

## Related Finding

`opencode.json` was found storing MCP service API keys in plaintext during this investigation — unrelated to the crash, but worth an audit on any OpenCode install. Keep such files out of version control; prefer environment variables for live keys.

## Takeaways

- Subagent/plugin config formats are not portable between AI coding tools by default, even with near-identical file conventions.
- Eager, fail-closed, whole-config validation means one bad file can abort every entry point.
- A CLI and a GUI app sharing one config root will share failure modes, regardless of separate installers/versions.
- Error message quality varies by surface, even within one product — reproduce in the CLI first.
- Timestamp-check log evidence before trusting it during verification.

---

Full technical writeup (complete diffs, environment fingerprint, appendix): https://istiquritconsultant.com/workflow-optimization-blogs/opencode-not-working-windows-11/

More postmortems: https://istiquritconsultant.com/workflow-optimization-blogs/

This postmortem topic was chosen by a newsletter reader vote — 69%, ahead of two other real incidents (13%, 18%). Open an issue or comment with topic suggestions for the next one, or subscribe: https://istiquritconsultant.com/no-spam-tech-newsletter/

## Find Me Elsewhere

- [Hashnode](https://istiqur-it-consultant.hashnode.dev/)
- [Pastebin](https://pastebin.com/u/remotegtmmanager)
- [X (Twitter)](https://x.com/mdistiqurrahman)
- [Blogger](https://remoteseoconsultant.blogspot.com/)
- [Dev.to](https://dev.to/remoteseoconsultant)
- [Google Sites](https://sites.google.com/view/remotegtmmanager/)
- [LinkedIn](https://www.linkedin.com/in/md-istiqur-rahman-rabby/)
- [CoderLegion](https://coderlegion.com/user/remoteseoconsultant)
- [Medium](https://remoteseoconsultant.medium.com/)
- [Substack](https://istiquritconsultant.substack.com/)
