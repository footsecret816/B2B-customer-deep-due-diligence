# 安全与凭据管理

## 严禁提交到 GitHub 的内容

- 用户名 / 密码
- 浏览器 Cookie
- Session Token
- API Key
- OAuth Token
- LinkedIn / Facebook / Instagram 等登录凭据
- 付费数据平台账号信息
- 客户未授权的敏感资料

## 登录型网站

如果 AI 平台支持授权浏览器：

1. 由用户本人完成登录或授权；
2. Skill 只定义“进入哪个页面、查询什么、提取什么”；
3. 凭据与会话由平台安全环境保存；
4. 不得把会话信息写回仓库。

## GitHub 建议

如本 Skill 后续加入公司内部专有流程、客户判断规则、权限逻辑或其他内部知识，建议设置为 Private Repository。
