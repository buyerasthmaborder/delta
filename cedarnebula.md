# NexusIndex

NexusIndex 是一个面向技术内容创作者与资源整理者的轻量级外链聚合与导航工具。项目定位为“技术资源的索引中间层”，聚焦于将分散在网络各处的优质外链、社区入口、媒体资源与文档站点进行结构化收录，并通过清晰的目录树与分类体系，降低团队内部或公开社区中信息检索的流转成本。NexusIndex 不存储任何实体文件，仅提供链接的元信息管理与快速跳转能力，适用于个人知识库、开源项目文档站、技术社群资源页等场景。

## 功能概览

- **多级目录资源分类**：支持按主题、地区、文件类型、语言、完整度等维度建立自定义分类树，每条资源可归属多个标签，便于交叉筛选。

- **外链存活检测**：内置定时任务，每日对收录的 URL 进行 HEAD 请求检测，标记失效链接并生成报告，帮助维护资源库的可用性。

- **Markdown 原生配置**：所有资源列表与分类规则以 Markdown 文件形式存储，支持 Git 版本管理，便于多人协作审阅与回滚。

- **静态站点生成**：提供内置的构建命令，可将资源目录一键渲染为纯静态 HTML 页面，适配 GitHub Pages、Cloudflare Pages 等托管服务。

- **快速检索与过滤**：前端支持按关键字、分类标签、添加时间、状态（有效/失效）进行实时搜索，降低海量链接中的定位耗时。

- **导入与导出接口**：支持批量导入 CSV / JSON 格式的链接清单，并支持导出为结构化 Markdown 表格或 JSON API 格式，方便对接其它系统。

- **访问统计看板**：记录每个外链的点击次数与最后访问时间，辅助判断资源热度，但不会采集用户个人隐私信息。

## 应用场景

- **开源项目文档站的外链附录**：当开源项目需要引用大量第三方依赖文档、社区论坛、示例仓库时，可使用 NexusIndex 生成独立的资源导航页，避免 README 过长且难以维护。

- **技术社群的知识沉淀仓库**：技术交流群组或内部团队可将长期积累的问答链接、工具站点、视频教程通过 NexusIndex 统一归档，新成员可快速了解可用资源全貌。

- **个人技术博客的友情链接管理**：博主可将合作站点、投稿渠道、投稿要求等外链集中存放，并利用失效检测功能定期清理过期友链，保持页面质量。

- **地区性资源专题汇总**：针对特定区域的内容（如地区性社区、本地化视频源、语言字幕组），可利用分类标签建立专题视图，便于按地域或语言筛选。

## 快速开始

以下命令可在本地快速启动 NexusIndex 开发实例。

```bash
# 克隆仓库
git clone https://github.com/nexusindex/nexusindex.git

# 进入项目目录
cd nexusindex

# 安装依赖（基于 Node.js 22 LTS）
npm install

# 启动开发服务器（默认端口 3000）
npm run dev
```

访问 `http://localhost:3000` 即可查看本地资源导航页面。修改 `./resources` 目录下的 Markdown 文件后，页面将自动热重载。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 22.x LTS 或更高 | 运行时环境，用于执行构建与服务脚本 |
| npm | 10.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.40 或更高 | 版本控制，用于克隆仓库及提交变更 |
| 内存 | 最低 512MB，推荐 1GB | 开发模式下内存占用约 300MB，生产构建约 600MB |
| 磁盘空间 | 至少 200MB | 包含依赖包与构建缓存，资源文件不占用额外存储 |
| 操作系统 | Linux / macOS / Windows WSL2 | 跨平台支持，Windows 原生环境需配置 PowerShell 执行策略 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `/docs/user-guide/` | 如何添加、编辑、删除资源链接？如何批量导入导出？如何查看失效报告？ |
| 管理员手册 | `/docs/admin/` | 如何配置定时检测间隔？如何自定义分类标签？如何备份资源数据？ |
| 开发者文档 | `/docs/developer/` | 如何扩展解析器？如何替换前端主题？如何编写自定义过滤器插件？ |
| 部署运维 | `/docs/deployment/` | 如何部署到云服务器？如何配置反向代理？如何启用 HTTPS 强制跳转？ |

## 资源列表

### 社区与社群

<code>bendiyueaisheququnzu.com.cn</code>

### 应用与工具

<code>siyueapp.com.cn</code>

### 视频媒体（清晰度）

<code>renqiwumagaoqingshipin.com.cn</code>

### 视频媒体（地区专题）

<code>ribenwumarenqizhuanqu.com.cn</code>

### 视频媒体（字幕）

<code>renqiwumazhongwenzimu.com.cn</code>

### 视频媒体（完整版）

<code>renqiwumawanzhengban.com.cn</code>

## 项目结构

```
nexusindex/
├── config/                     # 全局配置文件目录
│   ├── app.config.json         # 应用名称、默认语言、分页大小等
│   └── categories.yaml         # 预置分类标签与颜色映射
├── resources/                  # 核心资源数据目录（Markdown 存储）
│   ├── community/              # 社区与社群类资源（含地区子目录）
│   │   └── local/              # 本地社群链接清单
│   ├── applications/           # 应用与工具类资源
│   │   └── mobile/             # 移动端应用索引
│   ├── media/                  # 视频与媒体类资源
│   │   ├── hd/                 # 高清晰度视频源
│   │   ├── regional/           # 地区专题视频（如日本专题）
│   │   ├── subtitle/           # 字幕相关资源
│   │   └── full/               # 完整版视频入口
│   └── index.md                # 资源总览与默认视图
├── src/                        # 源代码目录
│   ├── core/                   # 核心解析与索引引擎
│   │   ├── parser.js           # Markdown 资源解析器
│   │   └── detector.js         # 外链存活检测模块
│   ├── server/                 # 开发服务器与热重载逻辑
│   │   └── dev-server.js       # 基于 Express 的开发服务
│   ├── build/                  # 静态站点生成器
│   │   └── static-generator.js # 渲染 HTML 输出
│   └── frontend/               # 前端界面资源（JS / CSS）
│       ├── search.js           # 客户端搜索与过滤逻辑
│       └── theme.css           # 默认主题样式
├── tests/                      # 单元测试与集成测试
│   ├── parser.test.js          # 解析器测试用例
│   └── detector.test.js        # 存活检测测试用例
├── docs/                       # 项目文档（用户指南、管理员手册、开发者文档、部署运维）
│   ├── user-guide/
│   ├── admin/
│   ├── developer/
│   └── deployment/
├── .github/                    # GitHub 相关配置
│   └── workflows/              # CI 流水线（自动检测 + 构建）
├── package.json                # npm 依赖与脚本定义
└── README.md                   # 项目入口说明（本文件）
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。请确保使用最新的 `main` 分支作为基线。

2. 在 `resources/` 目录下按分类新增或修改 `.md` 文件，并遵守既定的 Front Matter 格式（标题、标签、URL、添加时间等字段）。新增资源需通过 `npm run validate` 校验格式。

3. 提交变更前请运行 `npm run test` 确保所有单元测试通过，并执行 `npm run build` 验证静态站点生成无报错。

4. 发起 Pull Request 至 `main` 分支，并在 PR 描述中说明变更内容、涉及分类以及是否关联 Issue。PR 至少需要一名维护者审核通过。

5. 若涉及新增分类标签或修改配置结构，请同步更新 `/docs/admin/` 下的对应文档，确保手册与代码保持一致。

## 常见问题

**Q：检测到失效链接后，系统会自动删除该条目吗？**

不会。NexusIndex 仅标记失效状态并在看板中高亮显示，同时生成失效报告供管理员审阅。删除操作需由管理员手动确认，避免误判（例如临时维护的站点被误报失效）。

**Q：如何自定义前端页面颜色和 Logo？**

所有主题变量定义在 `src/frontend/theme.css` 中，您可以直接覆盖 CSS 变量（如 `--primary-color`、`--header-bg`）。Logo 图片请放置于 `src/frontend/assets/` 目录，并在 `config/app.config.json` 中配置 `logoPath` 字段。

**Q：支持多语言界面吗？**

当前版本仅提供中文界面，但架构已预留国际化接口。您可以在 `config/app.config.json` 中启用 `i18n.enabled`，并参考 `docs/developer/i18n.md` 添加其它语言的翻译文件。官方计划在 v2.0 版本正式支持中英文切换。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-08-24 21:34:14
