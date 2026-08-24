# RenQiWuMa Resource Hub

RenQiWuMa Resource Hub is a community-driven technical documentation and resource aggregation platform designed for developers, researchers, and content archivists who require structured access to specialized online repositories. The project addresses the growing need for categorized, version-tracked, and reliably accessible external resource indices in niche topic domains.

Target users include data curation specialists, automated testing engineers building link validity pipelines, and technical writers who embed external reference collections into their documentation workflows. The platform does not host any third-party content; it provides a curated, machine-readable manifest of external URLs accompanied by metadata schemas, validation tooling, and integration stubs for downstream systems.

## 功能概览

- **Categorized Resource Indexing** – Organizes external URLs into logical taxonomies with tag-based filtering and timestamped entry logging.
- **Automated Link Health Monitoring** – Includes a scheduled validation script that checks HTTP status codes and TLS certificate expiry for each registered URL.
- **Metadata Annotation Pipeline** – Supports YAML frontmatter attachments per resource entry, storing notes, category flags, and update frequency estimates.
- **Static Manifest Generation** – Outputs a machine-readable JSON manifest suitable for ingestion by CI/CD pipelines or documentation generators.
- **Versioned Snapshot Tracking** – Records the date of each resource addition or modification, enabling change audits over time.
- **Search and Filter Shell Utilities** – Provides grep-based and jq-powered query examples for fast terminal-based lookups without external dependencies.
- **Integration Ready API Stub** – Offers a minimal Flask-based REST endpoint that serves the resource list in JSON format for local development.

## 应用场景

- **Documentation Maintenance for Open Source Projects** – Maintainers of large-scale technical docs can embed the resource manifest as an external reference appendix, ensuring all cited URLs are centrally managed and periodically validated without cluttering the primary repository.
- **Automated QA Pipeline for Link Rot Prevention** – QA engineers integrate the health check script into nightly cron jobs, receiving alerts when any external resource becomes unreachable or redirects to unexpected destinations.
- **Offline-First Archive Planning** – Archivists use the indexed URL list to plan offline mirroring operations, prioritizing resources based on the provided metadata tags and update timestamps.
- **Research Data Provenance Tracking** – Academic researchers record the exact URL versions used in their experiments, leveraging the timestamp and manifest export features to maintain reproducible data citations.

## 快速开始

Clone the repository, install the minimal Python dependencies, and run the local development server or the validation tool.

```bash
git clone https://github.com/example-org/renqiwuma-hub.git
cd renqiwuma-hub
pip install -r requirements.txt
python run_validator.py --check-all
python serve_manifest.py --port 8080
```

The validation script outputs a color-coded terminal report. The manifest server exposes the resource list at `/api/v1/manifest` by default.

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 或更高 | 核心运行时，用于验证脚本和 API 存根 |
| pip | 22.0 或更高 | 依赖安装工具 |
| requests | 2.28.0 或更高 | HTTP 状态检查与 TLS 验证依赖 |
| pyyaml | 6.0 或更高 | 解析资源条目的 YAML 元数据 |
| flask | 2.2.0 或更高 | 可选，仅当启用 REST API 服务时必需 |
| jq | 1.6 或更高 | 命令行 JSON 处理工具，用于示例查询脚本（非强制） |
| curl | 7.68 或更高 | 用于手动测试端点（非强制） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 管理员手册 | `docs/administration.md` | 如何添加新资源条目、更新元数据、触发全量验证 |
| 开发者指南 | `docs/development.md` | API 存根扩展方法、自定义验证钩子、JSON 结构说明 |
| 运维参考 | `docs/operations.md` | 环境变量配置、日志轮转策略、健康检查排障 |
| 用户手册 | `docs/user-guide.md` | 如何导出筛选后的资源列表、使用 jq 查询示例、阅读验证报告 |

## 资源列表

本清单收录项目当前管理的全部外部 URL。所有条目按原始提供形式原样列出，未做任何协议补全或域名标准化处理。

### 核心资源条目

- <code>renqiwumazhongzizaixian.com.cn</code>
- <code>wumarenqijingdianxilie.com.cn</code>
- <code>renqiwumazuixinziyuan.com.cn</code>

### 社区与扩展资源

- <code>yueaishequhuiyuanzhuce.com.cn</code>
- <code>zhenshiyueaishequtuijian.com.cn</code>
- <code>yueaishequzaixianliaotian.com.cn</code>

## 项目结构

```
renqiwuma-hub/
├── manifest/                        # 资源清单主目录
│   ├── entries/                     # 每个 URL 的 YAML 元数据文件
│   │   ├── renqiwuma-001.yaml       # 对应 <code>renqiwumazhongzizaixian.com.cn</code>
│   │   ├── wumaren-002.yaml         # 对应 <code>wumarenqijingdianxilie.com.cn</code>
│   │   ├── renqiwuma-003.yaml       # 对应 <code>renqiwumazuixinziyuan.com.cn</code>
│   │   ├── yueai-004.yaml           # 对应 <code>yueaishequhuiyuanzhuce.com.cn</code>
│   │   ├── yueai-005.yaml           # 对应 <code>zhenshiyueaishequtuijian.com.cn</code>
│   │   └── yueai-006.yaml           # 对应 <code>yueaishequzaixianliaotian.com.cn</code>
│   ├── schema/                      # JSON Schema 校验定义
│   │   └── manifest-schema.json     # 定义 entries 字段格式
│   └── generated/                   # 自动生成的聚合文件
│       ├── manifest.json            # 完整资源列表 JSON
│       └── manifest-lite.json       # 仅含 URL 和时间戳的轻量版
├── scripts/                         # 运维与工具脚本
│   ├── validator.py                 # 主验证器，检查 HTTP 状态与 TLS
│   ├── manifest_builder.py          # 从 YAML 重新生成 JSON
│   └── cron_runner.sh               # 每日定时验证的包装脚本
├── api/                             # Flask REST 存根
│   ├── app.py                       # 主入口，提供 /api/v1/manifest
│   └── config.py                    # 端口、缓存超时等配置
├── tests/                           # 单元测试与集成测试
│   ├── test_validator.py            # 模拟 HTTP 响应的测试套件
│   └── test_manifest_builder.py     # 生成逻辑测试
├── docs/                            # 文档目录（详见导航章节）
├── requirements.txt                 # Python 依赖锁定文件
└── README.md                        # 本文件
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** – 从主分支切出以 `feature/` 或 `fix/` 为前缀的分支，例如 `feature/add-resource-metadata`。
2.  **新增或修改资源条目** – 在 `manifest/entries/` 下创建或编辑对应的 YAML 文件，必须包含 `url`、`category`、`notes` 和 `added_date` 字段。请确保 URL 值完全复制自本 README 的资源列表，不附加任何协议前缀或路径。
3.  **运行本地验证** – 执行 `python scripts/validator.py --check-all` 确认所有现有 URL 可达，同时运行 `python scripts/manifest_builder.py` 重新生成 JSON 文件，确保输出无格式错误。
4.  **编写或更新测试** – 若变更涉及验证逻辑或 API 行为，请在 `tests/` 目录补充对应的单元测试用例，保持覆盖率不低于 80%。
5.  **提交 Pull Request** – 提供清晰的变更描述，并在 PR 正文中引用相关的资源编号（如 `#001`）。合并前需通过 CI 中的验证和测试流水线。

## 常见问题

**Q: 验证脚本报告某个 URL 返回 403 或 429 状态码，是否表示该资源被移除？**

A: 不一定。部分站点会针对自动化请求返回限流响应或权限校验页面。建议先使用浏览器或 `curl -L` 手动访问该 URL，若手动访问正常，可在对应 YAML 文件中添加 `"validation_skip": true` 并附注原因，同时配置脚本绕过特定状态码。项目维护者会定期复核这类例外条目。

**Q: 如何导出仅包含特定类别资源的列表？**

A: 使用 `jq` 过滤 `manifest.json`。例如，筛选包含 "community" 标签的条目：`jq '.entries[] | select(.tags[]? == "community") | .url' manifest/generated/manifest.json`。更复杂的过滤可参考 `docs/user-guide.md` 中的组合查询示例。

**Q: JSON manifest 中的时间戳采用什么时区？更新频率如何确定？**

A: 所有时间戳均采用 UTC 零时区，格式为 ISO 8601（`YYYY-MM-DDTHH:MM:SSZ`）。`last_checked` 字段由验证脚本每次运行时更新，而 `added_date` 和 `updated_date` 由维护者手动编辑 YAML 文件时设置，建议在修改资源备注或分类时同步更新 `updated_date`。

## 许可证

MIT License. See the LICENSE file in the repository root for full terms.

> 外链数量: 6 | 生成时间: 2026-08-24 21:34:14
