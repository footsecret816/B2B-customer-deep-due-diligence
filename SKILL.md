---
name: b2b-customer-due-diligence
version: 1.0.0
language: zh-CN
description: 面向外贸B2B客户的标准化深度背调能力。固定核验官网、公开注册、域名、网站历史、地图、LinkedIn、Facebook、Instagram、YouTube、TikTok、行业市场信号及公开风险，并通过多源交叉验证输出可追溯客户画像，减少漏查与AI随机性。
---

# B2B 客户深度背调 Skill

## 1. 目标

对 B2B 潜在客户执行稳定、可重复、可追溯的公开信息背调。

本 Skill 负责回答：

- 这家公司是谁，主体是否真实？
- 官网、地址、注册主体、联系方式是否相互匹配？
- 公司经营什么产品、什么品牌、什么渠道、什么市场？
- 公司规模与市场活跃度有哪些公开信号？
- 谁可能是管理层、采购、Sourcing、Category / Product 相关人员？
- Facebook、Instagram、YouTube、TikTok 哪些是其实际活跃阵地？
- 是否存在公开诉讼、破产、诈骗、投诉、付款等风险信号？
- 哪些结论已经验证，哪些仍有冲突或信息缺口？

本 Skill 不负责最终销售决策。产品匹配、客户价值、MOQ 适配、开发优先级和推荐产品由上层业务 Agent 完成。

## 2. 默认模式

默认执行 **L2 标准背调**。

L1：快速背调，仅用于初筛。
L2：标准背调，日常默认。
L3：深度背调，仅在重要客户或异常信号触发时追加。

## 3. L2 核心主流程

按顺序执行：

1. J1 客户主体确认
2. J2 官网调查
3. J3 公开网页搜索
4. J4 公开工商 / 企业注册核验
5. J5 域名快速核验
6. J6 Archive 网站历史快速核验
7. J7 Maps / 地址实体核验
8. J8 LinkedIn 公司与关键人员
9. J9 社交媒体矩阵扫描：Facebook / Instagram / YouTube / TikTok
10. J10 行业 / 展会 / 合作 / 渠道信号
11. J11 公开风险调查
12. C1 多源交叉验证
13. J12 判断是否触发 L3 深挖
14. O1 输出 `CUSTOMER_PROFILE`

不得因为“信息已经很多”而自行跳过 J1-J11。

## 4. 信息状态

所有核心字段必须保留，查不到也要保留状态：

- `FOUND`：找到明确有效信息
- `PARTIAL`：仅找到部分信息
- `NOT_FOUND`：已执行规定检索但未找到
- `BLOCKED`：登录墙、权限、反爬或技术限制导致无法访问
- `NOT_PUBLIC`：确认属于非公开信息
- `UNVERIFIED`：只有单一来源或证据不足
- `CONFLICT`：可靠来源之间明显冲突
- `N/A`：对当前客户不适用

## 5. 输入

最低输入：

- `Company Name`
- `Country`（如未知可通过调查确认）
- `Website`（如已知）

可选：

- Contact Name
- Email
- Phone
- Address
- Inquiry Product
- Lead Source
- Known Brand
- `BUSINESS_CONTEXT`

## 6. BUSINESS_CONTEXT 使用规则

`BUSINESS_CONTEXT` 为上层业务 Agent 动态传入的公司业务上下文。

它可以包含：

- 当前公司产品能力
- 目标客户类型
- 业务重点
- 本次特别关注的品类 / 商业信号

强制规则：

1. 第一轮调查不得因 `BUSINESS_CONTEXT` 缩窄客户调查范围。
2. 先建立完整客户画像，再参考 `BUSINESS_CONTEXT` 做第二轮定向补充。
3. 本 Skill 不内置任何特定供应商的完整产品清单。
4. 没有 `BUSINESS_CONTEXT` 时照常完成客观背调。

## 7. 渠道执行原则

### A 类：L2 必查

- 客户官网
- 公开网页搜索
- 官方 / 公开企业注册信息
- RDAP / WHOIS 轻量核验
- Archive / Wayback 轻量核验
- Maps / 公开商户信息
- LinkedIn
- Facebook
- Instagram
- YouTube
- TikTok
- 公开风险信息
- 交叉验证

### B 类：必做存在性搜索，有结果再深入

- 行业协会
- 展会
- 合作伙伴
- 经销商 / Dealer
- 零售渠道
- 新闻
- 招聘活动

### C 类：可选免费信号

- Similarweb 免费公开字段
- 其他无需付费即可核验的网站流量 / SEO 信号

C 类渠道若看不到可靠免费数据，应立即停止，不得估算或伪造。

## 8. 社媒原则

Facebook、Instagram、YouTube、TikTok 四个平台均进行存在性扫描。

先确认是否为官方或高度可信账号：

- `CONFIRMED_OFFICIAL`
- `LIKELY_OFFICIAL`
- `UNVERIFIED`
- `NOT_FOUND`

只有 `CONFIRMED_OFFICIAL` 或有充分证据的 `LIKELY_OFFICIAL` 才进入内容分析。

对活跃平台，可抽样最近 12 条公开内容或最近 90 天内容，先达到者为准。

不得把“未找到官方账号”写成“公司没有该社媒”。

## 9. LinkedIn 原则

LinkedIn 固定调查：

- 公司主页 / 公司公开信息
- CEO / Owner / Managing Director
- Buyer
- Purchasing / Procurement
- Sourcing
- Category Manager
- Product Manager

五类采购 / 品类岗位必须全部尝试，不得因为找到一个 Buyer 就停止。

如果只能通过公开搜索获取部分信息，标记 `PARTIAL`；如果登录墙阻挡，标记 `BLOCKED`。

## 10. 风险原则

必须检查公开：

- lawsuit / litigation
- bankruptcy / insolvency
- fraud / scam
- complaint
- unpaid / payment complaint

非英语国家追加当地主要语言对应关键词。

证据优先级：

A：法院 / 政府 / 监管机构 / 官方破产资料
B：主流媒体 / 行业权威
C：评论网站 / 社媒 / 论坛

单独 C 级证据不得直接定性客户信用风险。

## 11. 交叉验证

最终报告前至少核验：

- 公司主体
- 地址
- 企业历史
- 主营业务
- 公司规模信号
- 管理层 / 关键人员
- 市场存在
- 风险信息

状态只使用：

- `VERIFIED`
- `PARTIALLY_VERIFIED`
- `UNVERIFIED`
- `CONFLICT`

出现 `CONFLICT` 时必须展示冲突双方及来源，不得自行隐藏。

## 12. L3 深挖触发

出现以下情况之一，可追加深挖：

- 重要客户 / 大项目 / 账期客户
- 公司历史或主体存在疑点
- 官网、地址、注册信息明显冲突
- 公司声称历史很长但公开证据很少
- 需要确认行业地位、展会、协会、合作网络
- LinkedIn 标准岗位未找到有效联系人
- 社媒存在明显活跃阵地

深挖可包括：

- Archive 多时间节点对比
- 域名详细信息
- 活跃社媒内容深挖
- 更多关键人员
- 行业协会 / 展会 / 合作伙伴深挖

## 13. 输出

最终输出必须遵循 `references/07_output_schema.md`，核心结果为 `CUSTOMER_PROFILE`。

输出必须包含：

- 主体与真实性
- 企业基本情况
- 产品 / 品牌 / 渠道 / 市场
- 规模与市场信号
- LinkedIn 与关键人员
- 四大社媒扫描结果
- 行业 / 展会 / 合作信号
- 风险信息
- 交叉验证
- 信息冲突
- 未验证信息
- 核心来源
- 是否建议追加专项调查

## 14. 禁止事项

禁止：

- 编造不存在的数据、链接、员工、营业额或采购额。
- 将企业官网自述直接写成已验证事实。
- 把域名注册时间当公司成立时间。
- 把同名企业资料混入目标客户。
- 因为 LinkedIn 员工少直接判断公司小。
- 因为没有 LinkedIn / 社媒就判断公司不真实。
- 因为 Maps 显示住宅地址直接判断诈骗。
- 因为没搜到负面信息就写“无风险”。
- 为了报告完整而猜测缺失字段。
- 因为上层业务 Agent 有产品清单，就只调查与产品清单相关的客户业务。
- 调用或假装调用本仓库未配置的付费海关、征信或付费流量数据库。

## 15. 完成门槛

生成“完整 L2 背调报告”前，必须确认：

- J1-J11 均已执行或明确标记 `BLOCKED / NOT_FOUND`
- C1 已完成
- 四大社媒均已做存在性扫描
- 关键结论有来源
- 重要冲突没有被隐藏
- 未验证信息已单独列出

未达到以上条件，不得声称“完整背调已完成”。
