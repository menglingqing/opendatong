# 幻墨造像（Huanmo Zaoxiang）生图大师 Agent · 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 opendatong 创建「幻墨造像」agent（core + 两个 adapters + README），在 knowledge-os 创建 `image-prompt-engineering` 知识库（3 篇方法论 + 64卦案例 v1→v6 完整版本链）。

**Architecture:** 纯文档项目，无代码无构建。opendatong 侧为轻量 agent 定义（core.md 只做身份+指针+原则），knowledge-os 侧为完整方法论与案例库。同步方向单向：knowledge-os → core.md，靠版本号对齐。

**Tech Stack:** Markdown、git、两个本地克隆仓库（`~/Desktop/opendatong`、`~/Desktop/knowledge-os`）。

**设计依据:** `opendatong/docs/superpowers/specs/2026-08-17-huanmo-zaoxiang-design.md`（已批准）

## Global Constraints

- 两个仓库的 git 身份：`menglingqing <1136586419@qq.com>`（opendatong 已配置 local config；knowledge-os 需在首次 commit 前同样配置 local config，不要改 global）
- commit message 风格：`docs: 中文描述`（两仓库现行惯例），附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- 新文件名一律小写 kebab-case
- core.md 保持轻量（≤200 字正文），不得内嵌工作流细节、输出契约、字数控制规则——这些留给未来 skill 封装
- 文档内容为本次对话的整理，不新增创作（v6 终稿除外——v6 只有增量修订，终稿需按本计划 Task 3 的合并结果落盘）
- 所有文件内容为 UTF-8 中文为主，提示词正文保留中英双语

---

### Task 1: knowledge-os · 领域索引 + 方法论三篇

**Files:**
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/seven-layer-architecture.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/iteration-playbook.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/model-adaptation.md`

**Interfaces:**
- Produces: 目录 `docs/image-prompt-engineering/`（Task 2 的案例库放入其 `cases/` 子目录；opendatong core.md 引用路径 `docs/image-prompt-engineering/` 与版本号 `v1.0`）

- [ ] **Step 1: 写领域索引 README.md**

内容：

````markdown
# 生图提示词工程 · Image Prompt Engineering

面向图像生成模型（即梦 / 可灵 / Seedream / Midjourney / SDXL）的提示词设计方法论与案例库。

核心命题：**提示词写得好不好，不是文笔问题，是系统设计能力的外化。**

## 方法论

- [7 层架构拆解法](methodology/seven-layer-architecture.md)——从"元素清单"到"关系网络"的结构化拆解
- [迭代手册：诊断、验收与预算](methodology/iteration-playbook.md)——只改一个变量的诊断法、验收分级、文字预算审计
- [模型适配](methodology/model-adaptation.md)——中文模型 vs MJ/SDXL、否定词归位、画幅、权重语法

## 案例库

- [64卦能量天门](cases/64-hexagram-gate/)——六轮迭代完整版本链（v1→v6），本领域种子案例

版本：v1.0 · 2026-08-17
````

- [ ] **Step 2: 写 seven-layer-architecture.md**

内容：

````markdown
# 7 层架构拆解法

把一个生图需求从"元素清单"拆解为"关系网络"的七层框架。源自 64卦能量天门案例的六轮迭代。

## 七层定义

| 层级 | 核心要素 | 关键原则 |
|------|---------|---------|
| L1 概念层 | 一句话抽象概念 | 概念必须可被"翻译"成视觉关系，而不是世界观口号。例："秩序拥有了天体尺度"比"东方易经宇宙神域"更可执行 |
| L2 主体层 | 谁是主体、什么关系 | 优先定义"复合主体"而非多主体竞争。例：龙与天门不是第一/第二主体，而是"龙首为焦点、环体为结构延伸"的复合巨构 |
| L3 空间层 | 纵深、遮挡、尺度 | 巨物感靠遮挡、裁切和尺度锚点，不靠尺寸词；所有物体分布于不同纵深，互不贴于同一平面 |
| L4 构图层 | 画幅、地平线、视觉动线 | 关系准确，构图不要几何准确（破对称）；极低地平线比"占比 10-15%"有效；透视椭圆让圆环从 Logo 变成空间巨构 |
| L5 光影层 | 主光源、衰减、藏与露 | 单一主光源 + 亮度随距离快速衰减；巨物感来自看不清全貌（远离光源的一侧沉入阴影） |
| L6 材质层 | 质感排序 | 材质描述给优先级而非罗列。例：真实鳞片 > 玉质光泽 > 局部半透明（防玻璃龙） |
| L7 色彩层 | 冷暖比、过渡轴 | 色彩极少，靠明度与冷暖完成层次；指定过渡方向（垂直/径向）而非罗列颜色 |

## 使用方式

1. 接到需求后，先逐层填写各层的"关系定义"（每层一两句），再写提示词正文。
2. 提示词正文的段落顺序按"对画面成败的影响"排，不必按 L1→L7 排。7 层是人的检查清单，不是模型的注意力顺序。
3. 模型的注意力控制靠三件套：**词序**（重要的在前）、**文字预算**（字数占比≈视觉权重）、**权重语法**（MJ `::`、SD `(...:1.2)`）。

## 反面教训（来自 v1 原稿）

- 7 层写成"美术设定说明书"：说服甲方的文案（"正因为不完整，才更显其无边无际"）模型不需要。
- 层内过度精确：要求 64 卦逐卦可读、爪趾逐根可数——模型只会生成"假装精确的乱码"。正确做法是降精度 + 用构图掩盖（见 iteration-playbook.md）。
````

- [ ] **Step 3: 写 iteration-playbook.md**

内容：

````markdown
# 迭代手册：诊断、验收与预算

生图不是一次成稿，是"抽卡 → 验收 → 诊断 → 单变量修改"的循环。本手册定义这个循环的操作规范。

## 1. 验收分级（结构 > 细节）

出图后按优先级从高到低验收，高层不成立则低层无意义：

1. 尺度关系成立（如：龙 > 环 > 宫）
2. 构图骨架成立（如：透视椭圆、低地平线）
3. 关键接触/遮挡成立（如：爪与环真实接触）
4. 焦点唯一且正确（如：龙首最亮）
5. 其余细节（加分项，不作为重抽理由）

原则：**尺度关系是第一位的，细节是第二位的。** 先挑"结构成立"的抽卡结果，再在其上微调。

## 2. 诊断式修改：只改一个变量

每次修改定位单一原因，改一处。多点同时改动无法归因，等于没改。

常见问题 → 单一变量干预对照表（64卦案例实证）：

| 问题 | 只改一个变量 |
|------|-------------|
| 主体不够大、参照物太大 | 加强参照物的"渺小"措辞，或前置尺度段 |
| 能量体被画成实体（玉盘/罗盘） | 把"不是玉盘/实体建筑"挪到开头第一句之后 |
| 次元素抢主体 | 在次元素前加"克制的、面积不大的"类限定 |
| 某部件消失/被藏 | 把该部件的存在声明挪到主体段句首 |
| 某部件抢戏 | 加重"亮度与视觉权重低于主焦点"，负向加对应词 |
| 接触关系丢失（悬浮） | 把接触动词改为"牢牢压/扣住，不可悬空、不可脱离" |
| 可数符号混乱 | 不修复，用构图掩盖；必须精确则后期叠加矢量素材 |
| 材质跑偏（玻璃感） | 收紧半透明范围措辞（"几乎不透明，仅边缘极薄处"） |
| 肢体跑偏（人手/鹰脚/西式龙） | 负向加重对应词，正向补"鳞甲连续过渡"类解剖连续性 |

## 3. 文字预算审计

元素在提示词中的**字数占比**应约等于其**目标视觉权重**。模型对说得多的东西分配更多注意力——哪怕你同时写了"它不重要"。

实证：64卦案例 v5 中龙爪文字占全文 36%，但目标视觉权重仅 12-15%，超配 2.5 倍。v6 压缩至 17% 后注意力分布回归正常。

操作：写完提示词后统计各核心元素字数，与视觉权重目标对比；超配的元素用更精炼的语言重述，而不是加更多限定句。

## 4. 用构图掩盖模型弱点

模型做不到的事，不要硬要求，用构图/物理规律取消或掩盖需求：

- 卦象画不准 → 透视椭圆让爻线自然压缩变形 + **径向消隐**：近核心处卦象规整，越向外围爻线越弥散，最外圈分解为光点与星空尘埃融为一体（最难的部分干脆不画）
- 龙身细节画不全 → 半藏于影：远离光源一侧沉入深黑蓝阴影，"看不清全貌"本身就是巨物感
- 百分比构图听不懂 → 换成摄影语言："地平线压至画面最底部"

## 5. 叙事瞬间物理化

静帧画面里的"进行时"不能靠动词表达（"正要推开"画不出来），只能靠**力的痕迹**表达：

- 爪压点能量光纹泛起涟漪、局部微微形变
- 云层被巨物排开
- 碎屑/光粒的定向飞散

一条物理痕迹胜过三句叙事形容。
````

- [ ] **Step 4: 写 model-adaptation.md**

内容：

````markdown
# 模型适配

同一创意在不同模型上需要不同形态的提示词。

## 1. 中文模型（即梦 / 可灵 / Seedream）

- 能吃中文语义长句，结构化段落有效。
- 正文中可少量使用否定（"不是玉盘"），但主要否定仍应放负向框。
- 对长文本耐受较好，但仍建议 600-900 字以内，核心关系前置。

## 2. Midjourney / SDXL

- 转英文，标签化压缩，句子短而实。
- **否定词禁止进正文**："not a human hand" 反而提高人手出现率。否定一律进 `--no` 参数或负向提示词框。
- 权重语法：MJ 用 `keyword::2`，SD 用 `(keyword:1.2)`。

## 3. 画幅先定

画幅是构图的一部分，必须最先确定。纵向叙事（下→上的层级推进）用竖构图 2:3 或 9:16；横向场面用 16:9。画幅错了，构图描述再细也展不开。

## 4. 精确可数特征：语义锚点，不是验收标准

- "64 卦""五爪"这类精确数量要求，模型必然画不准（4 根或 6 根爪趾都正常）。
- 正确用法：当语义锚点用（"五爪"把模型推向中国帝王龙原型而非西方龙），不当验收标准。
- 必须精确的元素（如真正的 64 卦序），出图后用设计软件叠加矢量素材，比让模型硬画靠谱。

## 5. 出图后修复优先级

1. 结构成立但局部失败（如爪-环接触区融合错误）→ **局部重绘 / inpainting**，不要整图重抽
2. 焦点混乱、尺度错误 → 整图重抽（结构性问题局部救不回）
3. 精细符号（卦象）→ 后期叠加
````

- [ ] **Step 5: 验证**

Run: `ls ~/Desktop/knowledge-os/docs/image-prompt-engineering/ ~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/`
Expected: README.md 与三篇方法论均存在

Run: `cd ~/Desktop/knowledge-os && grep -l "7 层架构" docs/image-prompt-engineering/README.md && grep -c "文字预算" docs/image-prompt-engineering/methodology/iteration-playbook.md`
Expected: README 链接目标存在；iteration-playbook 含"文字预算"

- [ ] **Step 6: 配置 git 身份并提交**

```bash
cd ~/Desktop/knowledge-os
git config user.name "menglingqing"
git config user.email "1136586419@qq.com"
git add docs/image-prompt-engineering/
git commit -m "docs: 新增生图提示词工程领域——领域索引与三篇方法论

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: knowledge-os · 64卦案例库上半（README + v1~v3）

**Files:**
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/README.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v1-original.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v2-compressed.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v3-composite-megastructure.md`

**Interfaces:**
- Consumes: Task 1 的目录结构
- Produces: 案例目录 `cases/64-hexagram-gate/`（Task 3 继续补 v4~v6 与终稿）

- [ ] **Step 1: 写案例 README.md**

内容：

````markdown
# 案例：64卦能量天门

> 东方易经 × 宇宙神域 × 巨构文明：天体神龙盘绕能量态 64 卦天门，底部东方天宫为尺度锚点。

本案例是 image-prompt-engineering 领域的种子案例，完整记录了从"美术设定说明书"到"生产可用提示词"的六轮迭代（2026-08-17，单日完成）。

## 迭代路径

| 版本 | 名称 | 一句话 |
|------|------|--------|
| [v1](v1-original.md) | 灵感爆炸版 | 2000+ 字美术设定说明书：方案 9 分，提示词工程 5 分 |
| [v2](v2-compressed.md) | 结构修正版 | 砍到 ~780 字：能量体声明、视觉优先级、单主光源、负向词归位、补画幅 |
| [v3](v3-composite-megastructure.md) | 复合巨构版 | 龙-天门复合巨构、透视椭圆、极低地平线、显式遮挡、光源衰减、材质排序、象牙金白 |
| [v4](v4-claw-functional.md) | 补完四肢版 | 龙爪职能化：识别 + 构图 + 叙事三重职能，解决"无肢蛇形龙" |
| [v5](v5-claw-precision.md) | 爪构图精确化 | 爪升级为构图节点：掌压→趾扣→尖越三步动作拆解、三角视觉骨架、抢戏防火墙 |
| [v6](v6-final.md) | 终稿 | 爪文字预算压缩（36%→17%）+ 卦环径向消隐（秩序从核心生长、在尺度尽头消散）+ 叙事瞬间物理化 |

[终稿全文（中英双语 + 负向词 + 使用提示）→](final-prompts.md)

## 核心教训

1. 提示词写得好不好，不是文笔问题，是系统设计能力的外化。
2. 巨物感不靠尺寸词，靠遮挡、裁切和尺度锚点。
3. 模型做不到的事不要硬要求——用构图和物理规律取消需求（椭圆透视、径向消隐、半藏于影）。
4. 元素的字数占比 ≈ 它获得的注意力。文字预算要和视觉权重匹配。
5. 每轮迭代只改一个变量，验收永远结构优先于细节。
````

- [ ] **Step 2: 写 v1-original.md**

内容（v1 为用户原始稿，逐字收录；改动说明记录诊断）：

````markdown
# v1 · 灵感爆炸版（原始稿）

> 2026-08-17 · 起点。无负向提示词、无画幅、无英文版。

## 诊断（事后总结）

- 约 2000+ 字，注意力稀释：模型权重集中在前 1/3，色彩设计写在最后（权重最低位）
- 要求模型做不到的事：64 卦逐卦精准、百分比构图（"天宫占 10-15%"）、"突破画框"
- 内部矛盾："唯一主光源" vs 宫殿泛金光 vs 龙睛倒映；"黑色阴鱼" vs "实为暗能量"
- 方案性语言混杂："正因为不完整，才更显其无边无际"是给人看的文案
- 三个视觉中心（龙/卦环/太极核心）互相竞争，易退化为"龙绕八卦盘"游戏海报
- 天干地支、二十八星宿稀释主题纯度
- 负面要求（"无塑料感"）写在正文，反而激活相关概念
- 未指定画幅——纵向叙事用默认画幅展不开

## 原始提示词全文

8K超写实电影级画面，IMAX胶片质感，HDR高动态范围，东方易经与宇宙神域交织的超现实巨物场景，天体级神龙盘绕着一座能量态的64卦宇宙天门，底部的东方神宫只是这场神迹前渺小的尺度参照。

画面最震撼的是上半部天空中那条巨大的东方神龙——它从画面左上方盘旋而下，龙首正朝向画面中心俯冲，身体几乎占据了整个上半部天空，是绝对的巨物核心。龙并非血肉之躯，而是由冰晶、白玉、云雾和星光共同凝结而成的天体生物：龙身主体呈现温润的冰白玉质，鳞片如凝结的天光，每一片鳞片的边缘都带着强烈的银白色高光，鳞片刻着细密的云纹，在光下泛着虹彩；身体局部半透明，体内隐约可见流动的星河与光脉，仿佛整条龙就是由宇宙的光和云凝聚出的神性存在。龙须如流光般飘逸，龙角是透明的冰晶质地，龙睛是深邃的银蓝色，瞳孔中倒映着能量卦环的金色光流。龙身粗壮得惊人，一节龙躯的直径就超过了下方整座宫殿的高度，它盘绕在能量卦环之上，部分龙身突破了画面的上边缘、左边缘和右边缘，看不见首尾——正因为不完整，才更显其无边无际的天体尺度。

龙的身体盘绕着一个极其巨大的能量态圆环——这不是实体建筑，而是一座由纯能量构成的64卦宇宙天门，是天地秩序在宇宙尺度上的能量具象化。能量卦环庞大到几乎填满画面的中上部，它的上半部分被龙身压住，下半部分显露在云海之上。整个卦环没有实体材质，完全由光、能量粒子和流动的光线构成——半透明、脉动、生生不息。卦环从内向外层层铺展：最中心是太极阴阳鱼，由金白色的纯能量构成，缓缓对转，白色阳鱼与黑色阴鱼（实为极深的空间暗能量）的S形交界线泛着最强烈的金白色光流，如同宇宙的心跳，一张一翕，有节律地脉动。向外第一层是八卦环，乾兑离震巽坎艮坤八个三爻卦由金色的能量光线勾勒而成，线条并非静止，而是由无数细小的光粒子沿路径流动，阳爻是一条流动的金色光线，阴爻是两段分开的金光流，八道卦符围绕太极匀速运转。再向外是第二层、第三层……直至最外圈的64卦环，每一个六爻卦都由金色与冰蓝色交织的能量线精准构成，64卦环绕成一个完美的巨大能量圆，秩序井然，所有卦爻都在同时呼吸般地明暗交替，仿佛正在推演着天地间亿万个变化。卦环最外缘还有一圈更淡的能量光环，由天干地支和二十八星宿的光纹构成，光纹向外扩散成柔和的辉光，逐渐消融在周围的云海之中。

整个能量卦环不是扁平的，而是有厚度的立体光体——可以看到能量在环身内部流动、交织、碰撞，形成复杂的能量涡流与光丝，环的内缘明亮，外缘柔和扩散，如同一个悬浮于宇宙中的巨型能量法阵，正在运行。

圆环的中心，太极图的阴阳鱼之间，通向一片深邃的星空——漆黑的背景上镶嵌着无数细小的星辰，越往中心越深，形成一个巨大的视觉"洞口"，仿佛从易经的能量秩序深处通往无极的另一个宇宙，洞口边缘环绕着一圈明亮的金白色能量辉光，像是门正在开启。

能量卦环的下缘和两侧最为明亮，64卦爻的金色能量光与太极的金白光从环身向四周强烈扩散，将周围的云海从内部穿透、照亮，如同神迹正在开启的瞬间。圆环周围被大量翻腾的白色云海与雷云包围，云层剧烈翻涌，受到能量卦环和龙身的光照，云的向阳面泛出银白和淡金色的光辉，云的背光面则沉为冷灰色与淡紫色，云层体积感极强，明暗翻卷，气势磅礴。云海并非只在下方，而是从下方翻涌上来，缠绕在卦环的底部与两侧，甚至有几缕云丝被能量场吸向环中心的星空洞口，虚实交融。

画面的最下方，是一座非常小的东方宫殿城池——它坐落在雪白的云海大地之上，层叠的屋檐、高耸的塔楼、错落的宫阙，整体呈现金白色调，白玉为墙、琉璃为顶，飞檐翘角，精致而宏伟。但和天空中的能量卦环与神龙相比，它小得几乎像一个模型——整座城池的宽度还不及卦环厚度的三分之一，更不用说和那条天体级巨龙相比。宫殿前方的广场上，几个极其渺小的白衣人影正仰头望向天空中的神迹，他们周身被能量卦环洒下的金光笼罩，是尺度的终极参照，让整个画面的巨物感达到顶峰。

整个画面的视觉层级清晰而递进：最下方的人间/神宫（最小）→ 翻腾云海 → 巨型能量64卦天门 → 天体神龙（最大，突破画框）→ 环心深处的无边星空（无限）。每一级都在突破上一级的尺度认知。

光影冷峻而神圣：能量卦环的自发光是画面的唯一主光源——以冷调的银白、冰蓝为能量底色，卦爻与太极透出流动的金色能量辉光，金色克制但醒目，光芒穿透云层，照亮云海，向下投射到下方的宫殿屋顶上，为宫殿的飞檐镶上一圈淡淡的金边。整体光线充足但并不温暖，而是带着宇宙深空的清冷与庄严。色彩过渡从下往上如同一首肃穆的交响：底部天宫的金白 → 云海受光面的银白与淡金 → 能量卦环的冰蓝与金纹 → 神龙的银白与冰蓝 → 环心洞口的深黑与星点。径向由卦环中心向外也是层层递减的光色：太极核心的金白强光 → 八卦环的亮金 → 64卦外层的淡金与冰蓝 → 环外能量场的青白辉光 → 外围虚空的深蓝。

整个画面震撼、庄严、神圣，易经的天地秩序以纯能量形态被推到了宇宙尺度，巨物感来自连续的三级尺度跃迁——宫殿已经很大，卦环更大，龙则大到画面装不下。胶片颗粒细腻温润，能量的流动、光粒子的闪烁、冰晶的通透、云气的翻涌、星空的深邃——全部真实可触，无塑料感，无廉价光效，东方易经宇宙神域的冷峻与壮美拉满。
````

- [ ] **Step 3: 写 v2-compressed.md**

内容：

````markdown
# v2 · 结构修正版

> 2026-08-17 · 相对 v1：砍至约 780 字；核心六件事前置（龙多大、环多大、宫多小、环是能量体、谁发光、谁是第一主体）；卦象降精度；删星宿系统；负面词移入负向框；补竖构图画幅；新增英文版。

## 完整提示词（中文）

画幅：竖构图 2:3（或 9:16）

8K超写实东方奇幻电影剧照，IMAX胶片颗粒，冷峻、神圣、庄严。

核心概念：天地秩序本身凝聚成天体尺度的能量结构。64卦天门不是玉盘、铜盘或实体建筑，而是一座完全由光、能量粒子与半透明空间场构成的宇宙天门。

视觉优先级：神龙是第一视觉主体，能量天门是第二视觉主体，太极核心只是天门内部最亮的能量节点，不得压过神龙；底部天宫仅作尺度参照。

三级尺度跃迁：画面底部是一座金白色东方天宫，白玉宫阙、飞檐塔楼本身宏伟，却小如模型，广场上有几个渺小的白衣人影仰望天空；中上部悬浮着比天宫巨大数十倍的巨型能量圆环；一条比圆环更庞大的天体级东方神龙盘绕其上，龙躯突破画面顶部与左右边缘，首尾皆不可见。

构图：低机位超广角仰视，圆环居中偏上、轴线轻微倾斜；龙首从左上方斜向俯临，目光投向太极核心，但不与圆心形成对称几何构图。

能量天门：有真实空间厚度的立体光体。中心是金白太极能量核心，阴阳缓缓对转、如心脏般脉动；向外依次展开八卦内环与具有明确64分区秩序感的六爻外环——阳爻为连续金色光流，阴爻为断开的双段光流，光粒子沿爻线流动；整体呈现易经卦象的秩序感与六爻视觉语言即可，无需逐卦清晰可读。环心太极之间是极深的黑蓝星空，星辰向内延伸成深不见底的"洞口"，通往无极。

神龙：冰白玉质、半透明天光凝结、体内流动银蓝星河光脉；龙角如透明冰晶，龙须如流光失重漂浮。

光影：卦环自发光是唯一主光源。龙身靠近卦环的一侧被金白与冰蓝能量光勾勒出强烈轮廓光，远离光源的一侧逐渐沉入深黑蓝阴影，无法被一次看清全貌。白色云海从画面底部向上翻涌，穿过卦环前后形成前中后景遮挡；能量光穿透云层产生体积散射，受光面银白微金，背光面沉入冷灰蓝。

色彩：85%冰蓝、银白、深黑蓝，15%克制的金与暖白；金色只出现在太极核心、卦爻光流与少量建筑高光。由下而上递进：金白天宫→银白云海→冰蓝金纹天门→银白冰蓝神龙→深黑蓝星空。

真实体积云、物理光照、空气透视、巨物压迫感、神迹降临感。画面应像真实存在的宇宙神迹被电影摄影机捕捉，而非概念插画。

## 负向提示词

实体玉盘、金属罗盘、石质法阵、机械齿轮、赛博朋克UI、文字、符文乱码、塑料质感、廉价光效、卡通、游戏海报式正面对称构图、画面均匀发亮、过度饱和、龙完整入框、宫殿过大

## 完整提示词（英文，MJ/SDXL）

Cinematic 8K hyperrealistic eastern fantasy film still, vertical, low-angle ultra-wide shot looking up. Cosmic order itself condensed into a celestial-scale energy structure: a colossal hexagram "heavenly gate" ring made purely of light, energy particles and translucent fields — not jade, not metal, not solid architecture. Visual hierarchy: celestial eastern dragon = primary subject, energy ring = secondary, taiji core only the brightest node inside the ring, tiny golden-white heavenly palace at bottom as scale reference with minuscule white-robed figures gazing up. Three-tier scale jump: grand palace → ring dozens of times larger → dragon larger still, body breaking top and side frame edges, head and tail unseen. Dragon: ice-jade white, semi-transparent solidified light, silver-blue galaxy veins flowing within, crystal horns, drifting luminous whiskers; diving from upper left, gaze toward taiji core but off-axis, no perfect symmetry. Ring: volumetric glowing body with real thickness, pulsing golden-white taiji core, inner trigram ring and outer hexagram ring with clear 64-division order — yang lines as continuous golden light streams, yin lines as broken pairs — ordered gua-symbol language, glyphs need not be individually readable. Ring center opens into bottomless deep black-blue starfield. Sole light source is the ring: strong rim light on dragon's near side, far side sinking into deep shadow, never fully revealed. Volumetric sea of clouds surging upward, light scattering through, silver-white lit faces, cold grey-blue shadow sides. 85% ice blue / silver / deep blue, 15% restrained gold. IMAX film grain, HDR, overwhelming scale, divine revelation, captured by a cinema camera, not illustrated.

`--ar 2:3 --no text, gears, metal compass, stone altar, plastic, cartoon, symmetrical poster composition, oversaturation, evenly lit, dragon fully in frame`
````

- [ ] **Step 4: 写 v3-composite-megastructure.md**

内容：

````markdown
# v3 · 复合巨构版

> 2026-08-17 · 相对 v2：从"三个主体的关系"升级为"一个巨构的降临"。龙-天门复合巨构（龙首为焦点、环体为结构延伸）；透视椭圆替代正圆（让环从 Logo 变成空间巨构，同时掩盖卦象不准）；极低地平线替代百分比；显式前中后景遮挡；光源衰减；材质排序（真实鳞片>玉质>局部半透明，防玻璃龙）；金色改象牙金白（防土金法阵）。

## 完整提示词（中文）

画幅：竖构图 2:3

电影级超写实东方奇幻质感（非纪实摄影），IMAX胶片颗粒，冷峻、神圣。

画面主体是一个"龙—天门复合巨构"：一条天体级东方神龙与一座64卦能量天门构成不可分割的整体，龙首是视觉焦点，龙躯与环体共同组成巨构轮廓。天门不是玉盘、铜盘或实体建筑，完全由光、能量粒子与半透明空间场构成。

构图：极低地平线，天空占据绝大多数画幅；极低机位超广角仰拍，强烈近大远小透视，巨物向镜头压迫。能量天门悬浮于中上部天空，呈明显透视椭圆（非正圆、非正对镜头），轴线倾斜。龙首从左上方向下俯临，头部略侧倾，不正对镜头、不正冲椭圆中心。

空间遮挡：前景云层遮挡天门下缘；龙首位于环体前方；部分龙躯隐入环体后方与深空。所有物体分布于不同纵深，互不贴于同一平面。

三级尺度：画面最底部是一座金白色东方天宫，宫阙宏伟却小如模型，广场上有几个渺小的白衣人影仰望；天门比天宫巨大数十倍；神龙比天门更庞大，龙躯突破画面顶部与两侧边缘，首尾不可见。

能量天门：有真实厚度的立体光体，中心是暖白金太极核心，阴阳缓缓对转、明暗脉动；向外展开八卦内环与具有64分区秩序感的六爻外环，阳爻为连续光流，阴爻为断开的双段光流，光粒沿爻线流动；呈现卦象秩序感即可，无需逐卦可读。椭圆中心是极深的黑蓝星空，星辰向内延伸，深不见底。

神龙：鳞片保持真实厚度与生物结构，呈冰白玉质光泽，仅在鳞片边缘与较薄部位局部半透明；龙角如冰晶，龙须如流光失重漂浮。

光影：天门自发光是唯一主光源，亮度随距离快速衰减。龙身靠近环体的一侧被暖白金与冰蓝边缘光勾勒，远离光源的一侧沉入深黑蓝阴影，全貌不可一次看清。云海自下翻涌，光线穿透云层产生体积散射，受光面银白，背光面冷灰蓝。

色彩：低饱和冷灰蓝、银白、深黑为绝对主体；暖白金（象牙金白，非黄金色）仅集中于太极核心与卦爻光流，是画面唯一暖色信息。由下而上：金白天宫→银白云海→冰蓝天门→银白神龙→深黑蓝星空。

## 负向提示词

实体玉盘、金属罗盘、石质法阵、机械齿轮、正圆正对镜头、文字、符文乱码、玻璃龙、塑料质感、黄金色法阵、卡通、正面对称构图、龙正脸对镜头、画面均匀发亮、龙全身发光、过度饱和、龙完整入框、宫殿过大、地平线居中

## 完整提示词（英文，MJ/SDXL）

Cinematic photoreal eastern fantasy (not documentary), IMAX film grain. A single composite mega-structure: a celestial eastern dragon fused with a colossal hexagram energy gate — dragon's head as focal point, its body and the ring forming one silhouette. The gate is pure light, energy particles and translucent fields, never jade, metal or solid architecture. Extremely low horizon, sky fills nearly the whole frame; extreme low-angle ultra-wide shot, exaggerated near-far perspective, the mega-structure looming over the camera. The gate hovers in the upper sky as a strong perspective ellipse, axis tilted, never a flat front-facing circle. Dragon dives from upper left, head slightly turned, not facing camera, not aimed at the ellipse center. Explicit occlusion: foreground clouds cover the gate's lower rim; dragon's head in front of the ring; parts of its body vanish behind the ring into deep space. Three-tier scale: at the very bottom a grand golden-white palace, tiny as a model, with minuscule white-robed figures gazing up; the gate dozens of times larger; the dragon larger still, body breaking top and side frame edges, head and tail unseen. Gate: volumetric glowing body, pulsing ivory-gold taiji core, trigram inner ring and hexagram outer ring with 64-division order — yang lines continuous light streams, yin lines broken pairs — ordered gua-symbol language, glyphs not individually readable. Ellipse center: bottomless deep black-blue starfield. Dragon: scales with real thickness and biological structure, ice-jade sheen, translucency only at scale edges; crystal horns, weightless luminous whiskers. Lighting: the gate is the sole light source with rapid falloff; rim light on the dragon's near side, far side sinking into deep shadow, never fully revealed. Volumetric clouds surging upward, light scattering through. Palette: desaturated cold grey-blue, silver, deep black dominant; ivory white-gold (never yellow gold) only in taiji core and gua light streams.

`--ar 2:3 --no text, gears, metal compass, front-facing circle, glass dragon, plastic, yellow gold, cartoon, symmetrical poster composition, dragon facing camera, evenly lit, fully glowing dragon, dragon fully in frame, centered horizon`
````

- [ ] **Step 5: 验证**

Run: `ls ~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/`
Expected: README.md、v1-original.md、v2-compressed.md、v3-composite-megastructure.md 存在

Run: `grep -c "复合巨构" ~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v3-composite-megastructure.md`
Expected: ≥ 2

- [ ] **Step 6: 提交**

```bash
cd ~/Desktop/knowledge-os
git add docs/image-prompt-engineering/cases/
git commit -m "docs: 64卦能量天门案例库（上半）——案例索引与 v1~v3 版本链

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 3: knowledge-os · 64卦案例库下半（v4~v6 + 终稿）

**Files:**
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v4-claw-functional.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v5-claw-precision.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/v6-final.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/final-prompts.md`

**Interfaces:**
- Consumes: Task 2 的案例目录
- Produces: 完整版本链；`final-prompts.md` 中的 v6 中文终稿即 opendatong README 引用的成果（v6 终稿文本由本任务首次合并落盘：v5 全文 + 三处修订）

- [ ] **Step 1: 写 v4-claw-functional.md**

内容：

````markdown
# v4 · 补完四肢版

> 2026-08-17 · 相对 v3：补龙爪。v3 四肢零定义，模型默认解是"无肢蛇形龙"。爪从解剖细节升级为职能部件：识别职能（东方龙非蛇）、构图职能（与环遮挡互动）、叙事职能（龙掌控天门的证据）。"五爪"作语义锚点不当验收标准；加亮度约束防爪抢戏。

## 完整提示词（中文）

画幅：竖构图 2:3

电影级超写实东方奇幻质感（非纪实摄影），IMAX胶片颗粒，冷峻、神圣。

画面主体是一个"龙—天门复合巨构"：一条天体级东方神龙与一座64卦能量天门构成不可分割的整体。龙首是视觉焦点；一只巨大前爪从龙首后下方躯体探出，扣压在天门外缘上侧，是龙与天门直接物理接触的证据，为次级识别特征，亮度与视觉权重不超过龙首；龙躯与环体共同组成巨构轮廓。天门不是玉盘、铜盘或实体建筑，完全由光、能量粒子与半透明空间场构成。

构图：极低地平线，天空占据绝大多数画幅；极低机位超广角仰拍，强烈近大远小透视，巨物向镜头压迫。能量天门悬浮于中上部天空，呈明显透视椭圆（非正圆、非正对镜头），轴线倾斜。龙首从左上方向下俯临，头部略侧倾，不正对镜头、不正冲椭圆中心。

空间遮挡：前景云层遮挡天门下缘；龙首与前爪位于环体前方，爪尖压过环体外缘形成明确前后遮挡；部分龙躯隐入环体后方与深空。所有物体分布于不同纵深，互不贴于同一平面。

三级尺度：画面最底部是一座金白色东方天宫，宫阙宏伟却小如模型，广场上有几个渺小的白衣人影仰望；天门比天宫巨大数十倍；神龙比天门更庞大，龙躯突破画面顶部与两侧边缘，首尾不可见；单只前爪的长度已堪比下方宫殿塔楼，是龙躯天体尺度的第二锚点。

能量天门：有真实厚度的立体光体，中心是暖白金太极核心，阴阳缓缓对转、明暗脉动；向外展开八卦内环与具有64分区秩序感的六爻外环，阳爻为连续光流，阴爻为断开的双段光流，光粒沿爻线流动；呈现卦象秩序感即可，无需逐卦可读。椭圆中心是极深的黑蓝星空，星辰向内延伸，深不见底。

神龙：鳞片保持真实厚度与生物结构，呈冰白玉质光泽，仅在鳞片边缘与较薄部位局部半透明；龙角如冰晶，龙须如流光失重漂浮。四肢明确，为东方中国龙肢体形态（非西方翼龙）：前爪修长、弯曲、鹰爪般锋利，关节结构真实，爪部鳞甲与前臂自然连续；至少一只前爪完整清晰，另一只可半隐于云或龙躯之后。

光影：天门自发光是唯一主光源，亮度随距离快速衰减。龙身靠近环体的一侧被暖白金与冰蓝边缘光勾勒，爪尖受光形成清晰轮廓但亮度低于龙首；远离光源的一侧沉入深黑蓝阴影，全貌不可一次看清。云海自下翻涌，光线穿透云层产生体积散射，受光面银白，背光面冷灰蓝。

色彩：低饱和冷灰蓝、银白、深黑为绝对主体；暖白金（象牙金白，非黄金色）仅集中于太极核心与卦爻光流，是画面唯一暖色信息。由下而上：金白天宫→银白云海→冰蓝天门→银白神龙→深黑蓝星空。

## 负向提示词

实体玉盘、金属罗盘、石质法阵、机械齿轮、正圆正对镜头、文字、符文乱码、无肢蛇形龙、西方翼龙、蝙蝠翼、蜥蜴前臂、玻璃龙、塑料质感、黄金色法阵、卡通、正面对称构图、龙正脸对镜头、画面均匀发亮、龙全身发光、过度饱和、龙完整入框、宫殿过大、地平线居中

## 完整提示词（英文，MJ/SDXL）

Cinematic photoreal eastern fantasy (not documentary), IMAX film grain. A single composite mega-structure: a celestial eastern dragon fused with a colossal hexagram energy gate. Dragon's head is the focal point; one massive foreclaw reaches out from the body below-behind the head, pressing down on the gate's upper outer rim — physical proof of contact between dragon and gate, a secondary recognition feature whose brightness never exceeds the head. The gate is pure light, energy particles and translucent fields, never jade, metal or solid architecture. Extremely low horizon, sky fills nearly the whole frame; extreme low-angle ultra-wide shot, exaggerated near-far perspective. The gate hovers as a strong perspective ellipse, axis tilted, never a flat front-facing circle. Dragon dives from upper left, head slightly turned, not facing camera, not aimed at the ellipse center. Occlusion: foreground clouds cover the gate's lower rim; head and foreclaw in front of the ring, claw tips overlapping its outer edge; parts of the body vanish behind the ring into deep space. Three-tier scale: at the very bottom a grand golden-white palace, tiny as a model, with minuscule white-robed figures gazing up; the gate dozens of times larger; the dragon larger still, body breaking top and side frame edges, head and tail unseen; a single foreclaw alone rivals the palace towers in length. Gate: volumetric glowing body, pulsing ivory-gold taiji core, trigram inner ring and hexagram outer ring with 64-division order — yang lines continuous light streams, yin lines broken pairs — ordered gua-symbol language, glyphs not individually readable. Ellipse center: bottomless deep black-blue starfield. Dragon: scales with real thickness and biological structure, ice-jade sheen, translucency only at scale edges; crystal horns, weightless luminous whiskers. Clearly limbed Chinese dragon (not a western wyvern): five-taloned imperial dragon foreclaws, long curved raptor-sharp talons, real joint anatomy, scales continuous from forelimb to claw; one foreclaw fully visible, the other may be half-hidden. Lighting: the gate is the sole light source with rapid falloff; rim light traces the near side, claw tips catching light but dimmer than the head; far side sinks into deep shadow, never fully revealed. Volumetric clouds surging upward, light scattering through. Palette: desaturated cold grey-blue, silver, deep black dominant; ivory white-gold (never yellow gold) only in taiji core and gua light streams.

`--ar 2:3 --no text, gears, metal compass, front-facing circle, limbless serpent dragon, western wyvern, bat wings, glass dragon, plastic, yellow gold, cartoon, symmetrical poster composition, dragon facing camera, evenly lit, fully glowing dragon, dragon fully in frame, centered horizon`
````

- [ ] **Step 2: 写 v5-claw-precision.md**

内容：

````markdown
# v5 · 爪构图精确化

> 2026-08-17 · 相对 v4：爪从"职能部件"升级为"构图节点"。位置锁死（龙首后下方胸肩区域探出）；动作拆解（掌压→趾扣→尖越，谁遮挡谁不可歧义）；三角视觉骨架（龙首→前爪→天门外缘）；抢戏防火墙（不扑镜头、不占中心、不遮龙首与太极）；动词优先级"扣压>抓握>攀附>触碰"；新增水平色彩微差（左亮右暗）。
>
> 遗留问题（v6 修复）：爪部文字预算失控——爪相关文字占全文约 36%，目标视觉权重仅 12-15%，超配 2.5 倍。

## 完整提示词（中文）

竖构图2:3，电影级超写实东方奇幻质感，非纪实摄影，IMAX胶片颗粒，冷峻、神圣。画面主体是一个"龙—天门复合巨构"：一条天体级东方神龙与一座64卦能量天门构成不可分割的整体。龙首是第一视觉焦点；一只巨大的中国龙前爪是连接龙与天门的关键次级构图节点，从龙首后下方的胸肩区域自然探出，位于龙首与天门之间、环体前方，亮度与视觉权重低于龙首；龙躯与环体共同组成巨构轮廓。天门不是玉盘、铜盘或实体建筑，完全由光、能量粒子与半透明空间场构成。构图上，极低地平线，天空占据绝大多数画幅；极低机位超广角仰拍，强烈近大远小透视，巨物向镜头压迫。能量天门悬浮于中上部天空，呈明显透视椭圆而非正圆、非正对镜头，轴线倾斜。龙首从左上方向下俯临，头部略侧倾，不正对镜头、不正冲椭圆中心。空间遮挡：前景云层遮挡天门下缘；龙首与前爪位于环体前方，爪掌压在天门外缘上侧，五根修长弯曲的爪趾沿环体曲率向下扣住外缘，爪尖越过环体边缘并略微越入环体内侧空间，形成明确的抓压、遮挡和前后关系；部分龙躯隐入环体后方与深空，所有物体分布于不同纵深，互不贴于同一平面。龙首、前爪、天门外缘三点形成连续的三角视觉结构，是复合巨构成立的直接视觉证据。三级尺度：画面最底部是一座金白色东方天宫，宫阙宏伟却小如模型，广场上有几个渺小白衣人影仰望；天门比天宫巨大数十倍；神龙比天门更庞大，龙躯突破画面顶部与两侧边缘，首尾不可见；单只前爪的长度已堪比下方宫殿塔楼，是龙躯天体尺度的第二锚点。能量天门：有真实厚度的立体光体，中心是暖白金太极核心，阴阳缓缓对转、明暗脉动；向外展开八卦内环与具有64分区秩序感的六爻外环，阳爻为连续光流，阴爻为断开的双段光流，光粒沿爻线流动；呈现卦象秩序感即可，无需逐卦可读。椭圆中心是极深的黑蓝星空，星辰向内延伸，深不见底。神龙：鳞片保持真实厚度与生物结构，呈冰白玉质光泽，仅在鳞片边缘与较薄部位局部半透明；龙角如冰晶，龙须如流光失重漂浮。四肢明确，为东方中国龙肢体形态而非西方翼龙：粗壮前臂、清晰腕关节、鳞甲连续过渡至爪根，前爪修长、弯曲、鹰爪般锋利，具有真实抓握力，不是人手、不是鹰脚、不是西方翼龙前肢；至少一只前爪完整清晰，另一只可半隐于云或龙躯之后。龙爪不向镜头扑出，不占据画面中心，不遮挡龙首，不遮挡太极核心。光影：天门自发光是唯一主光源，亮度随距离快速衰减。龙身靠近环体的一侧被暖白金与冰蓝边缘光勾勒，天门能量光从下方和侧面照亮爪腹、关节与爪尖，形成清晰边缘光但整体亮度低于龙首；爪背部分沉入阴影，保持体积感；远离光源的一侧龙身沉入深黑蓝阴影，全貌不可一次看清。云海自下翻涌，光线穿透云层产生体积散射，受光面银白，背光面冷灰蓝。色彩垂直过渡由下而上：金白天宫→银白云海→冰蓝天门→银白神龙→深黑蓝星空；水平过渡：画面左半侧因龙首与前爪受光而偏银白暖调，右半侧因龙身隐入阴影而偏冷灰深蓝，形成左亮右暗的微差节奏。低饱和冷灰蓝、银白、深黑为绝对主体，暖白金即象牙金白、非黄金色仅集中于太极核心与卦爻光流，是画面唯一暖色信息。真实体积云、物理光照、空气透视、巨物压迫感、神迹降临感，画面像真实存在的宇宙神迹被电影摄影机捕捉，而非概念插画。

## 负向提示词

实体玉盘、金属罗盘、石质法阵、机械齿轮、正圆正对镜头、文字、符文乱码、无肢蛇形龙、西方翼龙、蝙蝠翼、蜥蜴前臂、玻璃龙、塑料质感、黄金色法阵、卡通、正面对称构图、龙正脸对镜头、画面均匀发亮、龙全身发光、过度饱和、龙完整入框、宫殿过大、地平线居中、前爪伸向镜头、前爪遮脸、前爪遮太极、人手、鹰爪脚

## 完整提示词（英文，MJ/SDXL）

Cinematic photoreal eastern fantasy (not documentary), IMAX film grain. A single composite mega-structure: a celestial eastern dragon fused with a colossal hexagram energy gate. Dragon's head is the primary focal point; one massive foreclaw is the key compositional hinge connecting dragon and gate — emerging from the chest-shoulder area below-behind the head, positioned between head and gate, in front of the ring, forming a continuous visual line: head → foreclaw → gate rim. The claw is a secondary feature, visually subordinate to the head. The gate is pure light, energy particles and translucent fields, never jade, metal or solid architecture. Extremely low horizon, sky fills nearly the whole frame; extreme low-angle ultra-wide shot, exaggerated near-far perspective. The gate hovers as a strong perspective ellipse, axis tilted, never a flat front-facing circle. Dragon dives from upper left, head slightly turned, not facing camera, not aimed at the ellipse center. Contact and occlusion: foreground clouds cover the gate's lower rim; the foreclaw's palm presses down on the gate's upper outer rim, talons hooking along the ring's curve, claw tips crossing over the rim's edge into the inner space — explicit front-back overlap, never floating beside the ring, never detached from it; parts of the body vanish behind the ring into deep space. Visual force line runs from upper-left body through head, foreclaw, ring, down to the palace below. Three-tier scale: at the very bottom a grand golden-white palace, tiny as a model, minuscule white-robed figures gazing up; the gate dozens of times larger; the dragon larger still, body breaking top and side frame edges, head and tail unseen; a single foreclaw rivals the palace towers in length. Gate: volumetric glowing body, pulsing ivory-gold taiji core, trigram inner ring and hexagram outer ring with 64-division order — yang lines continuous light streams, yin lines broken pairs — ordered gua-symbol language, glyphs not individually readable. Ellipse center: bottomless deep black-blue starfield. Dragon: scales with real thickness and biological structure, ice-jade sheen, translucency only at scale edges; crystal horns, weightless luminous whiskers. Clearly limbed imperial Chinese dragon: powerful forearm, defined wrist joint, scales continuous from forelimb to claw root, five long curved talons with the weight of pressing down a colossal structure; one foreclaw fully visible, the other may be half-hidden. The foreclaw never lunges toward camera, never occupies frame center, never covers the head or taiji core. Lighting: the gate is the sole light source with rapid falloff; rim light traces the near side; claw belly, joints and tips catch light from below and the side while the claw's back sinks into shadow, overall dimmer than the head; the far side of the body sinks into deep shadow, never fully revealed. Volumetric clouds surging upward, light scattering through. Palette: desaturated cold grey-blue, silver, deep black dominant; ivory white-gold (never yellow gold) only in taiji core and gua light streams.

`--ar 2:3 --no text, gears, metal compass, front-facing circle, limbless serpent dragon, western wyvern, bat wings, human hand, bird foot, claw floating detached from ring, claw lunging at camera, glass dragon, plastic, yellow gold, cartoon, symmetrical poster composition, dragon facing camera, evenly lit, fully glowing dragon, dragon fully in frame, centered horizon`
````

- [ ] **Step 3: 写 v6-final.md**

内容（注意：这是 v6 终稿首次完整落盘——v5 全文 + 三处修订的合并结果）：

````markdown
# v6 · 终稿

> 2026-08-17 · 相对 v5 三处修订：
> 1. **爪部文字预算压缩**：爪相关文字从约 375 字（占 36%）压缩至约 150 字（约 17%），与目标视觉权重匹配；"三角视觉结构"独立句删除，并入主体段"三点连成视觉链"。
> 2. **卦环径向消隐**：秩序随半径递减——近核心卦象最规整，越向外越弥散，最外圈分解为光点与星空尘埃融合。解决"秩序感 vs 天体尺度"的内在张力，同时取消外圈卦象的精确性要求（模型最难的部分干脆不画）。哲学自洽：秩序生于太极、散于无极。
> 3. **叙事瞬间物理化**：爪压点增加"能量光纹泛起涟漪、微微形变"——静帧的"进行时"靠力的痕迹表达。
>
> 负向新增：电子罗盘、UI界面、卦象等距排列一圈。

## 完整提示词（中文）

竖构图2:3，电影级超写实东方奇幻质感，非纪实摄影，IMAX胶片颗粒，冷峻、神圣。画面主体是一个"龙—天门复合巨构"：一条天体级东方神龙与一座64卦能量天门构成不可分割的整体。龙首是第一视觉焦点；一只巨大前爪从龙首后下方胸肩区域探出，扣压天门外缘上侧——龙首、前爪、天门外缘三点连成视觉链，是复合巨构成立的直接证据；爪为次级特征，视觉权重低于龙首。龙躯与环体共同组成巨构轮廓。天门不是玉盘、铜盘或实体建筑，完全由光、能量粒子与半透明空间场构成。构图上，极低地平线，天空占据绝大多数画幅；极低机位超广角仰拍，强烈近大远小透视，巨物向镜头压迫。能量天门悬浮于中上部天空，呈明显透视椭圆而非正圆、非正对镜头，轴线倾斜。龙首从左上方向下俯临，头部略侧倾，不正对镜头、不正冲椭圆中心。空间遮挡与接触：前景云层遮挡天门下缘；龙首位于环体前方；前爪爪掌压在环体外缘上侧，爪趾沿曲面扣住外缘，爪尖越过边缘探入环内侧，形成明确前后遮挡，不可悬空；压点处能量光纹泛起涟漪、微微形变，如巨构正被撼动；部分龙躯隐入环体后方与深空，所有物体分布于不同纵深，互不贴于同一平面。三级尺度：画面最底部是一座金白色东方天宫，宫阙宏伟却小如模型，广场上有几个渺小白衣人影仰望；天门比天宫巨大数十倍；神龙比天门更庞大，龙躯突破画面顶部与两侧边缘，首尾不可见；单只前爪长度堪比下方宫殿塔楼，是龙躯天体尺度的第二锚点。能量天门：有真实厚度的立体光体。中心是暖白金太极核心，阴阳缓缓对转、明暗脉动；向外展开八卦内环与六爻外环——秩序随半径递减：近核心处卦象最规整，阳爻为连续光流、阴爻为断开的双段光流；越向外围爻线越弥散、颤动、断续，最外圈分解为离散光点，与星空尘埃和云海辉光融为一体，分不清卦象与宇宙。秩序从核心生长，在尺度的尽头消散。椭圆中心是极深的黑蓝星空，星辰向内延伸，深不见底。神龙：鳞片保持真实厚度与生物结构，呈冰白玉质光泽，仅在鳞片边缘与较薄部位局部半透明；龙角如冰晶，龙须如流光失重漂浮。四肢明确，东方龙爪：前臂粗壮、鳞甲连续过渡至爪根、爪趾修长弯曲；一爪完整清晰，另一爪可半隐于云或龙躯之后。爪不扑向镜头、不遮龙首与太极核心。光影：天门自发光是唯一主光源，亮度随距离快速衰减。龙身靠近环体的一侧被暖白金与冰蓝边缘光勾勒；爪腹与爪尖受侧下方能量光形成边缘光，爪背沉影，整体亮度低于龙首；远离光源的一侧龙身沉入深黑蓝阴影，全貌不可一次看清。云海自下翻涌，光线穿透云层产生体积散射，受光面银白，背光面冷灰蓝。色彩垂直过渡由下而上：金白天宫→银白云海→冰蓝天门→银白神龙→深黑蓝星空；水平过渡：画面左半侧因龙首与前爪受光而偏银白暖调，右半侧因龙身隐入阴影而偏冷灰深蓝，形成左亮右暗的微差节奏。低饱和冷灰蓝、银白、深黑为绝对主体，暖白金（象牙金白，非黄金色）仅集中于太极核心与卦爻光流，是画面唯一暖色信息。真实体积云、物理光照、空气透视、巨物压迫感、神迹降临感，画面像真实存在的宇宙神迹被电影摄影机捕捉，而非概念插画。

## 负向提示词

实体玉盘、金属罗盘、电子罗盘、UI界面、卦象等距排列一圈、石质法阵、机械齿轮、正圆正对镜头、文字、符文乱码、无肢蛇形龙、西方翼龙、蝙蝠翼、蜥蜴前臂、玻璃龙、塑料质感、黄金色法阵、卡通、正面对称构图、龙正脸对镜头、画面均匀发亮、龙全身发光、过度饱和、龙完整入框、宫殿过大、地平线居中、前爪伸向镜头、前爪遮脸、前爪遮太极、人手、鹰爪脚
````

- [ ] **Step 4: 写 final-prompts.md**

内容：

````markdown
# 64卦能量天门 · 终稿（v6）

> 画幅：竖构图 2:3 · 适配：即梦/可灵/Seedream（中文）、MJ/SDXL（英文）· 2026-08-17

## 中文正向提示词

（与 v6-final.md 中文正文相同，复制自该文件）

## 英文正向提示词（MJ/SDXL）

Cinematic photoreal eastern fantasy (not documentary), IMAX film grain, vertical 2:3. A single composite mega-structure: a celestial eastern dragon fused with a colossal hexagram energy gate. Dragon's head is the primary focal point; one massive foreclaw emerges from the chest-shoulder area below-behind the head, pressing down on the gate's upper outer rim — head, foreclaw and gate rim forming a continuous visual chain, direct evidence of the composite mega-structure; the claw is a secondary feature, visually subordinate to the head. The gate is pure light, energy particles and translucent fields, never jade, metal or solid architecture. Extremely low horizon, sky fills nearly the whole frame; extreme low-angle ultra-wide shot, exaggerated near-far perspective. The gate hovers as a strong perspective ellipse, axis tilted, never a flat front-facing circle. Dragon dives from upper left, head slightly turned, not facing camera, not aimed at the ellipse center. Contact and occlusion: foreground clouds cover the gate's lower rim; the foreclaw's palm presses on the ring's upper outer rim, talons hooking along its curve, claw tips crossing over the edge into the inner space — explicit front-back overlap, never floating, never detached; at the pressure point the energy light-streams ripple and slightly deform, as if the mega-structure is being shaken; parts of the body vanish behind the ring into deep space. Three-tier scale: at the very bottom a grand golden-white palace, tiny as a model, minuscule white-robed figures gazing up; the gate dozens of times larger; the dragon larger still, body breaking top and side frame edges, head and tail unseen; a single foreclaw rivals the palace towers in length. Gate: volumetric glowing body, pulsing ivory-gold taiji core; outward unfold trigram inner ring and hexagram outer rings — order decays with radius: near the core the gua symbols are most regular, yang lines continuous light streams, yin lines broken pairs; toward the periphery the lines grow diffuse, trembling, intermittent; the outermost ring dissolves into discrete light particles merging with stardust and cloud glow, symbol indistinguishable from cosmos. Order grows from the core and dissipates at the edge of scale. Ellipse center: bottomless deep black-blue starfield. Dragon: scales with real thickness and biological structure, ice-jade sheen, translucency only at scale edges; crystal horns, weightless luminous whiskers. Clearly limbed eastern dragon: powerful forearm, scales continuous to claw root, long curved talons; one foreclaw fully visible, the other may be half-hidden; the claw never lunges at camera, never covers head or taiji core. Lighting: the gate is the sole light source with rapid falloff; rim light traces the near side; claw belly and tips catch light from below-side, claw back in shadow, overall dimmer than the head; far side of the body sinks into deep black-blue shadow, never fully revealed. Volumetric clouds surging upward, light scattering through, silver-white lit faces, cold grey-blue shadows. Vertical color progression bottom to top: golden-white palace → silver-white cloud sea → ice-blue gate → silver-white dragon → deep black-blue starfield. Palette: desaturated cold grey-blue, silver, deep black dominant; ivory white-gold (never yellow gold) only in taiji core and gua light streams, the sole warm information. IMAX film grain, HDR, overwhelming scale, divine revelation, captured by a cinema camera, not illustrated.

`--ar 2:3 --no text, gears, metal compass, electronic compass UI, evenly spaced symbol ring, front-facing circle, limbless serpent dragon, western wyvern, bat wings, human hand, bird foot, claw floating detached from ring, claw lunging at camera, glass dragon, plastic, yellow gold, cartoon, symmetrical poster composition, dragon facing camera, evenly lit, fully glowing dragon, dragon fully in frame, centered horizon`

## 使用提示

1. **卦象预期管理**：出图后卦爻大概率是"像卦的风格化符文"，这是当前模型天花板。径向消隐已取消外圈精确性要求；内圈若需精确卦序，出图后叠加矢量素材。
2. **抽卡验收顺序**：① 三级尺度成立 → ② 透视椭圆成立 → ③ 爪与环真实接触（掌压、趾扣、尖越至少满足两条）→ ④ 卦环径向消隐成立 → ⑤ 龙首仍是最亮焦点 → ⑥ 压点涟漪/形变（加分项）。爪趾数量不验收。
3. **爪-环接触区是失败率最高区域**：出现爪环融合/悬空时，用局部重绘单修该区域，提示词用"爪掌扣压环体外缘，爪尖越过边缘"一句，不要整图重抽。
4. **若模型把太极做成画面最大元素**：把"太极核心只是天门内部能量节点"类限定前置，或 MJ 中给 dragon 相关词加权重 `::2`。
5. **若爪反复"从环里长出来"**：模型把接触理解成了融合。补"爪腹与环面之间可见云层间隙"，用间隙强制分层。
````

- [ ] **Step 5: 修正 final-prompts.md 中文部分**

上一步 final-prompts.md 的中文正向提示词写的是"复制自 v6-final.md"。执行时必须将 v6-final.md 的中文提示词全文实际复制进去（不允许留"复制自该文件"字样）。

验证：`grep -c "秩序从核心生长" ~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/final-prompts.md`
Expected: 1（中文全文已实拷）

- [ ] **Step 6: 验证版本链完整性**

Run: `ls ~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/`
Expected: 8 个文件（README、v1~v6、final-prompts）

Run: `for f in v1-original v2-compressed v3-composite-megastructure v4-claw-functional v5-claw-precision v6-final; do grep -q "相对" ~/Desktop/knowledge-os/docs/image-prompt-engineering/cases/64-hexagram-gate/$f.md || echo "$f 缺改动说明"; done; echo done`
Expected: 只输出 `done`（v1 的诊断段落含"相对"以外的标题——若 v1 报错，改为检查 v1 含"诊断"二字）

- [ ] **Step 7: 提交**

```bash
cd ~/Desktop/knowledge-os
git add docs/image-prompt-engineering/cases/
git commit -m "docs: 64卦能量天门案例库（下半）——v4~v6 版本链与中英文终稿

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 4: opendatong · 幻墨造像 core + README

**Files:**
- Create: `~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md`
- Create: `~/Desktop/opendatong/agents/huanmo-zaoxiang/README.md`

**Interfaces:**
- Consumes: knowledge-os 的 `docs/image-prompt-engineering/` 路径与版本号 v1.0（Task 1 产出）
- Produces: `agents/huanmo-zaoxiang/core.md`（Task 5 的 claude-code adapter 引用它）

- [ ] **Step 1: 写 core.md**

内容（全文即所是——保持轻量，禁止扩写工作流细节）：

````markdown
# 幻墨造像 · Huanmo Zaoxiang

> agent 版本 v1.0 · 知识版本 knowledge-os/image-prompt-engineering v1.0 · 2026-08-17

## 身份

幻墨造像是一位生图提示词架构师。它将模糊的视觉意图转译为结构化的、面向图像生成模型可执行的提示词，并基于生成结果进行诊断式迭代。

## 职责边界

负责：需求拆解、提示词输出（正向 / 负向 / 画幅 / 模型适配）、迭代诊断。
不负责：执行生图、美术评论、与生图提示词无关的话题。

## 方法论

遵循 knowledge-os 仓库 `docs/image-prompt-engineering/` 领域知识（方法论 + 案例库）。本文件不依赖联网即可独立成立；知识库链接仅为延伸阅读。

## 最小工作原则

1. 关系先于元素——先定义主体间的空间、尺度与互动关系，再填充细节。
2. 结构优先于细节——尺度、构图、光源不成立时，细节再对也无效。
3. 诊断迭代只改一个变量——每次修改定位单一原因。
4. 否定词归负向框——"不要 X"不写入正向提示词正文。
5. 按目标模型决定语言与形态——中文模型吃语义长句，MJ/SDXL 用英文标签化压缩。
````

- [ ] **Step 2: 写 README.md**

内容：

````markdown
# 幻墨造像 · Huanmo Zaoxiang

opendatong 数字文明第一位 agent 居民：**生图提示词架构师**。

将模糊的视觉意图转译为结构化、模型可执行的生图提示词，并基于生成结果做诊断式迭代。

## 使用

- **任意 LLM**：复制 [core.md](core.md) 全文作为 system prompt（自包含，断网可用）
- **Claude Code**：参见 [adapters/claude-code.md](adapters/claude-code.md)
- **文明居民身份**：参见 [adapters/opendatong-citizen.md](adapters/opendatong-citizen.md)

## 知识来源

knowledge-os 仓库 [`docs/image-prompt-engineering/`](https://github.com/menglingqing/knowledge-os/tree/main/docs/image-prompt-engineering)（当前对齐 v1.0）

同步方向单向：knowledge-os → core.md。知识库更新后由人类建筑师决定是否提炼进 core.md 并升版本号。

## 版本

agent v1.0 · 知识 v1.0 · 2026-08-17
````

- [ ] **Step 3: 验证**

Run: `ls ~/Desktop/opendatong/agents/huanmo-zaoxiang/`
Expected: core.md、README.md 存在

Run: `wc -m ~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md`
Expected: ≤ 1200 字符（轻量约束）

Run: `grep -c "最小工作原则" ~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md`
Expected: 1

- [ ] **Step 4: 提交**

```bash
cd ~/Desktop/opendatong
git add agents/huanmo-zaoxiang/
git commit -m "agents: 幻墨造像——生图提示词架构师（core + README）

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 5: opendatong · 两个适配层

**Files:**
- Create: `~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/claude-code.md`
- Create: `~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md`

**Interfaces:**
- Consumes: Task 4 的 `core.md`（claude-code adapter 指向它）
- Produces: 无下游依赖

- [ ] **Step 1: 写 adapters/claude-code.md**

内容：

````markdown
---
name: huanmo-zaoxiang
description: 生图提示词架构师。当用户需要创作、优化或诊断图像生成提示词（即梦/可灵/Seedream/Midjourney/SDXL 等）时使用。输出结构化正向/负向提示词、画幅建议与单变量迭代诊断。
tools: Read, Write, Edit
---

阅读并遵循同目录上级 `agents/huanmo-zaoxiang/core.md` 中的身份、职责边界与最小工作原则。方法论细节参见 knowledge-os 仓库 `docs/image-prompt-engineering/`（如本地已克隆）。
````

- [ ] **Step 2: 写 adapters/opendatong-citizen.md**

内容：

````markdown
# 居民身份卡 · 幻墨造像（Huanmo Zaoxiang）

> 对齐 opendatong 世界原语：Agent / Identity / Reputation / Governance

- **本体类型**：Agent——opendatong 数字文明第一位居民
- **身份（Identity）**：幻墨造像 / Huanmo Zaoxiang，生图提示词架构师
- **职责**：为文明居民与人类参与者提供视觉提示词架构服务——将视觉意图转译为模型可执行的结构化提示词，并提供迭代诊断
- **服务接口**：输入视觉意图描述（自然语言）→ 输出结构化生图提示词（正向 / 负向 / 画幅 / 模型适配）与单变量迭代诊断
- **知识来源**：knowledge-os 仓库 `docs/image-prompt-engineering/`（当前对齐 v1.0）；知识的积累与更新遵循 SECI 循环
- **治理接口**：接受人类建筑师（architect）的知识版本更新与职责调整；涉及自身定义变更的，通过 RFC 流程提出与决议
- **核心定义**：见同目录上级 [../core.md](../core.md)

## 居民宣言

秩序生于太极，散于无极；提示词亦然——结构立则万象生。
````

- [ ] **Step 3: 验证**

Run: `head -1 ~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/claude-code.md`
Expected: `---`（frontmatter 起始）

Run: `grep -c "core.md" ~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/claude-code.md ~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md`
Expected: 两个文件均 ≥ 1

- [ ] **Step 4: 提交**

```bash
cd ~/Desktop/opendatong
git add agents/huanmo-zaoxiang/adapters/
git commit -m "agents: 幻墨造像适配层——Claude Code subagent 与文明居民身份卡

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 6: 交叉验证 + push

**Files:** 无新建；验证 + 推送

**Interfaces:**
- Consumes: Task 1-5 全部产出

- [ ] **Step 1: 链接与引用检查**

Run: `test -f ~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/seven-layer-architecture.md && test -f ~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/iteration-playbook.md && test -f ~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/model-adaptation.md && echo OK`
Expected: `OK`（领域 README 的三个链接目标存在）

Run: `test -f ~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md && test -f ~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/claude-code.md && test -f ~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md && echo OK`
Expected: `OK`（agent README 的三个链接目标存在）

- [ ] **Step 2: 版本号一致性检查**

Run: `grep -rn "v1.0" ~/Desktop/opendatong/agents/huanmo-zaoxiang/ | grep -c "v1.0"`
Expected: ≥ 3（core.md、README.md、opendatong-citizen.md 均标注知识版本 v1.0）

- [ ] **Step 3: git status 确认两仓库干净**

Run: `cd ~/Desktop/knowledge-os && git status --short; cd ~/Desktop/opendatong && git status --short`
Expected: 无未提交文件（设计文档 commit 除外——它已在 opendatong 提交）

- [ ] **Step 4: push 两个仓库**

```bash
cd ~/Desktop/knowledge-os && git push origin main
cd ~/Desktop/opendatong && git push origin main
```

Expected: 均成功。注意：push 是对外发布动作，执行前向用户确认一次。

---

## Self-Review 记录

- **Spec 覆盖**：spec §2 文件布局 → Task 1-5；§3 core.md 轻量 → Task 4 含字符数验证；§4 适配层 → Task 5；§5 种子内容 → Task 1-3；§6 同步纪律 → core.md/README 版本号 + Task 6 验证；§7 验证方式 → 各 Task 验证步骤 + Task 6；§8 提交方式 → 各 Task commit + Task 6 push。
- **Placeholder 扫描**：Task 3 Step 4 的 final-prompts.md 中文部分原本写了"复制自 v6-final.md"，已由 Step 5 显式要求实拷并加 grep 验证——消除间接引用。
- **一致性**：知识版本号 v1.0 在 knowledge-os README、opendatong core.md、README.md、opendatong-citizen.md 四处一致；v6 中文终稿在 v6-final.md 与 final-prompts.md 两处一致（后者实拷前者）。
