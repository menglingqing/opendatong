# 幻墨造像（Huanmo Zaoxiang）生图大师 Agent · 设计文档

- 日期：2026-08-17
- 状态：已批准（方案 B：核心定义 + 三适配层，轻量化 core）
- 涉及仓库：`menglingqing/opendatong`（agent 本体）、`menglingqing/knowledge-os`（知识管理）

## 1. 背景与目标

创建名为「幻墨造像」的生图大师 agent，职责是帮助用户输出高质量的生图提示词（image prompt），并支持基于生成结果的诊断式迭代。

- agent 本体以**纯提示词定义文档**形态存在（无代码、无构建步骤），管理在 opendatong 仓库。
- 方法论知识以 markdown 长文形态管理在 knowledge-os 仓库。
- 种子知识来源于 2026-08-17 的「64卦能量天门」提示词迭代案例（v1→v6 共六轮）。

### 使用场景（三类，全部支持）

1. Claude Code 内作为 subagent 调用
2. 复制 core.md 全文粘贴到任意 LLM 作为 system prompt
3. 作为 opendatong 数字文明的第一位 agent 居民

## 2. 总体架构

**分工原则**：knowledge-os 是知识的完整栖息地（可长、可碎、可演进）；opendatong 是 agent 的居住地（自包含、可运行）。

### opendatong 侧（agent 本体）

```
agents/
└── huanmo-zaoxiang/                  # 幻墨造像
    ├── README.md                     # 居民名片：一句话职责、如何使用、知识版本
    ├── core.md                       # ★ 核心定义（轻量）：身份 + 方法论指针 + 最小工作原则
    └── adapters/
        ├── claude-code.md            # Claude Code subagent 格式（frontmatter + 指向 core.md）
        └── opendatong-citizen.md     # 文明居民身份卡（对齐 opendatong 本体概念）
```

### knowledge-os 侧（知识库）

```
docs/
└── image-prompt-engineering/         # 生图提示词工程领域
    ├── README.md                     # 领域索引：方法论 + 案例清单
    ├── methodology/
    │   ├── seven-layer-architecture.md   # 7层架构拆解法
    │   ├── iteration-playbook.md         # 诊断式修改 + 抽卡验收 + 文字预算审计
    │   └── model-adaptation.md           # 中文模型 vs MJ/SDXL、负面词归位、画幅
    └── cases/
        └── 64-hexagram-gate/             # 种子案例
            ├── README.md                 # 案例摘要 + 迭代路径总览
            ├── v1-original.md            # 各版本完整提示词 + 每轮改动说明
            ├── ...                       # v2 ~ v5
            ├── v6-final.md
            └── final-prompts.md          # v6 中英文终稿 + 负向词 + 使用提示
```

### 明确不做的事（YAGNI）

- 不引入 git submodule / subtree
- 不写构建脚本、不做自动拼装
- core.md 不内嵌完整工作流、字数控制规则、固定输出契约——这些留给后续封装 skill 时设计

## 3. core.md 设计（轻量核心）

core.md 只做三件事，预计一两百字级别：

1. **身份与职责边界**：幻墨造像是生图提示词架构师。负责需求拆解、提示词输出、迭代诊断；不越界（不执行生图、不评论美术史、不处理无关话题）。
2. **方法论指针**：声明遵循 knowledge-os `image-prompt-engineering` 领域知识，标注知识版本号（如 `knowledge: image-prompt-engineering v1.0`）。
3. **最小工作原则**（3~5 条，只点方向不展开）：
   - 关系先于元素
   - 结构优先于细节
   - 诊断迭代只改一个变量
   - 否定词归负向框
   - 按目标模型决定中英文与标签化程度

**断网可用性**：core.md 不依赖抓取 knowledge-os 即可独立成立；知识库链接仅为延伸阅读。

## 4. 适配层设计（薄壳）

### adapters/claude-code.md

- Claude Code subagent 标准格式：YAML frontmatter（`name`、`description`、`tools`）+ 正文一句话指向 core.md。
- **不内嵌方法论**，避免与 core.md 双写不同步。

### adapters/opendatong-citizen.md

对齐 opendatong 本体概念（Agent / Identity / Reputation / Governance），定义：

- 身份：幻墨造像，数字文明第一位居民
- 职责：为文明居民与人类参与者生成视觉提示词
- 服务接口：接收视觉需求描述 → 返回结构化提示词
- 知识来源声明：knowledge-os image-prompt-engineering 领域

## 5. knowledge-os 种子内容

内容从 2026-08-17 对话整理，不新增创作：

- **三篇方法论长文**：知识库不受字数预算约束，可详细；为后续 skill 封装提供素材池。
- **64卦案例完整版本链**：v1 原稿 → v6 终稿，每版附改动说明与对应 critique 要点。

## 6. 同步纪律

- **同步方向单向**：knowledge-os → core.md。
- core.md 头部记录知识版本号；知识库更新后，人工决定是否提炼进 core.md 并升版本号。
- 文件名使用小写 kebab-case（新目录为活文档风格，区别于 docs/ 下既有全大写文件）。

## 7. 验证方式（文档型项目，无代码测试）

1. 文件齐全且互相引用有效（链接路径正确）
2. core.md 粘贴到任意 LLM 能独立成立（断网可用性）
3. 64卦案例版本链完整可追溯（v1→v6 每版有改动说明）

## 8. 提交方式

- 两个仓库分别 commit & push，commit message 遵循各自仓库惯例（英文/中文均可，描述性）。
- 本设计文档存放于 opendatong `docs/superpowers/specs/`。
