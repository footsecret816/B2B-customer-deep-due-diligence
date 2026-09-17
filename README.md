# B2B 客户深度背调 Skill

> 面向外贸 B2B 场景的标准化客户背调能力包：用固定 SOP 核验客户主体、官网、工商、域名、网站历史、地图、LinkedIn、Facebook、Instagram、YouTube、TikTok、行业/展会/合作信号与公开风险，并通过多源交叉验证减少漏查、误判和 AI 每次搜索不一致的问题。

## GitHub 仓库描述（建议直接复制）

**外贸B2B客户深度背调 Skill：用固定SOP核验官网、工商、域名、Archive、Maps、LinkedIn及主流社媒，识别客户画像、关键人、市场与风险，多源交叉验证减少漏查与AI随机性，并支持业务Agent动态注入公司上下文。**

## 这个 Skill 能干什么

- 确认客户主体是否真实，避免同名公司串档。
- 深挖官网：公司历史、产品、品牌、渠道、市场、地址、联系方式、法律主体。
- 查询公开工商/注册资料，核验公司状态、成立时间和注册地址。
- 轻量核验 RDAP / WHOIS 与 Archive 历史，判断网站连续性与异常变化。
- 核验 Maps / 公开商户信息中的地址、电话、官网和实体经营信号。
- 固定扫描 LinkedIn 公司页及关键岗位：管理层、采购、Sourcing、Category / Product 等。
- 固定扫描 Facebook、Instagram、YouTube、TikTok；所有平台先做存在性扫描，仅对活跃平台继续深挖。
- 搜索展会、行业协会、合作伙伴、经销网络、零售渠道等 B2B 市场信号。
- 执行公开诉讼、破产、诈骗、投诉、付款等风险检索，并按证据等级判断。
- 对公司主体、地址、历史、主营、规模、人员、市场、风险做多源交叉验证。
- 输出固定结构 `CUSTOMER_PROFILE`，便于上层业务 Agent 继续做产品匹配、客户价值判断和开发策略。

## 核心优势

1. **稳定**：不是“让 AI 随便搜”，而是固定渠道、固定字段、固定停止条件。
2. **轻量**：保留原背调 SOP 的免费渠道，但降低默认深挖程度，避免每个客户都做成审计项目。
3. **跨平台**：核心规则全部放在平台无关的 Markdown 中，不依赖某一家 AI 平台的专有格式。
4. **可组合**：本 Skill 只负责公开信息背调；海关数据、报价、邮件等能力可作为独立 Skill 由上层 Agent 组合调用。
5. **不绑死公司产品**：不在 Skill 内硬编码供应商产品清单；上层业务 Agent 可动态传入 `BUSINESS_CONTEXT`。
6. **降低幻觉**：统一使用 FOUND / PARTIAL / NOT_FOUND / BLOCKED / CONFLICT / UNVERIFIED 等状态，查不到就明确写查不到。
7. **保留证据链**：重要结论必须附来源；企业自述与第三方事实分开表达。

## 不包含什么

本仓库默认不包含：

- 付费海关数据库；
- 超迹海关查询；
- Panjiva / ImportGenius 等付费贸易数据库；
- D&B / Creditsafe 等付费征信；
- Similarweb Pro；
- LinkedIn Sales Navigator；
- 任何账号密码、Cookie、Session、API Key。

海关数据建议独立做成 `Customs / Trade Data Skill`，由业务 Agent 在需要时追加调用。

## 仓库结构

```text
b2b-customer-due-diligence-skill/
├─ README.md
├─ AGENTS.md
├─ SKILL.md
├─ skill.yaml
├─ DESIGN.md
├─ CHANGELOG.md
├─ SECURITY.md
├─ references/
│  ├─ 01_execution_protocol.md
│  ├─ 02_channel_matrix.md
│  ├─ 03_linkedin_protocol.md
│  ├─ 04_social_media_protocol.md
│  ├─ 05_evidence_rules.md
│  ├─ 06_business_context_interface.md
│  └─ 07_output_schema.md
├─ templates/
│  └─ customer_profile.md
├─ examples/
│  └─ quick_start.md
├─ evals/
│  └─ test_checklist.md
└─ adapters/
   ├─ README.md
   ├─ generic/README.md
   ├─ openai/README.md
   ├─ accio/README.md
   ├─ qwenwork/README.md
   └─ workbuddy/README.md
```

## 推荐使用方式

### 方式 A：由现有业务 Agent 调用（推荐）

业务 Agent 已掌握公司产品、MOQ、客户定位、OEM/ODM 能力等知识；调用本 Skill 时，把本次相关的业务关注点通过 `BUSINESS_CONTEXT` 动态传入。

本 Skill：

1. 先客观调查客户；
2. 建立完整客户画像；
3. 如收到 `BUSINESS_CONTEXT`，再做一轮有针对性的补充信息采集；
4. 返回 `CUSTOMER_PROFILE`。

最终的“与我司匹配度、推荐产品、开发优先级、开发话术”由上层业务 Agent 负责。

### 方式 B：独立运行

没有上层业务 Agent 时，本 Skill 仍可独立工作，只输出客观客户画像，不强行判断与某一家供应商的匹配度。

## 跨平台适配原则

本仓库把 `SKILL.md` 作为唯一核心能力定义，其他文件只是引用资料和平台适配说明。

- 平台支持 Skill / 能力包：把 `SKILL.md` 作为主入口。
- 平台只支持系统提示词 / 自定义指令：把 `SKILL.md` 作为主指令，并按需加载 `references/`。
- 平台支持浏览器：允许按 SOP 打开网页、Maps、LinkedIn 等公开页面。
- 平台不支持浏览器但支持 Web Search：执行公开搜索模式，无法访问的页面标记为 `BLOCKED` / `PARTIAL`。
- 平台支持已登录浏览器：可在用户授权登录后执行更完整的 LinkedIn 等页面调查，但账号凭据不能写入仓库。

## 快速输入示例

```text
请背调以下客户：
公司名：ABC Footcare Ltd
国家：英国
官网：https://example.com
联系人：John Smith
邮箱：john@example.com

按 L2 标准背调执行。
```

如由业务 Agent 调用，可追加：

```text
BUSINESS_CONTEXT:
- 当前公司产品能力：由业务 Agent 动态提供
- 本次重点关注：自有品牌、Private Label、采购岗位、足护理相关产品
- 不改变第一轮客观调查范围
```

## 版本策略

- 核心方法变化：更新 `SKILL.md` 与 `DESIGN.md`。
- 单一渠道查询方式变化：优先更新 `references/`。
- 平台接入差异：只修改 `adapters/`，不改核心 Skill。
- 公司产品、客户定位等业务知识变化：更新业务 Agent，不修改本 Skill。
