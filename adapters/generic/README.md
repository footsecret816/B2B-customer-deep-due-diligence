# 通用平台适配

适用于支持以下任一能力的平台：

- 系统提示词 / 自定义指令
- Skill / Tool / Workflow
- Web Search
- Browser / Computer Use

## 最低适配

1. 把根目录 `SKILL.md` 设为主能力说明。
2. 允许模型按需读取 `references/`。
3. 开启公开网页搜索。
4. 无浏览器能力时，无法访问的页面必须按 `BLOCKED / PARTIAL` 处理。
5. 最终输出使用 `templates/customer_profile.md`。
