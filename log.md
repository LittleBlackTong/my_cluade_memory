# Wiki 日志

append-only 时间线。每行一个事件，前缀统一以便 grep。

## [2026-08-09] meta   | 创建 wiki 骨架与 CLAUDE.md schema
## [2026-08-09] ingest | 首次摄入：Karpathy LLM Wiki 声明 + 个人 wiki 搭建记录 + 长期记忆边界讨论 → pages/llm-wiki-karpathy.md, pages/setup-llm-wiki-personal.md, pages/long-term-memory-boundary.md, pages/CLAUDE-schema.md, pages/index-catalog.md, pages/log-timeline.md；创建 wiki 的页面 + 内置记忆系统（仅只读，无法直接写入）。用户工作模式确立：每次重要对话由 LLM 主动归档到 wiki。
## [2026-08-09] meta   | 初始化 git 仓库并接入远端 git@github.com:LittleBlackTong/my_cluade_memory.git；写入 CLAUDE.md "Git 与远端同步" 章节，约定本地 commit 由 LLM 执行、远端 push 由用户手动执行（沙箱 ssh 凭据隔离）；新增 .gitignore。
## [2026-08-09] meta   | 建立 agent 身份"小 C"：创建 user-profile.md（用户档案）+ feedback-voice-style.md（中文/逗比/认真/思考偏好），CLAUDE.md 顶部加入"Agent 身份"章节并指定会话开始恢复流程；用户授权 LLM 自主维护 wiki。
## [2026-08-09 15:57 CST] meta | 创建 feedback-time-awareness.md（时间获取意识约定）；CLAUDE.md 恢复流程加入"必读 date"步骤；要求任何写入前先 date 拿权威时间，禁止依赖系统提示 currentDate。
## [2026-08-09 16:00 CST] meta | 时间规则改方案 C（混合）：会话开始 date 一次锚定，连续写入复用直到跨午夜/超时/用户提及时间再 date；feedback-time-awareness.md 与 CLAUDE.md 同步更新。
## [2026-08-09 16:00 CST] meta | 用户报告首次 git push 成功；长期记忆边界页加入"第四层：Git 远端备份"小节，注明沙箱 ssh 限制与手动 push 工作流。