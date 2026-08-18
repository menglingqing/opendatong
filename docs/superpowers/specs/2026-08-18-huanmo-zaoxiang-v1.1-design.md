# 幻墨造像 v1.1 · 知识治理机制落地 设计文档

- 日期：2026-08-18
- 状态：待批准
- 前置：v1.0 设计（2026-08-17-huanmo-zaoxiang-design.md）已实施并推送
- 涉及仓库：`menglingqing/knowledge-os`（主要）、`menglingqing/opendatong`（core.md 升级）

## 1. 背景与目标

v1.0 部署后，经两轮外部评审（OS/Persona 分层 critique、GitHub 知识管理 critique），确认四个待吸收机制：知识晋升链路、最小 frontmatter、双日志、心跳自动化定义。本版本将它们装进现有 `docs/image-prompt-engineering/` 结构——**取机制、弃布局**，不改仓库骨架。

同时 core.md 升 v1.1，吸收两条人格强化："视觉导演"定位与"创意激进、执行保守"信条。

## 2. 变更清单

### knowledge-os 侧

**新增 3 个文件：**

```
docs/image-prompt-engineering/
├── governance.md           # 知识治理：晋升链路 + frontmatter 约定 + 心跳定义 + 双日志
├── experiments/
│   └── README.md           # 实验区说明（暂为空，不虚构实验）
└── ledger/
    └── learning-log.md     # 认知历史日志（首批两条：v1.0、v1.1）
```

**修改 4 个文件：**

- `methodology/` 三篇：头部注入 frontmatter `status: validated` + evidence 链接指向 64卦案例
- `README.md`：版本 v1.0 → v1.1，新增 governance/experiments/ledger 三个入口链接

### opendatong 侧

**修改 3 个文件：**

- `agents/huanmo-zaoxiang/core.md`：身份段加"视觉导演"定位；原则新增第 6 条"创意上激进，执行上保守"；版本头 v1.1
- `agents/huanmo-zaoxiang/README.md`：版本引用 v1.0 → v1.1
- `agents/huanmo-zaoxiang/adapters/opendatong-citizen.md`：知识版本引用 v1.0 → v1.1

## 3. 关键设计决策

1. **frontmatter 最小集**：只有 `status`（experimental/validated）+ `evidence`（案例链接列表）。不采纳 confidence / evidence_count / last_verified——evidence 链接本身就是计数，日期由 git 管理，没人维护的元数据会谎报权威。
2. **晋升规则量化**：experimental → validated 需 ≥3 个独立案例验证。写入 governance.md。
3. **权力分离**：Agent 提议知识晋升（diff/PR 形式），人类建筑师批准合并。当前单人仓库，PR 流程在多贡献者出现时启用；现阶段核心机制是 status 字段 + learning-log。
4. **心跳不入 prompt**：Knowledge Review Pipeline 定义为自动化任务（收集近期案例 → 找规律与冲突 → 生成晋升建议供人 review），不写入 core.md 或任何 agent 定义。
5. **core.md 轻量约束不变**：v1.1 正文 ≤ 1200 字符（v1.0 为 545）。
6. **版本同步**：knowledge 领域版本与 agent 版本同步升到 v1.1，两仓库同日提交。

## 4. learning-log.md 首批内容

```markdown
# 极简反馈日志 · Learning Log

认知历史：Agent 学会了什么。每条 ≤50 字核心经验。

## 2026-08-17 · v1.0
64卦案例：关系先于元素；用文字预算控制注意力；模型弱点用构图掩盖。

## 2026-08-18 · v1.1
知识分 experimental/validated；Agent 提议晋升、人类批准；心跳属于自动化而非 prompt。
```

## 5. 验证方式

1. governance.md 存在且含晋升链路、frontmatter 约定、心跳定义三节
2. 三篇方法论 frontmatter 注入成功且正文未被改动（diff 只加头部）
3. core.md v1.1 ≤ 1200 字符、含第 6 条原则、版本号一致
4. 两仓库版本引用全部为 v1.0 → v1.1，无遗漏（grep "v1.0" 应只剩历史说明性文字）
5. 链接有效性、git status 干净、分别 push

## 6. 明确不做

- 不建 ChatGPT 提议的仓库根级目录树（core/ visual/ models/ experiments/ ledger/ archive/）
- 不改案例库分类轴（保持按项目分，不按成败分）
- 不实现真实 cron/PR 自动化（只定义机制；实现留给需要时）
- 不虚构实验条目填充 experiments/
