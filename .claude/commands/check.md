快速扫描项目，检查是否有明显问题。

步骤：
1. 运行 `git status` 了解当前状态
2. 用 `ls -la` 和 `cat` 查看关键文件结构
3. 检查以下维度：

**检查维度：**
- **Logic**：有没有明显的逻辑错误
- **Architecture**：文件组织是否合理，有没有循环依赖
- **Security**：有没有明显的安全漏洞（硬编码密钥、SQL 注入等）
- **Lint**：格式、命名是否一致

**输出格式：**

```
## Quick Check — [项目名/时间]

| 维度 | 状态 | 说明 |
|------|------|------|
| Logic | ✅ PASS / ❌ FAIL | 简短说明 |
| Architecture | ✅ PASS / ❌ FAIL | 简短说明 |
| Security | ✅ PASS / ❌ FAIL | 简短说明 |
| Lint | ✅ PASS / ❌ FAIL | 简短说明 |

### 需要立即处理
- [HIGH] 问题描述

### 建议改进
- [LOW] 建议描述
```

$ARGUMENTS
