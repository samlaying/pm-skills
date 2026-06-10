# PM Skills — Claude Code 产品经理工作流 Skill 集

一套基于 Claude Code 的产品经理工作流 skill，覆盖从需求到交付的全流程。

---

## 🚀 一句话安装

把下面这句话发给你的 Claude Code agent：

> **帮我把 https://github.com/samlaying/pm-skills 这个仓库的 skills 安装到当前项目的 .claude/skills/ 下，然后在 CLAUDE.md 里注册路由。**

完事。agent 会自己 clone、复制、注册。

---

## 📦 这套 skills 能干嘛

### 一句话概括

**会议录音 → 会议纪要 + 任务拆解 + PRD + 飞书文档 + 行为复盘**，产品经理的全流程自动化。

### 详细说明

| Skill | 触发时机（你对 agent 说） | 它帮你做什么 | 产出物 |
|-------|--------------------------|-------------|--------|
| `project-context-maintainer` | "帮我维护一下XX项目的上下文" | 建立和维护项目记忆：背景、术语、决策、需求点层级 | `项目上下文.md`<br>`内部术语表.md`<br>`项目工作记录.md` |
| `meeting-notes-organizer` | "帮我处理一下这个会议录音" / "记录一下" | 按项目归档会议材料，区分会议类型（需求评审/MT沟通/周会/跨部门/日会），提取行动项和待确认问题 | 会议记录<br>需求点文件夹<br>todo 列表<br>技术细节文档 |
| `meeting-coach` | "帮我复盘一下这个会议我的表现" | 用 7 条文化价值观 + 5 项软实力评估你的行为，给出具体改进话术 | 行为复盘报告<br>改进话术<br>行动清单 |
| `task-arrangement-planner` | "领导安排了一个活，帮我拆一下" | 分析还缺什么信息、怎么推进、怎么排节奏、怎么跟领导沟通。简单任务快速出结果，复杂任务走五步框架 | 任务安排<br>工作节奏<br>待补信息<br>沟通话术 |
| `prd-writer` | "帮我写 PRD" / "整理成需求文档" | 从会议录音/材料提取需求，生成评审前 PRD，上传飞书 | V3.0 PRD<br>Happy Path<br>异常流程<br>飞书链接 |
| `prd-review-handler` | "评审完了，帮我处理反馈" | 拉飞书评论、对比最新版、处理评审意见、写验收标准、回写飞书 | 反馈处理记录<br>修订版 PRD<br>验收标准<br>飞书同步结果 |
| `update-writer` | "帮我写个汇报" / "写个通知发出去" | 读取项目上下文，生成结构化汇报/通知文档，上传飞书 | 汇报文档<br>通知文档<br>飞书链接 |

---

## 🔄 工作流全景

```
项目启动
  └─ project-context-maintainer（建立项目记忆）

需求阶段
  ├─ meeting-notes-organizer（会议材料 → 会议纪要 + todo）
  ├─ meeting-coach（会议录音 → 行为复盘 + 改进话术）
  ├─ task-arrangement-planner（领导安排 → 推进计划）
  └─ prd-writer（材料 → 评审前 PRD → 飞书）

评审阶段
  └─ prd-review-handler（评审反馈 → 修订 PRD → 验收标准）

日常同步
  ├─ update-writer（汇报/通知/进展同步 → 飞书）
  └─ meeting-notes-organizer（周会/日会 → 上下文更新）
```

---

## 🛠️ 安装方式

### 方式一：让 agent 自动安装（推荐）

对你的 Claude Code agent 说：

```
帮我把 https://github.com/samlaying/pm-skills 这个仓库的 skills 安装到当前项目的 .claude/skills/ 下，然后在 CLAUDE.md 里注册路由。
```

### 方式二：手动安装

```bash
# 1. clone 仓库
git clone https://github.com/samlaying/pm-skills.git /tmp/pm-skills

# 2. 全部安装
cp -r /tmp/pm-skills/* your-project/.claude/skills/

# 3. 或者按需安装（只装你需要的）
cp -r /tmp/pm-skills/prd-writer your-project/.claude/skills/
cp -r /tmp/pm-skills/meeting-notes-organizer your-project/.claude/skills/
cp -r /tmp/pm-skills/meeting-coach your-project/.claude/skills/

# 4. 清理
rm -rf /tmp/pm-skills
```

### 安装后：注册路由

在项目的 `CLAUDE.md` 中添加：

```markdown
## Agent skills

本仓库的本地 skills 放在 `.claude/skills/`。

| Skill | 什么时候用 |
|-------|-----------|
| `project-context-maintainer` | 维护项目背景、术语、决策 |
| `meeting-notes-organizer` | 处理会议材料、提取 todo |
| `meeting-coach` | 复盘会议中的沟通表现 |
| `task-arrangement-planner` | 领导安排任务后拆解推进 |
| `prd-writer` | 评审前写 PRD |
| `prd-review-handler` | 评审后处理反馈 |
| `update-writer` | 写汇报/通知文档 |
```

---

## 📁 项目目录结构

skill 按以下结构管理项目文件：

```
100-项目名/
├── 项目上下文.md          # 项目核心记忆（为什么做、做什么、卡在哪）
├── 内部术语表.md          # 项目特有概念（实习生光看资料能否理解）
├── 项目工作记录.md        # 时间线流水（什么时间做了什么）
├── 任务.md               # 可执行任务汇总（Tasks 插件可查询）
├── 技术细节.md            # 技术/流程决策记录
├── 会议纪要/
│   └── YYYYMMDD 类型-对象-主题.md
├── 行为复盘/
│   └── YYYYMMDD 会议类型.md    # meeting-coach 产出
└── 需求点/
    └── 需求点01-功能名/
        ├── 00-对齐记录.md    # MT 沟通记录
        ├── 01-理解.md        # 需求理解与行动
        ├── 01b-上线对齐.md   # 跨部门上线对齐
        ├── 10-过程记录.md    # 过程流水
        ├── 100-成品.md       # 最终产出
        └── 500-复盘.md       # 复盘
```

---

## ⚙️ 依赖

| 依赖 | 用途 | 是否必须 |
|------|------|---------|
| [Claude Code](https://claude.ai/code) | skill 运行环境 | ✅ 必须 |
| [lark-cli](https://github.com/nicholasxuu/lark-cli) | 飞书文档上传/读取 | 仅 `prd-writer`、`prd-review-handler`、`update-writer` 需要 |
| [Obsidian](https://obsidian.md/) | 本地文档管理 | 推荐，非必须 |

---

## 💡 使用示例

### 场景 1：处理会议录音

```
你：帮我处理一下这个会议录音
[贴入飞书妙记转写文本]

agent：我识别到这是一个需求评审会议，涉及"搜索优化"需求点。
       文件名：20260610 需求评审-搜索优化.md → OK？
       处理模式：只记录 / 处理？

你：处理

agent：[生成会议记录 + 需求点文件夹 + 行动项 + 任务.md 更新]
```

### 场景 2：复盘会议表现

```
你：帮我复盘一下这个会议我的表现
[贴入会议转写]

agent：会议类型：客户会议，你的角色：汇报者。
       重点复盘哪些维度？不选则全部评估。

你：沟通表达、批判性思维

agent：[生成行为复盘报告，包含正向行为、待改进行为、具体话术、行动清单]
```

### 场景 3：领导安排任务

```
你：领导说"这个月底前要把新版搜索上线，你负责跟各方协调"

agent：这是一个复杂任务（多方利益、有截止时间），我用五步框架帮你拆。
       先确认一下：领导原话还说了什么？有没有已知的约束？

你：[补充信息]

agent：[生成任务安排：利益相关方、动作组合、资源盘点、求助清单、迭代计划]
```

---

## 📄 License

MIT
