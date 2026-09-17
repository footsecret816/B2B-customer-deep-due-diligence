# Agent 使用入口

任何 AI Agent、Coding Agent 或工作流在使用本仓库时，应按以下顺序读取：

1. `SKILL.md` —— 核心执行规则，优先级最高。
2. `references/01_execution_protocol.md` —— 主流程与节点说明。
3. 按任务需要读取其他 `references/`，不要一次性把所有参考文件塞进上下文。
4. 最终输出遵循 `references/07_output_schema.md` 与 `templates/customer_profile.md`。

## 强制规则

- 不得跳过 L2 的核心必查模块。
- 不得把企业官网自述直接写成已验证事实。
- 不得把同名公司信息混入目标客户。
- 不得因为某个平台打不开就伪造结果。
- 不得把“未搜索到负面信息”写成“没有风险”。
- 不得把域名注册时间当成公司成立时间。
- 不得在本仓库保存账号、密码、Cookie、Session、API Key。
- 海关数据不属于本 Skill，除非上层 Agent 另外调用独立海关 Skill 并把结果作为外部证据传入。
- 如收到 `BUSINESS_CONTEXT`，第一轮仍必须先客观调查客户；业务上下文只用于第二轮定向补充，不得让供应商产品清单限制客户调查范围。
