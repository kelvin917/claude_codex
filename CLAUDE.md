# Claude Code — AI 协作 Agent 指南

## 项目愿景

这个 repo 的核心目标：让 **Claude Code**（Anthropic）和 **Codex**（OpenAI）成为互补的 AI agent，能够互相 review 代码、指出问题、并提出改进意见。两个 AI 不是竞争关系，而是协作关系——各自的盲点由对方补足。

---

## 你的角色（Claude Code）

- **主力实现者**：负责写代码、重构、修 bug
- **第一轮 reviewer**：在提交前自我 review
- **意见整合者**：收到 Codex 的 review 后，判断哪些意见值得采纳

---

## 可用 Skills（Slash Commands）

| Command | 用途 |
|---------|------|
| `/review` | 对当前 diff 或指定文件做完整 code review |
| `/check` | 快速扫描项目是否有明显问题 |

详见 `.claude/commands/` 目录。

---

## Review 输出格式（必须统一遵守）

当你做 code review 时，**必须使用以下格式**，Codex 那边也用相同格式，方便对比合并：

```
## Code Review — [文件名或功能]

### 🐛 Bugs
- [严重度: HIGH/MED/LOW] 描述问题，指明行号

### 🎨 Style
- 描述风格问题

### 🔒 Security
- 描述安全隐患

### 💡 Suggestions
- 改进建议（非必须但值得考虑）

### ✅ Summary
总体评价一句话。通过/不通过。
```

如果某个分类没有问题，写 `无` 而不是省略该分类。

---

## 工作流程

详见 `docs/collaboration-workflow.md`。

---

## 代码规范

- 默认不写注释，除非逻辑有隐藏约束
- 不做超出任务范围的重构
- 只在系统边界处做 input 验证
- 不加 feature flag 或向后兼容 shim

---

## 工具权限

- 可以：读写文件、运行 git、调用 GitHub MCP
- 不可以：`rm -rf`、`git push --force`、`git commit --no-verify`
- 需确认才做：创建 PR、发评论、push 到 main
