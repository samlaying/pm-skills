# PM Skills — 产品经理工作流 Skill 集

一套面向产品经理日常工作的 Agent Skills，覆盖项目上下文维护、会议处理、任务拆解、PRD 写作、评审反馈处理、汇报通知和个人沟通复盘。

这套 skills 以 `SKILL.md` 为核心格式，适合 Claude Code，也可以同步安装到 Codex 的 `.agents/skills/`。

---

## 一句话安装

把下面这句话发给你的 agent：

> 帮我把 https://github.com/samlaying/pm-skills 这个仓库的 skills 安装到当前项目。如果是 Claude Code，安装到 `.claude/skills/`；如果是 Codex，安装到 `.agents/skills/`；然后在项目说明文件里注册路由。

agent 会自己 clone、复制、注册。

---

## 这套 Skills 能做什么

一句话概括：

**会议材料 → 项目记忆 → 任务拆解 → PRD → 评审反馈 → 汇报通知**。  
`meeting-coach` 单独作为个人成长分支，用来复盘会议里的沟通表现和软实力。

| Skill | 什么时候用 | 主要产出 |
|-------|------------|----------|
| `project-context-maintainer` | 维护项目背景、内部术语、关键决策、需求点层级 | `项目上下文.md`、`内部术语表.md`、`项目工作记录.md` |
| `meeting-notes-organizer` | 处理会议录音、飞书妙记、会议纪要，或基于会议拆 todo | 会议记录、需求点文件、行动项、技术细节文档 |
| `task-arrangement-planner` | 领导安排一个活，需要拆推进节奏、补信息、沟通话术 | 任务安排、推进计划、待补信息、沟通话术 |
| `prd-writer` | 评审前写 PRD、更新 PRD 初稿、整理成可评审需求文档 | V3.0 PRD、Happy Path、异常流程、飞书链接 |
| `prd-review-handler` | PRD 评审后处理评论、对比飞书最新版、写验收标准 | 反馈处理记录、修订版 PRD、验收标准、同步记录 |
| `update-writer` | 写汇报、通知、进展同步、风险通报 | 汇报/通知文档、飞书链接 |
| `meeting-coach` | 复盘自己在会议/对话中的沟通表现 | 行为复盘报告、改进话术、行动清单 |
| `ai-pm-prd-builder` | 设计 AI / Agent 产品，交互式引导产出 AI 产品 PRD（节点流、节点契约、模型选型、评测体系） | AI 产品 PRD、节点契约、选型与评测方案 |

---

## 工作流全景

```text
项目启动
  └─ project-context-maintainer（建立项目记忆）

需求阶段
  ├─ meeting-notes-organizer（会议材料 → 会议纪要 + todo）
  ├─ task-arrangement-planner（领导安排 → 推进计划）
  └─ prd-writer（材料 → 评审前 PRD → 飞书）

评审阶段
  └─ prd-review-handler（评审反馈 → 修订 PRD → 验收标准）

日常同步
  ├─ update-writer（汇报 / 通知 / 进展同步）
  └─ meeting-notes-organizer（周会 / 日会 → 上下文更新）

个人成长
  └─ meeting-coach（会议表现 → 行为复盘 + 改进话术）

AI 产品设计
  └─ ai-pm-prd-builder（产品想法 → 节点流/契约/选型/评测 → AI 产品 PRD）
```

`_shared/workflow-rules.md` 是公共底座，统一处理：

- Claude / Codex 的结构化确认兼容
- 多项目识别
- 最小上下文读取
- 项目记忆更新
- `meeting-coach` 和项目工作流的边界

---

## 安装方式

### Claude Code

```bash
git clone https://github.com/samlaying/pm-skills.git /tmp/pm-skills
mkdir -p .claude/skills
rsync -a --delete --exclude ".git" --exclude "README.md" /tmp/pm-skills/ .claude/skills/
rm -rf /tmp/pm-skills
```

在项目的 `CLAUDE.md` 里加入路由说明：

```markdown
## Agent skills

本仓库的本地 skills 放在 `.claude/skills/`。

| Skill | 什么时候用 |
|-------|------------|
| `project-context-maintainer` | 维护项目背景、术语、决策 |
| `meeting-notes-organizer` | 处理会议材料、提取 todo |
| `task-arrangement-planner` | 领导安排任务后拆解推进 |
| `prd-writer` | 评审前写 PRD |
| `prd-review-handler` | 评审后处理反馈 |
| `update-writer` | 写汇报/通知文档 |
| `meeting-coach` | 复盘会议中的个人沟通表现 |
| `ai-pm-prd-builder` | 设计 AI/大模型产品，写 AI 产品 PRD |
```

### Codex

```bash
git clone https://github.com/samlaying/pm-skills.git /tmp/pm-skills
mkdir -p .agents/skills
rsync -a --delete --exclude ".git" --exclude "README.md" /tmp/pm-skills/ .agents/skills/
rm -rf /tmp/pm-skills
```

在项目的 `AGENTS.md` 里加入同样的路由说明，并把路径写成 `.agents/skills/`。

### 同时支持 Claude Code 和 Codex

```bash
git clone https://github.com/samlaying/pm-skills.git /tmp/pm-skills
mkdir -p .claude/skills .agents/skills
rsync -a --delete --exclude ".git" --exclude "README.md" /tmp/pm-skills/ .claude/skills/
rsync -a --delete --exclude ".git" --exclude "README.md" /tmp/pm-skills/ .agents/skills/
rm -rf /tmp/pm-skills
```

---

## 项目目录结构

skills 默认识别包含 `项目上下文.md` 的目录为项目根目录；下面是推荐的 Obsidian 项目结构：

```text
项目目录/
├── 项目上下文.md          # 项目核心记忆：为什么做、做什么、卡在哪
├── 内部术语表.md          # 项目特有概念
├── 项目工作记录.md        # 时间线流水
├── 任务.md               # 可执行任务汇总
├── 技术细节.md            # 技术/流程决策记录（按需）
├── 会议纪要/
│   └── YYYY-MM-DD 类型-对象-主题.md
└── 需求点/
    └── 需求点01-功能名/
        ├── 00-对齐记录.md
        ├── 01-理解.md
        ├── 01b-上线对齐.md
        ├── 10-过程记录.md
        ├── 100-成品.md
        └── 500-复盘.md
```

`meeting-coach` 默认不写入项目工作流；只有用户明确要求保存个人复盘时，再放到项目或个人指定目录。

---

## 依赖

| 依赖 | 用途 | 是否必须 |
|------|------|----------|
| Claude Code 或 Codex | skill 运行环境 | 必须 |
| `lark-cli` | 飞书文档上传、读取评论、同步文档 | 仅 `prd-writer`、`prd-review-handler`、`update-writer` 需要 |
| Obsidian | 本地文档管理 | 推荐，非必须 |

---

## 使用示例

### 处理会议材料

```text
你：帮我处理一下这个会议录音

agent：我识别到这是一个需求评审会议，涉及「搜索优化」需求点。
       文件名建议：2026-06-10 需求评审-搜索优化.md
       处理模式：只记录 / 处理？
```

### 写 PRD

```text
你：基于这个会议纪要帮我整理成评审前 PRD

agent：我会先读取项目上下文和术语表，再按 PRD 写作流程生成 Happy Path、
       异常场景和待确认项。需要确认本次是独立项目还是现有项目下的需求点。
```

### 评审后处理反馈

```text
你：评审完了，帮我处理飞书评论并补验收标准

agent：我会先拉取最新评论和飞书最新版，和本地 PRD 对比后生成反馈处理清单，
       再按确认后的流程补验收标准。
```

### 复盘会议表现

```text
你：帮我复盘一下这个会议我的表现

agent：我会从个人行为证据出发，按沟通表达、业务理解、批判性思维等维度给出反馈。
```

---

## 维护说明

- `_shared/` 是公共规则目录，不要单独删除。
- 不要把 `.zip`、`.png`、`.xml`、`.DS_Store` 等运行产物提交到 skill 仓库。
- 长参考文件顶部保留目录，方便 agent 按需读取。
- 如果只分发单个 skill，需要同时带上 `_shared/`，否则公共规则引用会断。

---

## License

MIT
