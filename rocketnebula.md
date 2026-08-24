# 外链引力场 - LinkGravity

外链引力场（LinkGravity）是一个面向中文互联网内容创作者、SEO 工程师与独立站长的外链资源聚合与导航工具集。本项目不生产内容，而是系统性地整理、分类与维护高价值外链入口，帮助用户快速定位特定垂直领域的内容分发渠道、读者社区与引用源。项目定位为“外链的变电站”，将零散的网址转化为可检索、可审计、可追踪的结构化资源池，适用于网站权重建设、内容推广初期冷启动以及竞品外链画像分析等场景。

本项目以静态站点方式提供资源导航，所有外链数据均存储于单一 JSON 文件中，支持通过 GitHub Action 定时更新失效检测，并输出可视化状态面板。目标用户为日均 UV 低于 5 万的个人站长、垂直领域内容编辑以及独立开发者。

## 功能概览

- **多维度外链分类索引**：按行业垂直（文学、社交、直播、地方门户等）提供二级分类导航，每一条外链均附带站点描述、预估流量等级与备案信息。

- **外链活性状态检测**：每日 03:00（UTC+8）自动发起 HEAD 请求，标记响应码非 200 的链接为“待复核”，状态变化记录至变更日志文件。

- **批量外链导出与过滤**：支持按状态码、域名后缀（.cn / .com / .net）、是否包含特定关键词等条件过滤并导出 CSV 或 Markdown 表格，便于嵌入周报。

- **反链关系可视化**：基于站点间的互引数据（需手动维护引用关系表）生成简易力导向关系图，输出为 HTML 静态页面，帮助识别内容枢纽节点。

- **外链变更通知订阅**：通过 RSS 或邮件（需自行配置 SMTP）推送新增、失效及恢复链接的每日摘要，维持团队内部信息同步。

- **资源离线存档提示**：对连续 7 天检测失效的站点，自动将其完整 HTML 首页归档至可配置的 S3 兼容存储，保存快照以作历史参考（默认保留 30 天）。

## 应用场景

- **垂直领域内容站点的冷启动外链建设**：新上线一个文学评论博客，需要在短期内获取首批高质量引用来源。编辑可使用本项目的“文学/连载”分类快速筛选出 20-30 个潜在互推站点，并通过导出功能生成推广优先级列表。

- **SEO 外链审计与竞品分析**：运营人员定期导出本项目的全部外链状态报表，与竞品的外链工具数据进行交叉比对，识别对方新增的引用来源，并同步更新自身的外链补充计划。

- **社群内容分发渠道管理**：社区运营需要将每周精选内容手动推送至多个 UGC 平台与兴趣社区。本项目提供“社交/交友”分类下的平台入口列表，配合状态检测避免点击失效链接，节省日常轮询时间。

- **内容安全与合规自查**：法务或合规团队需要定期检查站点引用的外部资源是否涉及违规域名。项目支持按关键词黑名单过滤外链列表，并输出风险警示标记，用于内部合规简报。

## 快速开始

以下步骤帮助您在本地完整运行本项目的外链数据同步与检测流程。

```bash
# 1. 克隆项目仓库
git clone https://github.com/linkgravity/linkgravity-core.git
cd linkgravity-core

# 2. 安装依赖（项目使用 Python 3.11 + poetry 管理）
pip install poetry
poetry install --no-dev

# 3. 执行外链状态检测并生成静态站点
poetry run python manage.py crawl --source data/links.json --output public/index.html
poetry run python manage.py export --format csv --out report.csv

# 本地预览生成站点（默认监听 8000 端口）
poetry run python -m http.server --directory public
```

## 安装要求

本项目运行环境依赖以下组件，请确保部署前已正确准备。

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.11.x | 核心运行环境，建议使用 pyenv 管理 |
| Poetry | 1.7.1 或更高 | 依赖管理与打包工具 |
| Git | 2.30+ | 用于克隆仓库及版本回退 |
| 网络带宽 | 出站 1 Mbps+ | 执行批量 HEAD 请求需要稳定的公网出口 |
| 存储空间 | 建议 2 GB 以上 | 存放 JSON 数据、归档快照及生成静态文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide/classification.md | 如何理解项目的分类体系？如何快速查找某类外链？ |
| 运维手册 | /docs/ops/health-check.md | 状态检测的具体原理、超时阈值如何调整？失效归档如何恢复？ |
| 开发手册 | /docs/dev/schema.md | links.json 的数据结构定义，新增字段如何兼容？ |
| 贡献指南 | /docs/contributing/standard.md | 提交新外链的审核标准、PR 模板与合并流程 |

## 资源列表

以下为本项目收录的全部外链资源入口，按类别分组展示。所有 URL 均取自用户原始数据，未做任何改写。

**文学 / 连载类**

- <code>chuguiriji.com.cn</code>
- <code>chengrenxiaoshuolianzai.com.cn</code>
- <code>renqichuguiriji.com.cn</code>

**社交 / 交友平台类**

- <code>chengrenzhibopingtaipaixing.com.cn</code>
- <code>tongchengshaofuyueai.com.cn</code>
- <code>yueaishequjiaoyoupingtai.com.cn</code>

## 项目结构

```text
linkgravity-core/
├── config/                         # 全局配置文件目录
│   ├── settings.yaml               # 检测超时、重试策略、归档保留时长
│   └── blacklist.keywords          # 合规过滤关键词列表，一行一个
├── data/                           # 核心数据目录
│   ├── links.json                  # 主外链库，含分类、描述、添加日期
│   ├── refs.graph                  # 站点间互引关系边表（手动维护）
│   └── archives/                   # 失效站点快照存储目录
│       └── 2026/                   # 按年月份归档
├── src/                            # 源代码目录
│   ├── crawler/                    # 状态检测模块
│   │   ├── agent.py                # 异步 HEAD 请求调度器
│   │   └── recorder.py             # 状态变化日志写入器
│   ├── exporter/                   # 导出模块
│   │   ├── csv_writer.py           # CSV 格式导出
│   │   └── md_builder.py           # Markdown 报告生成
│   ├── visualizer/                 # 关系图生成模块
│   │   ├── graph_builder.py        # 使用 networkx 构建力导向图
│   │   └── template.html           # 输出 HTML 模板
│   └── watcher/                    # 变更检测与通知模块
│       ├── diff.py                 # 比较两次检测结果的差异
│       └── notifier.py             # 邮件/RSS 推送接口
├── tests/                          # 单元测试与集成测试
│   ├── test_agent.py
│   └── test_exporter.py
├── scripts/                        # 运维辅助脚本
│   ├── init_db.sh                  # 初始化 JSON 数据文件
│   └── deploy_ghpages.sh           # 构建后自动推送至 GitHub Pages
├── public/                         # 生成的静态站点根目录
│   ├── index.html                  # 主仪表板页面
│   └── graph/                      # 关系图输出目录
├── pyproject.toml                  # Poetry 项目描述文件
├── manage.py                       # CLI 统一入口命令
└── README.md                       # 项目说明文档（本文件）
```

## 贡献指南

我们欢迎任何形式的外链资源补充、分类调整或检测逻辑优化。请遵循以下步骤：

1.  **查阅现有分类与数据规范**：在提交新增外链前，先阅读 `/docs/dev/schema.md` 确认 JSON 字段含义，并检查现有列表避免重复。新增域名需确保其内容主题符合该分类定义。

2.  **Fork 仓库并创建特性分支**：从主仓库 Fork 后，基于 `main` 分支创建 `feature/add-domain-xxx` 分支，所有修改请在该分支内完成。

3.  **提交数据变更并附注来源说明**：修改 `data/links.json` 时，请在提交信息（commit message）中注明外链来源依据（例如“参考某某平台友链页面”），便于审核人评估质量。

4.  **运行本地检测与导出测试**：执行 `poetry run python manage.py crawl --source data/links.json` 确保新增链接可正常访问，运行 `poetry run python manage.py export` 验证导出报表无格式错误。

5.  **发起 Pull Request 并等待审核**：PR 标题请以 `[data]` 或 `[feat]` 开头，内容中填写变更摘要及自检结果。项目维护者将在 3 个工作日内反馈合并意见。

## 常见问题

**Q: 外链状态检测会频繁访问目标站点，是否会被判定为攻击行为？**

A: 本项目使用单线程异步并发，默认并发数 8，每秒请求间隔不低于 150 毫秒，且仅发送 HEAD 请求（不下载主体内容），行为等同于普通浏览器检查书签。建议用户将检测频率调整为每日一次，避免对小型站点造成负担。若目标站点的 robots.txt 明确禁止自动化检测，请手动将该链接加入 `config/blacklist.ua` 跳过检测。

**Q: 项目中的外链分类依据是什么？为什么某些站点同时出现在多个分类下？**

A: 分类基于站点自身的内容定位与运营方公开描述进行一级划分。部分综合性站点（如同时提供连载和交友服务）会标记主要分类为主分类，次要分类通过 `tags` 字段补充，在索引页面中以辅助标签形式展现。若您发现分类明显错误，请按贡献指南提交修正 PR。

**Q: 生成的静态站点是否可以直接部署到 Nginx 或 GitHub Pages？**

A: 可以。`public/` 目录中的全部资源均为纯静态文件（HTML + CSS + JavaScript），无需后端服务。部署至 GitHub Pages 时，建议启用自定义域名并配置强制 HTTPS，但本项目内部资源引用使用相对路径，因此兼容任意基础路径。

## 许可证

MIT License

Copyright (c) 2026 LinkGravity Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-08-24 21:34:14
