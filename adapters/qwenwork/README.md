# QwenWork 平台适配原则

- 核心规则仍使用根目录 `SKILL.md`。
- 如果平台支持网页检索，则执行公开搜索模式。
- 如果不支持登录态浏览器，LinkedIn / 社媒无法访问的部分标记为 `PARTIAL / BLOCKED`。
- `BUSINESS_CONTEXT` 由上层业务 Agent 动态传入。
- 平台专有工作流只放在本适配目录，不修改核心 Skill。
