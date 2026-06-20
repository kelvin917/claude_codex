# AI 协作 Review 工作流程

## 角色定义

| AI | 角色 | 主要职责 |
|----|------|----------|
| Claude Code | 主力实现者 + 第一轮 reviewer | 写代码、重构、整合意见 |
| Codex | 独立 reviewer | 提出第二意见、发现盲点 |

两个 AI 的 review 输出格式完全相同，方便用户对比和合并意见。

---

## 标准工作流程

```
1. Claude Code 实现功能 / 修 bug
        ↓
2. Claude Code 自我 review（/review）
        ↓
3. Claude Code 提交 PR
        ↓
4. Codex 独立 review（读取同一份 diff）
        ↓
5. 用户对比两份 review，决定采纳哪些意见
        ↓
6. Claude Code 整合意见，更新代码
        ↓
7. 重复直到两边都通过
```

---

## 触发 Codex Review 的方式

在 PR 或 issue 中，用以下格式请求 Codex review：

```
@codex 请对以下 diff 做 code review，使用标准格式输出：

[粘贴 git diff 内容]
```

Codex 会按照 `AGENTS.md` 里定义的格式返回 review 结果。

---

## Review 格式（两边统一）

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

没有问题的分类写「无」，不省略。

---

## 意见冲突处理

当 Claude Code 和 Codex 意见相反时：

1. **两边都标 HIGH** → 用户必须介入决定
2. **一边 HIGH，一边 LOW** → 优先采纳 HIGH 的判断
3. **纯 Style 冲突** → 用户选择偏好，或维持现状
4. **一边通过，一边不通过** → 默认不合并，等用户决定

---

## 意见整合规则（Claude Code 负责）

收到 Codex review 后，Claude Code 按以下优先级处理：

1. **Bugs (HIGH)** → 必须修复，不接受不采纳
2. **Bugs (MED)** → 默认修复，除非有充分理由
3. **Security** → 必须修复
4. **Bugs (LOW) / Style / Suggestions** → 参考采纳，列出不采纳原因

每次整合后，Claude Code 输出一份「意见采纳报告」：

```
## 意见采纳报告

### 已采纳
- [来源: Codex] 描述修复内容

### 未采纳
- [来源: Codex] 描述问题 → 原因：...
```

---

## 终止条件

当以下条件都满足时，该功能/PR 视为完成：

- Claude Code review：通过
- Codex review：通过
- 所有 HIGH 级别问题已修复
- 用户最终确认
