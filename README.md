# PM Skills — Claude Code 产品经理工作流 Skill 集

一套基于 Claude Code 的产品经理工作流 skill，覆盖从需求到交付的全流程。

## Skills 一览

| Skill | 用途 | 主要产出 |
|-------|------|---------|
| `project-context-maintainer` | 维护项目背景、内部术语、关键决策、需求点层级、工作记录 | `项目上下文.md`、`内部术语表.md`、`项目工作记录.md` |
| `meeting-notes-organizer` | 处理会议材料（妙记转写、笔记、口述），按项目归档，按类型生成产物 | 会议记录、todo、对齐记录、技术细节 |
| `task-arrangement-planner` | 领导安排任务后，拆解信息缺口、推进节奏、沟通话术 | 任务安排、工作节奏、待补信息、下一步行动 |
| `prd-writer` | 评审前写 PRD，从材料提取到结构化文档到飞书上传 | V3.0 PRD、Happy Path、异常流程、飞书链接 |
| `prd-review-handler` | PRD 评审后处理：拉评论、对比最新版、处理反馈、写验收标准、回写飞书 | 反馈处理记录、修订版 PRD、验收标准 |
| `update-writer` | 汇报/通知/进展同步文档，读上下文后生成结构化文档上传飞书 | 汇报文档、通知文档、飞书链接 |

## 工作流全景

```
项目启动
  └─ project-context-maintainer（建立项目记忆）

需求阶段
  ├─ meeting-notes-organizer（会议材料 → 会议纪要 + todo）
  ├─ task-arrangement-planner（领导安排 → 推进计划）
  └─ prd-writer（材料 → 评审前 PRD → 飞书）

评审阶段
  └─ prd-review-handler（评审反馈 → 修订 PRD → 验收标准）

日常同步
  ├─ update-writer（汇报/通知/进展同步 → 飞书）
  └─ meeting-notes-organizer（周会/日会 → 上下文更新）
```

## 安装

将需要的 skill 目录复制到你的项目的 `.claude/skills/` 下：

```bash
# 全部安装
cp -r pm-skills/* your-project/.claude/skills/

# 按需安装
cp -r pm-skills/prd-writer your-project/.claude/skills/
cp -r pm-skills/meeting-notes-organizer your-project/.claude/skills/
```

然后在项目的 `CLAUDE.md` 中注册 skill 路由：

```markdown
## Agent skills

| Skill | 什么时候用 |
|-------|-----------|
| `prd-writer` | 评审前写 PRD |
| `meeting-notes-organizer` | 处理会议材料 |
| `update-writer` | 汇报/通知文档 |
| ... | ... |
```

## 依赖

- **Claude Code** — skill 运行环境
- **lark-cli** — 飞书文档上传（`prd-writer`、`prd-review-handler`、`update-writer` 需要）
- **Obsidian** — 本地文档管理（推荐，非必须）

## 项目目录结构

skill 按以下结构管理项目文件：

```
100-项目名/
├── 项目上下文.md          # 项目核心记忆
├── 内部术语表.md          # 项目特有概念
├── 项目工作记录.md        # 时间线流水
├── 任务.md               # 可执行任务汇总
├── 技术细节.md            # 技术/流程决策记录
├── 会议纪要/
│   └── YYYYMMDD 类型-主题.md
└── 需求点/
    └── 需求点01-功能名/
        ├── 00-对齐记录.md    # MT 沟通记录
        ├── 01-理解.md        # 需求理解与行动
        ├── 01b-上线对齐.md   # 跨部门上线对齐
        ├── 10-过程记录.md    # 过程流水
        ├── 100-成品.md       # 最终产出
        └── 500-复盘.md       # 复盘
```

## License

MIT
