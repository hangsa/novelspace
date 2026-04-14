# TOOLS.md — nvl-plotter 工具与知识库

> nvl-plotter 的核心能力来自内置的章节设计方法论与叙事节奏知识库。

---

## 统一任务包格式

agNovel 调用时传入统一任务包：

```
【调用目标】     nvl-plotter
【任务类型】     outline_init | outline_revision | outline_extend
【项目代号】     {code}
【当前阶段】     剧情大纲 Phase 2 / 大纲修改 / 续章延伸
【传递内容】     完整内容（见下方）
【特殊要求】     用户对本批大纲的特殊说明（可为空）
```

**outline_init 传递内容**：
- `{code}-framer.md` 完整内容
- 章节范围说明

**outline_revision 传递内容**：
- 当前大纲版本
- 用户修改意见

**outline_extend 传递内容**：
- 已有大纲
- 续章起始位置

---

## 内置知识库

### 章节叙事结构

- **场景目标理论**：每个场景必须改变故事状态，不变则无效
- **场景极性翻转**：从正到负或负到正产生戏剧张力
- **三场景法则**：建立→发展→转折

### 情绪节奏理论

- 情绪曲线设计：全章情绪必须有起伏
- 压力锅原理：爽感 = 压迫积累时长 × 强度
- 呼吸感节奏：高强度段后必须有短暂松弛

### 钩子理论

- 截章黄金位置：场景高潮前一刻
- 悬念分级：生死 > 秘密 > 情感 > 日常
- 钩子复合法：情绪高点 + 信息未完整 + 行动待发生

### 伏笔设计

- 植入时机：情节自然流动时顺势植入
- 回收时机：情绪高点前后顺势回收
- 单章不超过2个新伏笔

---

## 工具接口

### read_file（只读）

**必须读取**：`{code}-framer.md`

**按需读取**：`{code}-outliner.md`、`{code}-section-{num}.md`

### write_file（不可用）

所有输出通过 agNovel 传递。

---

## 能力边界

**能做的**：六要素大纲设计、伏笔管理、节奏规划、发现并上报框架问题

**不能做的**：修改已确认框架、保证市场反应、替代正文/审查

---

## 环境配置

```
agent_role: sub-agent（由 agNovel 调度）
output_format: Markdown
chapter_batch: 10-20章/批
input_from: agNovel
output_to: agNovel
foreshadowing_id: F-{三位数编号}
```
