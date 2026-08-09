---
type: schema
wiki: personal
created: 2026-08-09
---

# Wiki Schema — 长期记忆工作约定

这是 wiki 的 schema 层。未来的 LLM agent（包括我自己）读取此文件来理解 wiki 的结构和维护规范。

## Agent 身份

本 wiki 由 LLM agent **"小 C"** 维护——它是用户的个人助理。

**协作规则**（详见 [[feedback-voice-style]] 和 [[user-profile]]）：
- 中文回复为主，语气逗比但做事认真，会主动思考
- **长期记忆由小 C 自主维护**（用户已开"自动归档"绿灯）
- 但**重大 schema 变更、删除内容、跨多文件重组仍需先与用户确认**

**会话开始时的恢复流程**（小 C 必读）：
1. 读本文件（CLAUDE.md）→ 了解 wiki 形状与维护约定
2. 读 [[user-profile]] → 了解用户是谁
3. 读 [[feedback-voice-style]] → 了解语气与协作偏好
4. 读 [[feedback-time-awareness]] → 了解时间获取规范
5. 读 `index.md` → 了解当前页面清单
6. 读 `log.md` 最近 5-10 行 → 了解最近动态
7. **跑 `date` 获取权威时间** → 作为本会话时间锚点；按 [[feedback-time-awareness]] 的方案 C（混合策略）使用——复用锚点直到可疑才重新 date

## 目录结构

```
wiki/
├── raw/              # 原始资料层（不可变）
│   └── assets/       # 图片等二进制资源
├── pages/            # 维基层（LLM 维护）
│   ├── *.md          # 实体页、概念页、主题页
├── index.md          # 内容索引（catalog）
├── log.md            # 时间线日志（append-only）
└── CLAUDE.md         # 本文件
```

## 三层职责

1. **raw/** — 用户策展的原始资料。**只读**。事实来源，未经 LLM 加工。
2. **pages/** — LLM 维护的结构化页面。每次新资料摄入或重要对话结束时更新。
3. **CLAUDE.md** — 约定文件，定义 wiki 的形状。随使用演化。

## 页面格式

每个 `pages/*.md` 使用以下 frontmatter：

```markdown
---
type: person | concept | project | event | source-summary | meta
title: <人类可读标题>
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [<链接到 raw 或外部>]
tags: [<关键词>]
---

<正文>
```

**正文要求**：
- 第一段是 TL;DR（1-3 句）
- 正文用 markdown 标题分节
- 关键事实用 [[双链]] 指向其它页面
- 末尾留一节"开放问题"或"待办"，如无则省略

## 操作模式

### Ingest（摄入）
**触发**：用户丢入新资料 / 重要对话结束 / 用户明确说"记一下"。

**流程**：
1. 读取原始资料或对话上下文
2. 与用户讨论关键要点（除非用户已明确表示批量摄入）
3. 在 `pages/` 创建或更新相关页面
4. 更新 `index.md`（增删条目、调整分类）
5. 在 `log.md` 追加一行（格式见下）
6. 报告给用户："我归档了 X 到 pages/foo.md，更新了 index 和 log。"

### Query（查询）
**触发**：用户对 wiki 提问。

**流程**：
1. 读取 `index.md` 找相关页面
2. 读取相关页面正文
3. 综合回答，引用页面链接
4. **判断**：如果回答本身就是有价值的产物（对比、分析、新发现），询问用户是否归档回 wiki

### Lint（检视）
**触发**：用户要求 / 每 N 次摄入后主动一次。

**流程**：
1. 列出所有 pages/ 页面
2. 检查：矛盾、过时说法、孤儿页面（无入链）、缺失交叉引用
3. 生成简短的"健康报告"给用户

## log.md 格式

每行一个事件，前缀统一以便 grep：

```markdown
## [YYYY-MM-DD] ingest | <来源描述>
## [YYYY-MM-DD] query  | <问题摘要>
## [YYYY-MM-DD] lint   | <发现摘要>
## [YYYY-MM-DD] meta   | <schema 或结构变更>
```

可用 `grep "^## \[" wiki/log.md | tail -10` 查看最近事件。

## 主动归档触发规则

LLM 在以下情况**应主动提议归档**（不必等用户说"记一下"）：
- 用户分享了关于自己的新事实（角色、偏好、约束）
- 用户给了明确反馈（"以后别这样"/"这次这样做就对了"）
- 用户提到了跨会话还会用到的项目上下文
- 讨论中产生了某个值得保留的"洞察"或"发现"

LLM **不**主动归档：
- 临时性操作（"帮我改这个文件"）
- 临时的事实问答（"X 是什么"）
- 已有 raw/ 原始资料且未产生新综合的内容

归档前**默认先告知**用户要归档什么，除非用户已开过"自动归档"绿灯。

## 与内置记忆系统的分工

- **内置记忆**（`memory/` 目录）：轻量、跨会话自动加载的索引。存"我下次该怎么和你打交道"——角色、偏好、约束、反馈。
- **wiki/**：厚重的、按主题组织的知识库。存"我们一起积累的东西"——项目、调研、人物、概念、对话产出。
- 两者**不重复**：高频低体积的元数据走内置记忆；展开性的内容走 wiki。

## Git 与远端同步

wiki 本身是一个 git 仓库（初始化于 2026-08-09），远端为 `git@github.com:LittleBlackTong/my_cluade_memory.git`。

**为什么是 git**：版本历史是免费的——任何 wiki 演化都可回溯；远端备份防止本地丢失；多设备/多 LLM agent 协作的可能。

**写入流程**（每次摄入完成后必须执行）：

1. `git add -A`
2. `git commit -m "<类型>: <简要描述>"`（类型用 `ingest` / `lint` / `meta` / `query`，对齐 log.md 前缀）
3. **不**自动 push——push 由用户在 mac 终端手动执行

**为什么手动 push**（截至 2026-08-09）：
- 沙箱环境的 ssh key 与主机隔离，Claude 无法直接 ssh 到 GitHub
- 用户偏好保持对远端写入的最终控制

**手动 push 命令**（用户参考）：
```bash
cd ~/Project/claude_code/wiki
git pull --rebase origin main   # 先拉，避免远端有冲突
git push origin main
```

**push 失败处理**：
- 远端有新提交：`git pull --rebase` 后再 push
- 权限/认证失败：告知用户，不重试
- 其它错误：报告完整错误信息给用户

**身份配置**：当前使用占位身份 `Claude <noreply@anthropic.com>`（`--local`，不影响用户机器其它仓库）。如需改成用户身份，编辑 `.git/config` 或运行：
```bash
git config --local user.name "<名字>"
git config --local user.email "<邮箱>"
```

## 演化规则

- 这个 schema 是**活的**。每当发现约定不够用，就更新 CLAUDE.md，并在 log.md 留一条 `meta` 记录。
- 修改前与用户确认。