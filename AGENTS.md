# AGENTS.md — AI 执行纪律

- 本仓为私有主仓；公开面只有 `homepage/`（subtree → GitHub 公开仓 `u32-cn-site/www`）。推 subtree 前必须检查 `homepage/` 内无密钥、无本地路径、无个人隐私数据。
- `m/` 子应用不入 git，走 OSS `u32-cn-data/_inner_/bigdata/20261124-u32-cn-m/data/`；`m/info/czm/ion_token.*` 含 Cesium token，禁止入任何 git 仓。
- 修改 `homepage/` 后的发布顺序：commit 本仓 → subtree push → 验证 GitHub Pages → 验证 u32.cn → 按需 `tccli teo` 刷缓存。
- 不重部署已在阿里云运行的任何服务；本仓只管静态站。
- OSS / EdgeOne 操作遵循 ai-pages-2026 README 同款凭证与环境变量。
