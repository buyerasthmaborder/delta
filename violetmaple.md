# TechLink Navigator

TechLink Navigator 是一个面向开发者、技术研究团队与内容策展人的轻量级外链资源聚合与导航系统。项目定位于解决技术社区中优质外部资源分散、检索效率低、链接失效频繁的问题，通过结构化分类、版本化存储与可用性监控，为团队内部或公开社区提供一个可维护、可扩展的技术资源枢纽。目标用户包括开源项目维护者、技术文档工程师、架构师以及需要系统化整理外部参考链接的研发团队。

系统本身不存储任何实体内容，仅对用户提供的原始 URL 进行组织、分类与状态跟踪。相比传统书签管理工具，TechLink Navigator 提供更强的元数据扩展能力、链接健康检查机制与轻量级访问统计，使资源列表从静态收藏夹进化为动态知识索引。

## 功能概览

- **分类资源树** 支持无限层级目录结构，每一条外链可归属至多级分类，便于按领域、用途或来源进行维度划分。

- **链接健康巡检** 内置定时任务，每日对收录的 URL 执行可用性探测，自动标记异常链接并生成报告，降低失效引用风险。

- **访问热度统计** 记录每个外链的点击次数与最后访问时间，辅助识别高频资源，为内容优化提供数据参考。

- **元数据扩展字段** 每条链接可附加标签、摘要说明、维护人、更新周期等自定义属性，满足团队协作场景下的信息补充需求。

- **导入导出兼容** 支持批量导入用户原始链接列表（纯文本或 CSV），并可导出为标准 HTML 导航页或 JSON 格式数据，便于迁移与二次开发。

- **页面内嵌预览** 针对文档类外链，提供 iframe 嵌入式预览窗口（可配置开关），减少跳转成本，提升浏览体验。

- **只读只写权限分离** 内置基础角色控制，允许设置管理员与普通访客权限，适合公开导航站与内部知识库两种部署模式。

## 应用场景

1. **技术团队内部知识库索引** 研发团队可将日常参考的 API 文档、设计规范、运维手册等外部分散资源统一收录，按项目或技术栈分类，新成员入职时快速获取所需资料入口。

2. **开源项目文档站外链管理** 开源项目维护者使用本系统管理 README、Wiki 或官网中引用的外部链接，当第三方服务变更时，可批量更新导航配置，避免文档中出现死链。

3. **技术社区内容策展** 社区运营人员可整理优质教程、工具站点、视频资源等，生成分类导航页供社区成员使用，同时通过热度统计了解内容偏好，指导后续内容方向。

4. **个人技术书签云同步** 开发者可将个人浏览器书签导出后导入系统，配合健康巡检功能定期清理失效资源，实现跨设备、跨浏览器的统一书签管理。

## 快速开始

以下步骤将在本地环境启动 TechLink Navigator 实例，默认使用 SQLite 数据库，无需额外安装数据库服务。

```bash
# 1. 克隆代码仓库
git clone https://github.com/techlink-navigator/navigator.git
cd navigator

# 2. 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化数据库与默认配置
python manage.py migrate
python manage.py loaddata initial_categories.json

# 4. 启动开发服务器
python manage.py runserver 0.0.0.0:8000
```

访问 <code>http://localhost:8000</code> 即可进入导航主页。默认管理员账号为 <code>admin@techlink.local</code>，密码 <code>admin123456</code>，首次登录后请及时修改。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 - 3.12 | 核心运行环境，低于 3.9 版本不支持类型注解特性 |
| Django | 4.2.x LTS | Web 框架，用于提供路由、ORM 与管理后台 |
| SQLite | 3.31+ | 默认内嵌数据库，适合小型部署；生产环境可换用 PostgreSQL |
| redis | 6.0+ | 可选依赖，用于缓存热度统计与链接巡检任务队列 |
| requests | 2.28+ | 链接健康检查模块所需 HTTP 客户端库 |
| beautifulsoup4 | 4.11+ | 页面预览时用于清洗提取正文摘要，避免加载恶意脚本 |
| gunicorn | 20.1+ | 生产环境 WSGI 服务器，仅在 Linux 部署时使用 |
| nodejs | 18.x | 仅当启用前端资产构建时必需，默认发行版包含预编译静态文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | <code>/docs/user-guide/</code> | 如何录入链接、分类管理、设置标签与元数据；如何查看健康报告与访问统计 |
| 管理员指南 | <code>/docs/admin-guide/</code> | 如何配置巡检周期、调整权限角色、执行数据备份与迁移；如何接入外部认证 |
| 开发参考 | <code>/docs/developer-api/</code> | 如何基于 RESTful API 进行二次开发；请求与响应格式说明；鉴权方式与限流策略 |
| 部署运维 | <code>/docs/deployment/</code> | 如何部署至生产环境（Nginx + Gunicorn + PostgreSQL）；如何配置 HTTPS、日志轮转与监控告警 |

完整文档还包含常见操作示例、故障排查清单以及性能调优参数说明，建议新用户优先阅读用户手册第一章快速入门部分。

## 资源列表

以下为本项目当前收录的全部原始外链资源，按内容主题分类整理。所有链接均为用户提供，系统仅做索引不做任何内容修改。

### 社区与群组

<code>bendiyueaisheququnzu.com.cn</code>

### 应用与工具

<code>siyueapp.com.cn</code>

### 视频资源 - 人气无码高清

<code>renqiwumagaoqingshipin.com.cn</code>

### 视频资源 - 日本无码专区

<code>ribenwumarenqizhuanqu.com.cn</code>

### 视频资源 - 中文字幕

<code>renqiwumazhongwenzimu.com.cn</code>

### 视频资源 - 完整版

<code>renqiwumawanzhengban.com.cn</code>

## 项目结构

项目采用 Django 标准布局，并扩展了导航专用模块。以下为核心目录树及注释说明。

```
navigator/
├── manage.py                      # Django 管理入口脚本
├── requirements.txt               # Python 依赖列表
├── config/                        # 项目全局配置目录
│   ├── settings.py               # 主配置文件（含数据库、缓存、中间件）
│   ├── urls.py                   # 根路由分发
│   └── wsgi.py                   # 生产部署入口
├── apps/                          # 所有自定义应用
│   ├── links/                    # 外链管理核心应用
│   │   ├── models.py             # 链接、分类、标签、巡检记录模型
│   │   ├── views.py              # 导航主页、分类浏览、详情页视图
│   │   ├── serializers.py        # DRF 序列化器，供 API 使用
│   │   ├── tasks.py              # 链接健康巡检定时任务（Celery）
│   │   └── utils.py              # URL 规范化、域名提取等工具函数
│   ├── accounts/                 # 用户与权限管理
│   │   ├── models.py             # 扩展用户模型，增加角色字段
│   │   └── backends.py           # 自定义邮箱登录认证后端
│   └── stats/                    # 访问统计模块
│       ├── models.py             # 点击日志、每日汇总表
│       └── middleware.py         # 请求拦截中间件，记录访问行为
├── static/                        # 静态资产（CSS、JS、图片）
│   ├── css/
│   ├── js/
│   └── images/
├── templates/                     # Django 模板文件
│   ├── base.html                 # 基础布局模板
│   ├── index.html                # 导航首页（分类卡片 + 热门链接）
│   └── detail.html               # 链接详情及预览页
├── docs/                          # 文档源文件（Markdown 格式）
│   ├── user-guide/
│   ├── admin-guide/
│   └── developer-api/
├── scripts/                       # 运维与辅助脚本
│   ├── import_links.py           # 批量导入原始 URL 脚本
│   └── health_check.py           # 手动触发链接巡检脚本
└── docker/                        # 容器化部署文件
    ├── Dockerfile
    └── docker-compose.yml
```

## 贡献指南

欢迎社区开发者参与贡献，无论是报告问题、提交补丁还是完善文档。请遵循以下流程：

1. **查阅现有 Issue 与项目看板** 访问 GitHub Issues 页面，确认您要处理的问题尚未被认领。新功能建议请先创建讨论议题，与维护者沟通设计思路后再开始编码。

2. **派生仓库并创建功能分支** 将主仓库 Fork 至个人账号，然后基于 <code>main</code> 分支创建新的功能分支，分支命名建议使用 <code>feat/</code>、<code>fix/</code> 或 <code>docs/</code> 前缀，例如 <code>feat/add-import-export</code>。

3. **编写代码并遵循编码规范** 项目使用 PEP 8 风格，提交前请运行 <code>flake8</code> 与 <code>black</code> 进行自动格式化。所有新增功能需包含对应的单元测试，测试用例放置于各应用下的 <code>tests/</code> 目录。

4. **提交变更并签署开发者原创声明** 提交信息请使用约定式提交格式（<code>feat:</code>、<code>fix:</code>、<code>docs:</code>），并在 Pull Request 描述中确认代码为原创且未侵犯第三方权益。

5. **发起 Pull Request 并参与评审** 向主仓库的 <code>main</code> 分支发起 PR，维护者将在 3 个工作日内进行评审。请根据反馈及时修改，合并后您的贡献将被列入项目贡献者列表。

## 常见问题

**Q: 系统可以处理多少个链接？性能是否有瓶颈？**

A: 系统设计上支持 5 万条以内的链接管理，在此范围内页面响应时间保持在 300ms 以下（基于 SQLite 测试）。链接巡检任务采用异步队列执行，不会阻塞前台访问。若链接数超过 5 万，建议切换至 PostgreSQL 并启用 Redis 缓存，可支撑至 20 万条规模。

**Q: 如何保证用户提供的原始 URL 不会被修改或丢失？**

A: 系统对每个原始 URL 存储两份字段：<code>raw_url</code> 保存用户输入的完整原始字符串（不做任何规范化），<code>normalized_url</code> 则用于去重与匹配。所有展示和跳转均使用 <code>raw_url</code> 字段，确保用户原始数据一字不差。导入功能会额外记录导入批次与时间戳，便于追溯。

**Q: 是否支持私有部署且不联网使用？**

A: 完全支持。除链接健康巡检功能需要向外发起 HTTP 请求外，其余所有功能均可离线运行。您可以在配置中关闭巡检任务，系统即成为一个纯静态导航管理工具。所有静态资产和文档均打包在发行版中，无需额外 CDN 资源。

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本软件，包括商业用途。完整许可证文本请参见项目根目录下的 <code>LICENSE</code> 文件。

> 外链数量: 6 | 生成时间: 2026-08-24 21:34:14
