# Wiki 日志

append-only 时间线。每行一个事件，前缀统一以便 grep。

## [2026-08-09] meta   | 创建 wiki 骨架与 CLAUDE.md schema
## [2026-08-09] ingest | 首次摄入：Karpathy LLM Wiki 声明 + 个人 wiki 搭建记录 + 长期记忆边界讨论 → pages/llm-wiki-karpathy.md, pages/setup-llm-wiki-personal.md, pages/long-term-memory-boundary.md, pages/CLAUDE-schema.md, pages/index-catalog.md, pages/log-timeline.md；创建 wiki 的页面 + 内置记忆系统（仅只读，无法直接写入）。用户工作模式确立：每次重要对话由 LLM 主动归档到 wiki。
## [2026-08-09] meta   | 初始化 git 仓库并接入远端 git@github.com:LittleBlackTong/my_cluade_memory.git；写入 CLAUDE.md "Git 与远端同步" 章节，约定本地 commit 由 LLM 执行、远端 push 由用户手动执行（沙箱 ssh 凭据隔离）；新增 .gitignore。