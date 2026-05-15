# AI Diff Viewer

A sharper way to review what your AI CLI just changed.

Works with **Claude Code**, **Codex**, **Qwen**, and any CLI that writes files to your workspace. Sits quietly in your sidebar, lights up the lines an AI touched, and lets you accept or revert hunk-by-hunk without the editor getting in your face.

> Fork of [konan-1947/ai-cli-diff-view](https://github.com/konan-1947/claude_diff_view_vscode_extension) (MIT) with a non-intrusive UX, a configurable diff-editor policy, and a smarter Session panel.

---

## What's different

- **Auto-open diff editor is OFF by default.** Edits show as inline highlights inside the file you already have open — green / red gutter, hunks visible in place. The split-view diff opens **only when you ask for it**.
- **A toggle for the auto-open behaviour** lives at the bottom of the Session panel and in VS Code settings (`ai-cli-diff-view.autoOpenDiffEditor`). Flip it back on if you want the classic flow.
- **Session panel rows don't hijack clicks.** The row itself does nothing; on hover you get two explicit buttons:
  - **Open file** — opens the file in a normal editor (still with inline highlights).
  - **Open diff** — opens the split-view diff editor on demand.
- **Per-file Accept / Revert on hover** (`✓` / `✗`) next to those buttons, plus **Accept All / Revert All** above the list.
- **No more "I closed the diff, reopened the file, and the diff popped right back"** — that loop is gone.

Everything else from the upstream extension is preserved: snapshot-based hunk detection, CodeLens Accept/Revert in the diff editor, Alt+H / Alt+L navigation, Claude CLI hooks installer.

---

## Quick start

1. Install **AI Diff Viewer** from the VS Code Marketplace.
2. Open the **AI Diff Viewer** activity-bar view in the sidebar.
3. Click **Install CLI hooks** (one-time). This writes pre/post hooks into `~/.claude/settings.json` so the extension knows when Claude Code is about to write to a file.
4. Run your AI CLI as normal. As it edits files, you'll see the inline highlights appear. Open the **Session** panel to review changes file-by-file.

> Hook install currently targets Claude. Codex and Qwen still work via the workspace file watcher (no hooks needed) — slightly less precise on rapid multi-file writes, but functional.

---

## Keybindings

| Action                        | Default                |
|-------------------------------|------------------------|
| Accept all hunks in file      | `Cmd/Ctrl + Shift + Y` |
| Revert all hunks in file      | `Cmd/Ctrl + Shift + Z` |
| Previous edited file          | `Alt + H`              |
| Next edited file              | `Alt + L`              |
| Start Claude session (panel)  | `Cmd/Ctrl + Shift + A` |

All commands also live under `AI Diff: …` in the Command Palette.

---

## Settings

| Setting                                | Default | Effect |
|----------------------------------------|---------|--------|
| `ai-cli-diff-view.autoOpenDiffEditor`  | `false` | When true, opens the split-view diff editor automatically every time the AI CLI writes a file. When false (default), the extension only paints inline decorations and waits for an explicit **Open diff** action. |

---

## Why fork?

The upstream extension is excellent for the demo flow, but in a real review session the auto-opened diff editor competes with everything else you're doing — switching back to the file pops the diff back, closing it just to read the file is a loop. This fork makes the diff editor opt-in and keeps inline highlights as the default surface. Same engine underneath.

If you want the classic behaviour back, set `ai-cli-diff-view.autoOpenDiffEditor: true` (or toggle it in the Session panel) and the extension behaves exactly like upstream.

---

## Credits

- Original work: [konan-1947](https://github.com/konan-1947) — every line of the snapshot/hunk/CodeLens machinery is theirs.
- Fork & UX changes: [MtGlitch](https://github.com/EloWeld).

Bug reports and PRs welcome at <https://github.com/EloWeld/ai-diff-viewer>.

## License

MIT — see [LICENSE](./LICENSE).
