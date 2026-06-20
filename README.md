# claude_codex

让 **Claude Code**（Anthropic）和 **Codex**（OpenAI）成为互补的 AI agent：互相 review 代码、补足彼此盲点。两个 AI 用**完全相同的输出格式**工作，方便对比和合并意见。

---

## 一、环境准备

### Claude Code
正常使用即可（你现在用的就是）。

### Codex CLI
本机已用 nvm 安装（避开 root 全局目录）：

```bash
# 安装（首次）
nvm use 24
npm install -g @openai/codex

# 登录（首次，浏览器 OAuth，连 ChatGPT/OpenAI 账号）
codex login

# 验证
codex --version    # codex-cli 0.x
```

---

## 二、核心协作流程

```
1. Claude Code 实现 / 修 bug
2. Claude Code 自我 review（/review）
3. Claude Code 整合 + 落盘到 .ai-collab/
4. Codex 独立 review（codex exec 读同一份内容）
5. 用户对比两份意见，决定采纳
6. Claude Code 整合意见，出「采纳报告」（DEC-XXXX）
7. 重复 4–6 直到两边都「通过」
8. 用户最终确认
```

详见 [docs/collaboration-workflow.md](docs/collaboration-workflow.md)。

---

## 三、怎么用

### A. 让 Claude Code review
在 Claude Code 里输入 slash command：

| 命令 | 用途 |
|------|------|
| `/review` | 对当前 diff 或指定文件做完整 code review |
| `/check` | 快速扫描项目是否有明显问题 |
| `/propose` | 新建一份协作提案（PROP-XXXX），用于修改协作机制/baseline |

### B. 让 Codex review（在本 repo 目录下）
```bash
cd claude_codex
codex exec "读 <文件路径>，按 AGENTS.md 的标准格式做 code review"
```
也可以直接 `codex` 进交互界面。

### C. 统一 review 输出格式（两边一致）
```
## Code Review — [文件名或功能]

### 🐛 Bugs
- [严重度: HIGH/MED/LOW] 描述问题，指明行号

### 🎨 Style / 🔒 Security / 💡 Suggestions
- ...

### ✅ Summary
总体评价一句话。通过/不通过。
```
没有问题的分类写「无」，不省略。

---

## 四、Baseline + Amendments（保护初始设置）

为防止两个 AI 把初始设置改乱，采用 **Baseline + Amendments** 协议。

### Baseline（冻结，不可直接改）
见 [docs/protocol/BASELINE.md](docs/protocol/BASELINE.md)：
- `AGENTS.md`、`CLAUDE.md`、`.claude/settings.json`、`.claude/commands/*.md`、`docs/protocol/BASELINE.md`

> ⚠️ `.claude/settings.json` 的写保护只能约束 Claude Code，**管不到** Codex / shell / CI。它是 Claude-side 防线，不是全局锁。

### 想改协作机制？走提案流程
```
/propose <你的诉求>          # 生成 PROP-XXXX（不直接改 baseline）
  → 另一个 agent review
  → 用户显式批准
  → 落成 docs/protocol/amendments/AMD-XXXX + 同步 CURRENT.md
```

### 编号规则
- `PROP-XXXX` 提案 · `AMD-XXXX` 已批准修正案 · `DEC-XXXX` 决议/采纳报告
- 不要求一一对应：一个 PROP 可有多个 DEC。

**当前生效规则的单一事实来源**：[docs/protocol/CURRENT.md](docs/protocol/CURRENT.md)

---

## 五、目录结构

```
claude_codex/
├── AGENTS.md                 # Codex 的角色与格式（baseline）
├── CLAUDE.md                 # Claude Code 的角色与格式（baseline）
├── README.md                 # 本文件
├── .claude/
│   ├── settings.json         # 权限配置（baseline）
│   └── commands/             # slash 命令：review / check / propose（baseline）
├── docs/
│   ├── collaboration-workflow.md
│   └── protocol/
│       ├── BASELINE.md       # 冻结清单（baseline）
│       ├── CURRENT.md        # 当前生效规则汇总
│       └── amendments/       # 已批准的修正案 AMD-XXXX
└── .ai-collab/
    ├── proposals/            # 提案 PROP-XXXX
    └── decisions/            # review / 第二意见 / 采纳报告 DEC-XXXX
```
