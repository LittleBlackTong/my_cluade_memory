---
type: source-summary
title: Karpathy "LLM Wiki" 声明
source: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
created: 2026-08-09
updated: 2026-08-09
tags: [knowledge-management, llm, methodology]
---

# Karpathy "LLM Wiki" 声明

**TL;DR**：Karpathy 提出用 LLM 增量式维护一个持久化的、相互链接的 markdown 维基，作为个人知识库的核心。区别于 RAG 的"每次从原始文档重新检索"，wiki 是"编译一次、持续更新"的复利型产物。

## 核心观点

- **RAG 的局限**：LLM 每次查询都从原始文档重新发现知识，没有积累。综合五个文档的微妙问题需要每次都重新拼凑。
- **维基的优势**：跨引用已经在那儿，矛盾已经被标记，综合已经反映所有已读内容。每加入一个资料源或提出一个问题，wiki 就更丰富。
- **角色分工**：Obsidian 是 IDE，LLM 是程序员，wiki 是代码库。人类策展资料、引导分析、问好问题；LLM 做所有簿记工作（摘要、交叉引用、归档、维护一致性）。

## 三层架构

1. **Raw sources**（原始资料）— 用户策展、不可变、事实来源
2. **Wiki**（维基）— LLM 生成的 markdown 实体/概念页，LLM 完全负责维护
3. **Schema**（约定文档）— CLAUDE.md 或 AGENTS.md，定义 wiki 形状与维护规则，与 LLM 共同演化

## 三种操作

- **Ingest（摄入）**：新资料 → 读、提取要点、写摘要、更新相关页面、记录日志
- **Query（查询）**：读 index 找相关页面 → 综合回答；好回答可归档回 wiki
- **Lint（检视）**：定期健康检查——矛盾、过时说法、孤儿页面、缺失引用

## 为什么可行

人类放弃维基是因为维护成本超过价值。LLM 不无聊、不会忘记更新引用、一次能触及 15 个文件。维护成本接近零。

历史脉络：与 Vannevar Bush 1945 年的 Memex 构想（个人策展、关联链路）精神相通。布什解决不了的"谁来做维护"，由 LLM 承担。

## 相关页面

- [[setup-llm-wiki-personal]] — 用户在自己的机器上实例化这个模式的具体配置
- [[long-term-memory-boundary]] — LLM 长期记忆机制的边界讨论