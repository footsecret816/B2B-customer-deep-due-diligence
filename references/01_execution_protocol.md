# 01｜标准执行协议

## L2 主流程

```text
J1  客户主体确认
↓
J2  官网调查
↓
J3  公开网页搜索
↓
J4  工商 / 企业注册核验
↓
J5  域名快速核验
↓
J6  Archive历史快速核验
↓
J7  Maps / 地址实体核验
↓
J8  LinkedIn公司与关键人员
↓
J9  四大社媒扫描
↓
J10 行业 / 展会 / 合作 / 渠道信号
↓
J11 公开风险调查
↓
C1  多源交叉验证
↓
J12 深挖触发判断
↓
O1  CUSTOMER_PROFILE
```

## J1 主体确认

最低输入：公司名；国家和官网有则使用。

固定搜索：

- `"<公司名>" "<国家>"`
- `"<公司名>" "<官网域名>"`（官网已知）
- `"<公司名>" "<城市>"`（城市已知）

必须输出：

- 最可信公司名称
- 国家
- 官网
- 地址
- 邮箱域名
- 品牌
- 是否存在同名企业
- `RESOLVED / PARTIALLY_RESOLVED / UNRESOLVED`

## J2 官网

必查：

- Homepage
- About
- Products / Services
- Contact

检查是否存在并按需读取：

- Brands
- Locations / Stores
- News / Blog
- Careers
- Distributor / Dealer
- Footer / Terms / Privacy / Legal Notice

提取：公司名、法律主体、品牌、企业自述成立时间、历史、总部、地点、电话、邮箱、产品、渠道、市场、自有品牌、代理品牌、最近活动。

## J3 公开网页搜索

固定核心 Query：

1. `"<公司名>" "<国家>"`
2. `"<公司名>" products`
3. `"<公司名>" brands`
4. `"<公司名>" distributor retailer`
5. `"<公司名>" news`
6. `"<公司名>" LinkedIn`
7. `"<公司名>" lawsuit complaint`
8. `"<公司名>" bankruptcy fraud scam`

## J4 企业注册

优先顺序：

政府官方注册数据库 → 政府开放企业资料 → 可靠公开商业资料。

重点字段：注册名称、注册号、公司状态、成立日期、注册地址、公开董事/负责人。

## J5 域名快速核验

默认只取：

- Domain
- Creation Date
- Registrar
- Domain Status

异常时才追加 Registrant、更新时间、Name Server 等。

## J6 Archive快速核验

默认只确认：

- 是否有历史快照
- 最早可见年份
- 最早记录的业务是否大体一致

出现历史疑点时进入 L3：最早 / 中间 / 近期多时间节点对比。

## J7 Maps / 地址

固定搜索：

- `"<公司名>" "<城市>"`
- `"<公司名>" "<官方地址>"`

核验：公司名、地址、电话、官网、营业状态、类别、公开照片。

地图环境只能作为辅助证据。

## J8 LinkedIn

详见 `03_linkedin_protocol.md`。

## J9 社媒

详见 `04_social_media_protocol.md`。

## J10 行业 / 展会 / 合作 / 渠道

固定存在性搜索：

- `"<公司名>" exhibition`
- `"<公司名>" trade show`
- `"<公司名>" association`
- `"<公司名>" partnership`
- `"<公司名>" distributor`
- `"<公司名>" dealer`
- `"<公司名>" retailer`

有有效结果才深入。

## J11 风险

核心搜索：

- lawsuit / litigation
- bankruptcy / insolvency
- fraud / scam
- complaint
- unpaid / payment complaint

非英语国家追加当地主要语言。

## C1 交叉验证

至少核验：主体、地址、历史、主营、规模信号、管理层/关键人、市场存在、风险。

## J12 深挖触发

重要客户、历史疑点、地址冲突、官网新旧异常、LinkedIn找不到有效联系人、社媒活跃、行业地位需要验证时触发 L3。
