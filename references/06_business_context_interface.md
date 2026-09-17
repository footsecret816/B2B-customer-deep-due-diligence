# 06｜BUSINESS_CONTEXT 接口

## 目的

让本 Skill 可以被已经掌握公司知识的业务 Agent 调用，同时避免把某一家公司的产品知识硬编码在 Skill 内。

## 推荐输入结构

```text
BUSINESS_CONTEXT

Company Capability:
- 由上层业务 Agent 动态提供当前产品 / 服务能力

Target Customer Types:
- 由上层业务 Agent 动态提供

Special Research Focus:
- 本次特别关注的品类、商业信号、渠道或人员

Commercial Constraints:
- 可选，例如 MOQ、认证、目标市场等
```

## 执行顺序

### 第一轮：客观背调

先完整调查客户，不使用供应商产品清单缩窄范围。

输出：

- Customer Product Map
- Brands
- Channels
- Markets
- Own-brand / Private-label Signals
- Key People
- Risk

### 第二轮：定向补充

如果收到 `BUSINESS_CONTEXT`：

1. 将客户画像与公司能力对照；
2. 识别值得继续核实的客户品类 / 商业信号；
3. 仅做必要的补充搜索；
4. 返回额外事实，不直接替上层 Agent 做最终销售判断。

## Skill 与 Agent 的职责边界

### 本 Skill 负责

客户事实、商业画像、公开风险、关键人员、产品与渠道信息、证据链。

### 上层业务 Agent 负责

- 与我司匹配度
- 推荐产品
- 客户价值
- MOQ适配
- 开发优先级
- 开发策略
- 下一步业务动作
