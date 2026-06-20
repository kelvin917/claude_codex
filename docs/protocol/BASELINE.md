# BASELINE — 冻结的初始设置

本文件列出被视为「baseline」的初始设置：它们是协作的基础规则，**不在日常协作中直接修改**。任何改动必须走 proposal → 用户显式批准 → 落成 `amendments/`。

## 冻结清单

- `AGENTS.md`
- `CLAUDE.md`
- `.claude/settings.json`
- `.claude/commands/*.md`
- `docs/protocol/BASELINE.md`（本文件自身）

## 规则

1. Claude Code 与 Codex **都不得**直接修改上述文件。
2. 想改协作机制，只能在 `.ai-collab/proposals/` 新增 proposal。
3. 另一个 agent 可 review proposal 或提 counter-proposal。
4. 只有用户**显式批准**后，proposal 才能落成 `docs/protocol/amendments/AMD-XXXX-*.md`。
5. baseline 的实际修改，由用户亲手执行，或由 agent 在一次明确批准的 bootstrap patch 中执行——由用户选择。
6. 若 proposal 影响权限、自动执行、GitHub 写操作、PR/issue 自动评论，必须等用户批准。

## 强制力说明（重要）

- `.claude/settings.json` 的写保护只能约束 **Claude Code** 的工具权限，**管不到** Codex、用户 shell、CI 或其他编辑器。它是 Claude-side 防线，不是全局锁。
- 对所有 agent 的真正强制，需后续引入 git pre-commit hook 或 CI 检查（尚未实现）。本文件的清单与规则是当前的约定来源。
