# Chigua Navigator

Chigua Navigator 是一个面向中文互联网内容索引与资源聚合的开源导航站项目，定位为技术驱动的信息筛选与分发工具。本项目不生产内容，仅通过可验证的公开数据源构建索引图谱，帮助开发者、研究员与内容消费者快速定位特定垂直领域内的站点资源与信息入口。

项目目标用户包括网络爬虫开发者、数据标注团队、内容安全研究方向人员以及需要批量获取特定类别网址清单的运维工程师。Chigua Navigator 通过结构化的元数据描述和状态监测机制，解决上述用户在面对海量无序域名时检索效率低下、可用性验证缺失、分类标准模糊等核心痛点。

## 功能概览

- **分类索引引擎**：支持按内容类型、运营主体、访问热度等多维度筛选，提供稳定的分类浏览入口。
- **可用性健康检查**：内置定时探测模块，对收录域名进行可达性与响应时延检测，自动标记异常状态。
- **批量导出机制**：支持将筛选后的域名列表导出为纯文本、JSON 或 CSV 格式，便于下游脚本或分析工具直接调用。
- **标签过滤系统**：允许用户自定义标签组合进行二次过滤，例如按“小说”“日记”“交友”等标签交叉查询。
- **元数据快照存储**：记录每个域名的基础 Whois 信息、ICP 备案状态以及页面 Title/Description 摘要，形成静态快照。
- **变化差异比较**：提供按时间维度的收录变更记录，清晰展示新增、下架或属性调整的条目。
- **只读 API 接口**：以 RESTful 风格开放查询接口，支持分页、排序和字段投影，便于第三方系统集成。
- **轻量管理面板**：基于 Web 的管理界面，供维护人员执行收录审核、标签校正和异常标记人工确认。

## 应用场景

- **爬虫起始种子构造**：开发者可快速获取指定领域（如日记、文学阅读或社交平台）的初始域名种子列表，用于构建垂直爬虫的入口队列，避免盲目搜索。
- **内容安全策略测试**：安全研究人员可利用本项目的分类标签与可用性数据，搭建测试环境中的模拟流量，验证 URL 过滤策略的准确性与覆盖度。
- **数据标注样本采集**：数据标注团队可依据标签体系筛选特定类型的站点，批量采集页面文本用于训练分类模型或语义相似度任务。
- **运维监控补充源**：运维工程师可将本项目输出的健康检查结果作为自有监控系统的外部数据源，用于对比分析 DNS 解析或网络连通性的区域性差异。
- **学术研究样本框构建**：社会科学或网络传播学研究者可基于本项目的持续快照数据，抽样分析特定类型中文网站的存活周期、内容演变及交互特征。

## 快速开始

以下指令适用于 Linux / macOS 环境，Python 3.10 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/example/chigua-navigator.git
cd chigua-navigator

# 安装项目依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化本地数据库并导入基础索引数据
python manage.py init_db
python manage.py import_seeds --source data/seeds.json

# 启动本地开发服务器
python manage.py runserver --host 127.0.0.1 --port 8080
```

访问 `http://127.0.0.1:8080/dashboard` 可查看管理面板，访问 `http://127.0.0.1:8080/api/v1/domains` 可获取 API 返回示例。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10.x 或 3.11.x | 核心运行时，低于 3.10 不兼容异步语法 |
| SQLite | 3.35.0+ | 内嵌数据库，用于存储域名元数据与快照 |
| aiohttp | 3.8.4+ | 异步 HTTP 客户端，用于并发健康检查 |
| beautifulsoup4 | 4.11.0+ | HTML 解析库，用于提取页面摘要信息 |
| whois | 0.9.3+ | 域名 Whois 信息查询工具 |
| pytest | 7.2.0+ | 单元测试与集成测试框架（仅开发环境） |
| docker | 20.10.0+ | 容器化部署支持（生产环境可选） |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user_guide.md` | 如何使用分类浏览、标签过滤和导出功能？API 的鉴权方式是什么？ |
| 开发指南 | `docs/development.md` | 如何扩展新的探测协议（如 TCP/ICMP）？如何自定义标签体系？ |
| 运维手册 | `docs/operations.md` | 如何配置定时任务自动更新可用性状态？如何迁移 SQLite 到 PostgreSQL？ |
| 设计文档 | `docs/architecture.md` | 异步探测队列的调度逻辑是什么？快照存储的增量策略如何工作？ |
| 贡献规范 | `CONTRIBUTING.md` | 提交代码或新增域名收录需要遵循哪些流程和编码标准？ |
| 安全策略 | `SECURITY.md` | 如何报告收录链接中发现的恶意内容或安全风险？ |

## 资源列表

以下为项目当前阶段收录并维护的原始资源链接。所有链接均按来源分组呈现，且严格保持原始字符串形式。

### 日记与个人记录类

- <code>chuguiriji.com.cn</code>
- <code>renqichuguiriji.com.cn</code>

### 文学阅读与小说连载类

- <code>chengrenxiaoshuolianzai.com.cn</code>

### 平台排行与评测类

- <code>chengrenzhibopingtaipaixing.com.cn</code>

### 社交与互动社区类

- <code>tongchengshaofuyueai.com.cn</code>
- <code>yueaishequjiaoyoupingtai.com.cn</code>

## 项目结构

```
chigua-navigator/
├── data/                           # 静态数据与种子文件
│   ├── seeds.json                  # 初始收录域名清单（含分类标签）
│   └── categories.yaml             # 分类层级与标签映射定义
├── src/                            # 核心源代码
│   ├── collector/                  # 采集与探测子模块
│   │   ├── checker.py              # 异步可用性检查器（HTTP/HTTPS 探活）
│   │   ├── parser.py               # 页面摘要解析器（Title/Description）
│   │   └── whois_lookup.py         # Whois 信息查询封装
│   ├── api/                        # RESTful API 实现
│   │   ├── routes.py               # 路由定义与请求参数校验
│   │   └── serializers.py          # 响应数据序列化与字段投影
│   ├── dashboard/                  # 管理面板后端逻辑
│   │   ├── auth.py                 # 简单令牌认证（开发环境可绕过）
│   │   └── audit_log.py            # 收录变更操作审计
│   ├── storage/                    # 存储层抽象
│   │   ├── db_client.py            # SQLite/PostgreSQL 适配器
│   │   └── models.py               # ORM 模型定义（Domain, Snapshot, Tag）
│   └── utils/                      # 通用工具函数
│       ├── time_utils.py           # 时间格式化与时区转换
│       └── validators.py           # 域名合法性校验与标准化
├── tests/                          # 测试套件
│   ├── unit/                       # 单元测试（覆盖 checker, parser）
│   └── integration/                # 集成测试（API 与数据库交互）
├── scripts/                        # 运维与辅助脚本
│   ├── daily_update.py             # 每日更新定时任务入口
│   └── export_formats.py           # 导出为 JSON/CSV/TXT 的转换脚本
├── docs/                           # 完整文档（详见文档导航）
├── requirements.txt                # 生产依赖列表
├── requirements-dev.txt            # 开发额外依赖
├── Dockerfile                      # 容器镜像构建文件
├── docker-compose.yml              # 本地开发容器编排
├── manage.py                       # 统一命令行管理入口
└── README.md                       # 项目主说明文档（当前文件）
```

## 贡献指南

1.  **问题报告与建议**：请在 GitHub Issues 中提交详细的问题描述或功能建议，包含复现步骤或使用场景说明。对于新增收录域名的请求，需附带该站点的分类依据和简要描述。
2.  **代码贡献流程**：Fork 本仓库后，在 `develop` 分支上创建以 `feature/` 或 `fix/` 为前缀的功能分支。所有代码提交需通过静态检查（`flake8`）和单元测试（`pytest`），并确保新功能的测试覆盖率不低于 85%。
3.  **文档更新要求**：任何涉及接口变更、配置项新增或数据模型修改的 Pull Request，必须同步更新 `docs/` 下对应的文档文件，并在 `CHANGELOG.md` 中添加变更记录。
4.  **收录审核标准**：新增域名必须满足内容合法、可公开访问且稳定运行超过 30 天的基础条件。提交收录请求时需提供 Whois 信息或备案截图作为参考。维护团队将在 5 个工作日内完成审核。
5.  **行为准则**：所有参与者需遵守项目行为准则，尊重他人劳动成果，禁止提交含有恶意代码或侵犯隐私的内容。违反者将被永久移除贡献资格。

## 常见问题

**Q1：项目是否会主动抓取并存储收录站点的完整页面内容？**

不会。本项目的核心定位是索引与导航，而非内容镜像。系统仅在可用性检查阶段获取每个域名首页的 Title 和 Description 元数据，用于生成摘要快照。该快照最长保留 90 天，且不存储页面正文、图片或脚本资源。如需获取完整内容，请直接访问原始站点。

**Q2：收录域名的可用性检测频率是多少？检测结果是否准确？**

默认情况下，系统对每个收录域名每 6 小时执行一次异步探测，连续三次超时或返回非 2xx/3xx 状态码则标记为“异常”。考虑到网络波动和区域性差异，系统会从两个不同网络出口（电信 / 联通）发起请求，并取综合结果。如发现误判，可通过管理面板手动重新检测或申请人工复核。

**Q3：如何将本项目的索引数据完全迁移到内网环境，不依赖外部互联网？**

项目本身除收录域名的探测任务外，不依赖任何外部 API 或云服务。您可以将 `data/seeds.json` 与 `data/categories.yaml` 文件打包，连同源代码一同部署到内网 Git 仓库中。运行 `manage.py import_seeds` 时指定本地文件路径即可完成数据导入。所有 Whois 查询和页面解析均在本地执行，不会外传数据。

## 许可证

MIT License

Copyright (c) 2026 Chigua Navigator Contributors

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
