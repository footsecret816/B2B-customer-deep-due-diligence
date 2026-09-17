# 平台适配说明

本目录只负责“如何把同一套核心 Skill 接到不同 AI 平台”，不修改业务逻辑。

核心规则永远以仓库根目录 `SKILL.md` 为准。

不同平台只需要解决三件事：

1. 如何加载 `SKILL.md`；
2. 如何提供 Web Search / Browser / Maps 等工具；
3. 如何把业务 Agent 的 `BUSINESS_CONTEXT` 传给 Skill。

不要把平台专有逻辑写回核心 Skill。
