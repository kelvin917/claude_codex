# CURRENT — 当前生效的协作规则汇总

> 本文件是「当前生效规则」的单一事实来源。**每次新增 amendment，必须在同一变更里同步更新本文件**，否则该 amendment 不算完成。
> 规则只有在用户**显式批准**后才进入「已生效」区。

## 已生效的规则

1. **review 统一格式**：两个 agent 都使用 AGENTS.md / CLAUDE.md 规定的标准格式（Bugs / Style / Security / Suggestions / Summary）。
2. **基础工作流**：Claude Code 实现 + 第一轮 review → Codex 独立第二意见 → 用户对比裁决 → Claude Code 整合，详见 `docs/collaboration-workflow.md`。
3. **意见冲突与整合规则**：见 `docs/collaboration-workflow.md`（HIGH / Security 必修等）。
4. **Baseline 冻结**：见 `BASELINE.md` 清单，两个 agent 不得直接修改；改动走 proposal → 用户批准 → amendment。
5. **变更流程**：`.ai-collab/proposals/PROP-XXXX` → 另一 agent review → 用户批准 → `docs/protocol/amendments/AMD-XXXX` + 同步本文件。
6. **编号规则**：`PROP-XXXX`（提案）/ `AMD-XXXX`（修正案）/ `DEC-XXXX`（决议）；不要求一一对应，一个 PROP 可有多个 DEC，decision 文件名带回链。
7. **proposal 状态机**：frontmatter `Status:` 取值 `proposed / accepted / rejected / superseded`。
8. **可选字段**：`Supersedes:` / `Superseded-by:`，非必填。
9. **settings.json 写保护**：deny 已拦截对 baseline 的 Edit/Write（Claude-side 防线，管不到 Codex / shell / CI）。
10. **`/propose` 命令**：见 `.claude/commands/propose.md`，自动生成下一个 PROP 编号。

## 已批准的 amendments

（暂无。第一个修正案将从 AMD-0001 起。）

## 待批准后生效

（暂无。）

## 未来增强（非阻塞）

- git pre-commit hook 或 CI 检查，对所有 agent 强制 baseline 保护（settings.json 管不到 Codex / shell / CI）。
