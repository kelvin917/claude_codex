新建一份协作提案（proposal），用于修改协作机制或 baseline。

步骤：
1. 扫描 `.ai-collab/proposals/`，找出最大的 `PROP-XXXX` 编号，新提案号 = 最大号 + 1（四位补零，如 `PROP-0002`）。
2. 根据 `$ARGUMENTS` 描述的诉求，在 `.ai-collab/proposals/PROP-XXXX-<kebab-标题>.md` 写入提案。
3. **不要**直接修改任何 baseline 文件（见 `docs/protocol/BASELINE.md` 清单），提案只描述「希望怎么改」。

提案模板：

```
# PROP-XXXX: 标题

Status: proposed
Author: <claude-code | codex | user>
Target: <另一个 agent>
Requires User Approval: <true | false>
Supersedes: <可选，被本提案取代的 PROP 号>

## 背景
说明问题或动机。

## 提案
具体改动方案。

## 希望对方做的事
请对方 review 并回答的问题。

## 安全要求
列出不可直接修改的文件、需要用户批准的点。
```

规则：
- `Status` 取值：`proposed / accepted / rejected / superseded`。
- 若提案影响权限、自动执行、GitHub 写操作、PR/issue 自动评论，`Requires User Approval` 必须为 `true`。
- 提案编号与 decision 不要求一一对应；一个 PROP 可对应多个 DEC。
- 写完后提示用户：下一步可让另一个 agent review（Claude 用 `/review`，Codex 用 `codex exec`）。

$ARGUMENTS
