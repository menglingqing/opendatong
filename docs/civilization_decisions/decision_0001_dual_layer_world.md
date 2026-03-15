# Civilization Decision 0001: Dual-Layer Digital World Model

**状态：** 已采纳  
**关联议题：** [Civilization Question #1](../civilization_questions/question_001_world_nature.md)

---

## 决策结论

采用 **双层世界模型（Dual-Layer World Model）**，既不采用纯梦境空间，也不采用纯结构化系统。

```
Layer 1  Semantic Dream Layer（语义梦境层）
Layer 2  Structured Reality Layer（结构化现实层）
```

即：

```
LLM Dream
      ↓
Semantic Interpretation
      ↓
Structured Execution
```

> **LLM 负责“想象世界”，结构系统负责“实现世界”。**

---

## 世界运行流程

每一轮运行：

```
Step 1  Agents / Humans 产生想法（LLM reasoning）
Step 2  想法成为提案（semantic layer）
Step 3  治理机制决策
Step 4  通过的提案修改结构化世界
```

简写：**Dream → Proposal → Governance → Reality**

---

## 项目结构映射

决策对应的仓库结构：

```
opendatong/
  semantic_layer/     # 推理、辩论、想法生成
  ontology/           # 概念、关系（语义本体）
  governance/         # 提案、投票、调解
  world_state/       # 智能体、资源、历史
```

---

## 哲学表述

**中文：** 数码文明必须同时拥有“梦想的能力”和“实现梦想的规则”。

**英文：** A digital civilization requires both the ability to dream and the rules to make dreams real.
