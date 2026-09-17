# OpenAI 平台适配原则

本文件仅说明通用映射，不依赖某一版本界面。

- 核心指令：使用根目录 `SKILL.md`。
- 参考资料：按需读取 `references/`。
- 如运行环境提供 Web / Browser / Computer Use，则按 Skill 的渠道协议调用。
- 上层业务 Agent 调用时，通过上下文传入 `BUSINESS_CONTEXT`。
- 不要把公司完整产品知识复制进本 Skill。
- 不要把账号凭据写入仓库。
