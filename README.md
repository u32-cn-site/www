# U32 智能服务平台（u32-www-2026）

私有主仓，收纳 u32.cn 根域门户。公开站点把 `homepage/` 经 `git subtree` 同步到 GitHub `u32-cn-site/www`，经 GitHub Actions → Pages 部署，EdgeOne 回源 GitHub Pages 分发到 `u32.cn/`。

## 目录结构

```
u32-www-2026/
├── README.md                 # 本文件
├── AGENTS.md                 # AI 执行纪律
├── .gitignore
└── homepage/                 # 静态站点（subtree 推 GitHub 公开仓）
    ├── index.html            # u32.cn 根域门户首页（内联 CSS/JS，自足单文件）
    ├── public-list.json      # 根域公开列表（sync.js 生成物，勿手改）
    ├── favicon* / apple-touch-icon.png
    ├── 178d...txt / 1c24...txt  # 平台验证文件，勿删改
    ├── .nojekyll
    └── .github/workflows/static.yml  # Pages 部署流水线
```

## 子应用（m/，不在本仓）

根域子应用集合（aichat/aichat2/aifile/info/jinfei/zyj）**不入 git**，存阿里云 OSS：

- OSS：`u32-cn-data/_inner_/bigdata/20261124-u32-cn-m/data/<应用名>/`
- 公网：`https://u32.cn/m/<应用名>/`（EdgeOne 规则引擎 `^/m/(.*)$` 重写到上述 OSS 前缀）
- OSS 侧说明文档：`u32-cn-data/_inner_/bigdata/20261124-u32-cn-m/README.md`
- 备份：百度网盘 `personal/`（JSL 条目）

## 发布链路

```
homepage/ → git subtree push --prefix homepage github main
         → GitHub Actions → Pages https://u32-cn-site.github.io/www/
         → EdgeOne 回源（规则引擎 HostHeader→u32-cn-site.github.io + 重写 → /www/$1）
         → https://u32.cn/
```

- 公开仓：`git@github.com:u32-cn-site/www.git`（空仓，不勾 README/.gitignore/License）
- 私有仓远端：`codeup` = `git@codeup.aliyun.com:jinfei/2026/u32-www-2026.git`
- 同步命令：`git subtree push --prefix homepage github main`

## 迁移背景（2026-11-24）

自 ai-pages-2026 `pages/p/www` 迁出（参照 u32-kid-2026 模式）：

- 根域首页改走 GitHub Pages 回源；子应用 m/ 走 OSS bigdata 独立前缀
- OSS `_inner_/zt/p/www/web/` 旧静态分发在切换验证通过后删除
- EdgeOne `/m/`、`/zt/`、`/bd/`、`/api/` 路径规则按迁移方案调整，兼容路径不变

## 注意事项

- `homepage/` 内禁止放大数据文件与密钥（公开仓，推送前隐私扫描）
- 更新首页：改 `homepage/` → commit 到本仓 → `git subtree push --prefix homepage github main` → 验证 Pages → 按需 `tccli teo` 刷缓存
- 更新子应用：直接上传 OSS 对应前缀，不动 git；`m/info/czm/ion_token.*` 含 Cesium token，只许存 OSS，禁止入任何 git 仓
