对以下代码或当前 git diff 做完整 code review。

如果用户没有提供具体文件，先运行 `git diff HEAD` 获取最新改动，再进行 review。

**必须使用以下标准格式输出**（与 Codex 端格式完全一致）：

```
## Code Review — [文件名或功能描述]

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

规则：
- 每个分类如果没有问题，写「无」，不省略该分类
- 严重度必须标注 HIGH / MED / LOW
- 意见必须具体，指明文件名和行号
- 不推荐没有理由的风格偏好

$ARGUMENTS
