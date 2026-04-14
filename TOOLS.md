# TOOLS.md — agNovel 工具与子 Agent 能力手册

---

## 统一任务包格式

每次调用子 Agent 时，使用以下统一格式：

```
【调用目标】     agent_id（nvl-framer / nvl-plotter / nvl-writer / nvl-checker）
【任务类型】     task_type（见下方枚举）
【项目代号】     {code}
【当前阶段】     中文描述当前在哪一步
【传递内容】     完整原始内容
【特殊要求】     用户原话（可为空）
```

### 任务类型枚举

| 类别 | 任务类型 | 适用 Agent |
|------|----------|------------|
| 框架 | `framework_init` / `framework_revision` | nvl-framer |
| 大纲 | `outline_init` / `outline_revision` / `outline_extend` | nvl-plotter |
| 章节 | `chapter_draft` / `chapter_revision` | nvl-writer |
| 审查 | `chapter_review` / `chapter_re_review` | nvl-checker |

---

## 子 Agent 能力

### nvl-framer（框架设计师）

**职能**：根据用户需求设计小说整体框架（世界观、主角、核心矛盾、写作基调、目标读者、预计字数等）

**调用时机**：新小说生产流程 Phase 1；用户要求修改框架时

**必传参数**：用户需求原文 + agNovel 整理的需求摘要

**输出格式**：Markdown 结构化框架文档（六模块）

---

### nvl-plotter（大纲策划师）

**职能**：根据确认的框架设计章节级剧情大纲（主线/支线、节奏安排、爽点分布）

**调用时机**：框架确认归档后；用户要求修改大纲时

**必传参数**：完整框架文档内容

**输出格式**：Markdown 分章节大纲，每章含 A-F 六要素

---

### nvl-writer（首席执笔）

**职能**：根据框架、大纲完成指定章节的正文创作；根据审查意见修改章节

**调用时机**：Phase 3 章节创作；nvl-checker 审查后的修改任务

**必传参数（创作）**：框架文档 + 大纲文档 + 当前章节六要素 + 章节编号

**必传参数（修改）**：原始章节内容 + 审查意见 + 用户确认的修改方向

**输出格式**：纯正文，含章节标题，Markdown 格式

---

### nvl-checker（挑剔的读者）

**职能**：以严苛读者视角审查章节内容（逻辑漏洞、节奏问题、爽点缺失、角色一致性、与大纲偏差等）

**调用时机**：nvl-writer 每次完成章节或修改后

**必传参数**：章节正文 + 框架文档 + 当前章节大纲六要素

**输出格式**：Markdown 审查报告（🔴🟡🟢 分级）

**迭代上限**：最多3轮，第3轮完成后将意见列表交用户决策

---

## 工具可用性检查

会话启动时，如项目处于进行中状态，验证：

```
□ Notion Repos/Novels/{code}/ 文件夹存在
□ {code}-framer.md 可读（Phase 1 完成标志）
□ {code}-outliner.md 可读（Phase 2 完成标志）
□ 最新 {code}-section-{num}.md 编号与 MEMORY.md 记录一致
```

---

## 环境配置

```
workspace_root: {由系统配置提供}
default_encoding: UTF-8
file_format: Markdown (.md)
date_format: YYYYMMDD
max_checker_rounds: 3
```
