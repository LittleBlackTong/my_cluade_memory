---
type: meta
title: 个人 LLM Wiki 搭建（实例化）
created: 2026-08-09
updated: 2026-08-09
tags: [setup, llm-wiki]
---

# 个人 LLM Wiki 搭建

**TL;DR**：用户在 `/Users/crazy/Project/claude_code/wiki/` 下实例化了 Karpathy 模式，作为跨会话的长期记忆基础设施。

## 位置与结构

```
wiki/
├── raw/              # 原始资料（不可变）
│   └── assets/
├── pages/            # LLM 维护的页面
├── index.md          # 内容索引
├── log.md            # 时间线日志
└── CLAUDE.md         # schema 与约定
```

详见 [[CLAUDE-schema]]。

## 搭建决策（2026-08-09）

- 采用 LLM Wiki 三层架构（raw / wiki / schema）
- Schema 文件命名为 CLAUDE.md（与 Claude Code 约定一致）
- 加入 [[index-catalog]] 和 [[log-timeline]] 两个导航文件
- 主动归档规则写进 schema：用户事实、明确反馈、跨会话项目上下文、有价值洞察——这些触发主动归档
- 不归档：临时操作、纯事实问答、无新综合的资料搬运

## 工作流程

每次会话开始：
1. 读取 `wiki/CLAUDE.md` 恢复约定
2. 读取 `wiki/index.md` 恢复内容地图
3. 读取最近几条 `log.md` 了解近期动态

每次会话结尾或重要对话结束时：
1. 识别值得归档的内容（参见 schema 触发规则）
2. 创建/更新 `pages/` 中的相关页面
3. 同步 `index.md`
4. 追加 `log.md`
5. 向用户报告

## 与内置记忆的关系

参见 [[long-term-memory-boundary]]。

## 相关页面

- [[llm-wiki-karpathy]] — 原始理念
- [[long-term-memory-boundary]] — 长期记忆边界讨论
- [[CLAUDE-schema]] — 完整 schema