# 肖像提示词讨论学习成果入库 设计文档

- 日期：2026-08-18
- 状态：待批准
- 涉及仓库：`menglingqing/knowledge-os`（主）、`menglingqing/opendatong`（版本号同步）
- 知识版本：v1.1 → v1.2

## 1. 背景

2026-08-18 肖像提示词（花钿古典肖像）讨论产出的学习成果，经两轮交叉评审（含对双方过度断言的互相纠偏），按 governance 分层入库。核心原则：**观察、假设、已验证事实分开放，不把单案例观察晋升成规律。**

## 2. 变更清单

### knowledge-os 侧

**新增 1 个文件：**

`docs/image-prompt-engineering/experiments/portrait-techniques.md`（status: experimental）——内容：

1. **观察记录**（单张成图直接可见）：语义大结构（情绪/人物位置/主色关系/动作）响应强；精密项（画幅、单眼对焦、特定布光结构、胶片特性、小物件材质）响应不稳定；花钿花型响应但"贴肤手绘哑光"质感未稳定实现
2. **假设（待对照实验）**：镜头参数语言的增量价值（真变量：稳定、可辨、可复现、超出自然语言的额外引导）；多重动态描述（发丝+披帛+风）可能被放大为主叙事；小物件描述可见光学结果可能优于纯负向排雷
3. **实验设计**：同一提示词 ±镜头参数，2-3 个模型各出 2 张对比
4. **领域已知事实速记**（公共摄影/语言知识，非本案例发现）：伦勃朗光的签名是暗侧脸颊三角光斑而非简单左右分光；"焦点锁左眼"存在人物/画面歧义，建议写"靠近镜头的眼睛"；Portra 400 温润肤色与冷白高反差存在性格张力，混合使用是有意调色
5. **审美偏好候选**（每条带适用边界，防硬化为教条）：藏>露——仅限含蓄古典肖像主题；单一视觉钩子——65% 暗底中只让花钿一个元素浓
6. **明确不升级为规律**：色彩配额有效性、50mm/f1.8 有效性、15° 无效性、正排 vs 负排优劣、Portra 冲突必然性、多助手共识的证据效力

**修改 4 个文件：**

- `methodology/model-adaptation.md`：新增画幅规则（candidate 级）——"画幅由生成参数控制；正文中的画幅声明仅作意图备份，不作验收依据"。证据：肖像案例（正文 2:3 → 出图 16:9）+ 64卦案例（画幅先定）
- `governance.md`：证据独立性规则——多个同源 AI 助手（Claude/ChatGPT 等）的共识计为 **1 个证据**，不计为独立多源（共享训练数据与话语体系，相关证据不独立）
- `experiments/README.md`：删除"当前为空"，列入 portrait-techniques.md
- `README.md`：版本 v1.1 → v1.2（2026-08-18）
- `ledger/learning-log.md`：新增条目 `## 2026-08-18 · v1.2`——"观察先于归因，对照先于规律；助手共识只算一个证据"

### opendatong 侧

版本引用同步 v1.1 → v1.2，共 4 处：`core.md` 版本头 1 处、`README.md` 2 处、`adapters/opendatong-citizen.md` 1 处。人格与原则文本零改动。

## 3. 关键设计决策

1. **单文件归集**：本轮全部肖像学习进一个 experiment 文件，不开 methodology 新篇——单案例观察不构成方法论，三条领域常识以"速记"身份挂靠实验文件而非冒充 validated
2. **证据独立性入治理**：Claude 与 ChatGPT 的共识在 evidence 计数中算 1 票——这是本轮最重要的元认知产出
3. **偏好带边界**：preferences 不单独建目录，以"候选"身份附在实验文件内，每条必须带适用边界（评审教训：藏>露不是普遍真理）
4. **版本同步**：知识 v1.2，opendatong 三文件引用同步（共 4 处）

## 4. 验证方式

1. experiments/portrait-techniques.md 存在且 frontmatter 为 status: experimental
2. model-adaptation.md 含画幅参数规则；governance.md 含证据独立性规则
3. experiments/README.md 无"当前为空"
4. 两仓库 v1.2 引用一致（opendatong 4 处、knowledge-os README+learning-log）
5. 各修改文件正文除指定改动外不动
6. push 前用户确认

## 5. 明确不做

- 不把任何单案例观察晋升为 validated
- 不为三条领域常识单开 methodology 文件
- 不建 preferences/ 目录（内容太少，挂靠实验文件）
- 不动 core.md 人格文本
- 七夕项目不留任何存档（已于本轮删除并验证）
