# Session: 2026-03-17 05:42:58 UTC

- **Session Key**: agent:agnovel:feishu:direct:ou_dc8c0a460d1eb853e320e9994459675e
- **Session ID**: 772244e6-ff13-494d-bf10-1d909b0270e1
- **Source**: feishu

## Conversation Summary

user: Conversation info (untrusted metadata):
```json
{
  "message_id": "om_x100b547bcdbe14acc3b1ee6235d0726",
  "sender_id": "ou_dc8c0a460d1eb853e320e9994459675e",
  "sender": "ou_dc8c0a460d1eb853e320e9994459675e",
  "timestamp": "Sat 2026-03-14 13:55 GMT+8"
}
```

Sender (untrusted metadata):
```json
{
  "label": "ou_dc8c0a460d1eb853e320e9994459675e",
  "id": "ou_dc8c0a460d1eb853e320e9994459675e",
  "name": "ou_dc8c0a460d1eb853e320e9994459675e"
}
```

[message_id: om_x100b547bcdbe14acc3b1ee6235d0726]
ou_dc8c0a460d1eb853e320e9994459675e: 查看下openclaw中配置了哪些agent
assistant: [curAgent:agnovel, curModel:minimax/MiniMax-M2.5]

当前 OpenClaw 配置了 **5 个 Agent**：

| Agent | 说明 | 工作目录 | 模型 |
|-------|------|----------|------|
| **main** (default) | 默认主Agent | ~/.openclaw/workspace | moonshot/kimi-k2.5 |
| **agnovel** (agNovel) | 爽文工厂主控 | ~/.openclaw/novelspace | moonshot/kimi-k2.5 |
| **nvl-outliner** | 大纲设计Agent | ~/.openclaw/novelspace/outlines | moonshot/kimi-k2.5 |
| **nvl-writer** | 写作Agent | ~/.openclaw/novelspace/wirtes | zai/glm-4.7-flash |
| **nvl-critic** | 质检Agent | ~/.openclaw/novelspace/critics | moonshot/kimi-k2.5 |

**路由规则**：
- `main` 和 `agnovel` 各有 1 条路由规则
- `nvl-outliner`、`nvl-writer`、`nvl-critic` 暂无路由规则（需要通过其他 Agent 调用）

看起来这是一个爽文小说生成的工作流系统，对应 `AGENTS.md` 中描述的 workflow：
1. `agnovel` 接收需求 → 2. 派发给 `nvl-outliner` 设计大纲 → 3. 派发给 `nvl-writer` 写作 → 4. 派发给 `nvl-critic` 质检
