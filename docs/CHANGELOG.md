# 更新日志 · GhostAI

## 2026-05 · 0.3.0

- 🎁 **联盟分销系统上线**：推广链接首单返 30%，公开业绩面板，每周一手动转账
- 🛡️ **加固完成**：Qdrant ulimit 修复、安全响应头（HSTS/X-Frame/CSP）、订单限速、磁盘监控、待付订单 7 天自动过期
- 📦 **数据备份**：PG + Dify storage + Qdrant + 配置全套 nightly NAS 备份，sha256 三处校验

## 2026-05 · 0.2.0

- 💳 **半自动收款**：自助下单 → 显示金额 + 收款码 → 客户上传付款截图 → admin 后台一键激活
- 📧 **续费邮件**：到期前 3 天邮件提醒 + 一键续费链接（HMAC 签名 14 天 TTL）
- 📊 **admin 后台**：订单 / 客户 / 套餐 / 配额 / 邮件全套 CRUD
- 🔒 **session 持久化**：admin 会话签名 cookie，服务重启不掉登录
- 🔌 **支付方案可切换**：易支付协议（虎皮椒兼容）+ 支付宝官方 API 备份

## 2026-05 · 0.1.5

- 🎨 **品牌白标**：Dify → GhostAI（logo / manifest / 可见文字全替换）
- 🌐 **公网域名**：https://www.ghostai.top（DigiCert TLS 1.3）
- 🔧 **frp 隧道**：家服 ↔ VPS 反向代理，国内合规接入
- 📈 **客户配额**：tokens / docs / apps 三维监控 + 自动提醒

## 2026-05 · 0.1.0

- 🚀 **首发**：基于 Dify 内核 + DeepSeek V4 + bge-m3 + Qdrant 国内部署
- 📚 **多租户**：每客户独立 workspace + 数据隔离
- 💼 **三档套餐**：个人 ¥39 / 团队 ¥199 / 企业 ¥999
- 📨 **邮件系统**：163 SMTP，welcome / 续费 / 到期提醒 / 配额提醒模板齐全

---

订阅更新：[公众号 GhostAI · 官网](https://www.ghostai.top)
