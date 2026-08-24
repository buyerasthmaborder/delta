# Rina Resource Aggregator

Rina Resource Aggregator is a curated technical index and navigation system designed for developers, researchers, and content archival specialists who require structured access to specialized regional media metadata and linguistic corpora. The project does not host, store, or distribute any third-party content; instead, it provides a deterministic, machine-readable mapping layer that resolves query patterns to externally maintained data sources. The primary target audience comprises automated analysis pipelines, academic linguistic studies focusing on East Asian subtitle corpora, and forensic media verification workflows that depend on version-stamped external references.

The system addresses the common failure modes of link rot, inconsistent URL schemes, and manual bookmark proliferation by offering a single, version-controlled manifest that can be consumed via RESTful endpoints or flat-file exports. Every entry in the aggregation is accompanied by cryptographic digest placeholders, last-seen timestamps, and availability health checks, enabling operators to build reliability monitors atop otherwise volatile external resources. Rina is not a search engine, nor does it implement crawling logic; it is a static, auditable index that prioritizes uptime and transparency over algorithmic discovery.

## 功能概览

- **Deterministic URL Manifest** – Each external reference is stored as an immutable string literal, preserving protocol, domain, and path casing exactly as provided by upstream maintainers, with no auto-correction or normalization.

- **Health Probe Adapter** – The manifest schema includes optional fields for HTTP status code expectations and TLS fingerprint hints, allowing integration with external monitoring daemons such as Uptime Kuma or Blackbox Exporter.

- **Tag-Based Faceting** – Every index entry can be assigned multiple labels (e.g., `region:jp`, `format:srt`, `quality:1080p`, `status:active`), enabling slice-and-dice queries without a full-text search engine.

- **Versioned Snapshot Export** – The entire manifest can be exported as JSON Lines or YAML frontmatter blocks, with each release tagged by a Git SHA and an ISO 8601 timestamp, supporting reproducibility in academic citation.

- **Offline-First Cache Hint** – For each aggregated URL, the manifest optionally stores a content-addressed backup pointer (IPFS or Archive.org) to facilitate retrieval when the primary endpoint becomes unreachable.

- **Webhook Notification Bus** – A lightweight publisher-subscriber module emits events when a monitored URL changes its response signature (status, redirect chain, or content-length), enabling downstream alerting or auto-update scripts.

- **CLI Query Tool** – A Go-based command-line client provides subcommands for `lookup`, `verify`, `diff`, and `export`, with output formatting for both human readability and machine parsing (JSON, CSV, plaintext).

- **Static Site Generator** – The project ships with a Hugo-based theme that renders the manifest as a browsable HTML table, complete with search filters and dark-mode support, suitable for internal team dashboards.

## 应用场景

- **Academic Corpus Curation** – Linguistics researchers can integrate the manifest into their data ingestion pipelines to systematically reference external subtitle archives without manually curating URL lists across multiple lab servers. The versioned snapshots ensure that paper reproducibility remains intact even when upstream sources reorganize their directory structures.

- **Regional Media Metadata Aggregation** – Analysts tracking regional content distribution can use the tag facets to quickly isolate subsets of links relevant to specific encoding standards or geographical release patterns, reducing the time spent on manual browser tab management from hours to seconds.

- **Automated Quality Assurance for Archival Systems** – Organizations maintaining long-term preservation repositories can configure the health probes to periodically validate that all referenced external endpoints remain compliant with their internal security policies, with webhook alerts triggering ticket creation in Jira or ServiceNow upon detection of certificate expiry or unexpected redirects.

- **DevOps Pipeline Dependency Pinning** – Infrastructure teams can treat the manifest as a "bill of materials" for external data dependencies, incorporating it into Terraform or Ansible playbooks to provision allowlists for firewall egress rules, thereby preventing accidental access to unvetted domains during deployment phases.

- **Forensic Link Provenance Verification** – Digital forensics examiners can cross-reference the manifest against proxy logs to identify whether any of the aggregated URLs were accessed during a specific investigation window, leveraging the immutable Git history as an evidentiary chain-of-custody record.

## 快速开始

The following sequence assumes a Linux or macOS environment with Git, Go (1.21+), and GNU Make installed. For Windows, use WSL2 or the provided PowerShell wrapper scripts.

```bash
# Clone the repository with full commit history
git clone https://github.com/rina-agg/rina-core.git
cd rina-core

# Install Go dependencies and build the CLI tool
make deps
make build

# Run the initial manifest validation and generate the static site
./bin/rina verify --manifest=manifest.yaml --strict
./bin/rina export --format=html --output=./public/index.html

# Start the embedded development server on port 8080
./bin/rina serve --port=8080 --watch
```

For production deployments, it is recommended to use the provided Dockerfile and docker-compose.yml to orchestrate the service alongside Prometheus and Grafana for observability.

## 安装要求

| Dependency | Required Version | Purpose and Remarks |
|------------|------------------|----------------------|
| Go | 1.21 or later | Primary language for CLI tool and webhook dispatcher; uses the standard library and a minimal set of third-party modules (cobra, viper, zap). |
| Git | 2.25 or later | Required for clone operations, tag management, and to enable the `--git-metadata` flag during export. |
| GNU Make | 3.81 or later | Used to orchestrate build targets, test execution, and linting; not required if you manually invoke `go build`. |
| Hugo | 0.111.3 or later | Only needed for the static site generation feature; can be skipped if you only use the CLI for data export. |
| Docker | 20.10 or later | Optional but recommended for containerized deployment; the official image is based on Alpine and includes both the CLI and the site renderer. |
| yq | 4.35 or later | Used in CI pipelines to merge manifest patches; not required for runtime operation but helpful for advanced manifest editing. |

## 文档导航

| Layer | Directory / Resource | Questions Addressed |
|-------|-----------------------|----------------------|
| User Manual | `docs/manual/` | How do I install the CLI? How do I query a specific URL? How do I add a custom tag? |
| API Reference | `docs/api/` | Which endpoints are exposed by the embedded server? What is the request/response schema for health checks? |
| Operator Guide | `docs/operator/` | How do I deploy the static site behind an nginx reverse proxy? How do I configure webhook secrets? |
| Contributor Handbook | `CONTRIBUTING.md` | What are the coding conventions? How do I run the test suite? What is the pull request workflow? |
| Schema Specification | `docs/schema/` | What fields are mandatory in the manifest? How are timestamps formatted? What is the retention policy for old entries? |
| Security Policy | `SECURITY.md` | How are TLS certificates validated? What logging is emitted for access attempts? How to report a vulnerability? |

## 资源列表

The following external resources are aggregated as immutable references. Each entry is preserved exactly as provided, without protocol upgrades, www prefix additions, or trailing slash normalization. These links are not under the control of the Rina project, and their availability is subject to external factors.

### Primary Content Domains

- <code>ribenwumarenqizhuanqu.com.cn</code>

- <code>renqiwumazhongwenzimu.com.cn</code>

- <code>renqiwumawanzhengban.com.cn</code>

- <code>renqiwumamianfeibofang.com.cn</code>

- <code>renqiwumagaoqingxiazai.com.cn</code>

- <code>ribenwumarenqiheji.com.cn</code>

## 项目结构

```
rina-core/
├── cmd/                                    # CLI entry points and subcommand implementations
│   ├── rina/                               # Main binary package (main.go, root.go)
│   ├── lookup/                             # 'rina lookup' – resolve a single URL entry
│   ├── verify/                             # 'rina verify' – validate manifest integrity
│   ├── export/                             # 'rina export' – output in various formats
│   └── serve/                              # 'rina serve' – embedded HTTP server and webhook listener
├── internal/                               # Private packages not intended for external import
│   ├── manifest/                           # Manifest parser, validator, and schema definitions
│   ├── probe/                              # HTTP health check engine with retry and backoff
│   ├── cache/                              # In-memory LRU cache for frequent lookups
│   ├── webhook/                            # Dispatcher for outgoing notifications (Slack, Mattermost, generic webhook)
│   └── metrics/                            # Prometheus counter and histogram wrappers
├── pkg/                                    # Public packages that can be imported by third-party tools
│   ├── types/                              # Shared data structures (Entry, Tag, HealthStatus)
│   ├── client/                             # HTTP client wrapper with custom TLS configuration
│   └── format/                             # Encoding/decoding helpers for YAML, JSON, and CSV
├── configs/                                # Default configuration files and schema examples
│   ├── manifest.example.yaml               # Full manifest with all optional fields annotated
│   ├── webhook.example.yaml                # Example webhook routing rules
│   └── prometheus/                         # Alerting rules and Grafana dashboard provisioning
├── deployments/                            # Containerization and orchestration assets
│   ├── Dockerfile                          # Multi-stage build for minimal Alpine image
│   ├── docker-compose.yml                  # Stack with Prometheus, Grafana, and the rina service
│   └── kubernetes/                         # Helm charts and kustomize overlays for K8s
├── site/                                   # Hugo-based static site generator source
│   ├── layouts/                            # HTML templates for table rendering and search UI
│   ├── assets/                             # CSS, JS, and webfonts (Tailwind-based)
│   └── content/                            # Markdown pages for about, license, and changelog
├── test/                                   # Integration and end-to-end test suites
│   ├── mock/                               # Mock HTTP server for probe testing
│   ├── fixtures/                           # Pre-canned manifest files for regression tests
│   └── e2e/                                # Shell scripts that exercise the full CLI pipeline
├── docs/                                   # Detailed documentation (see the Documentation Navigation section)
├── Makefile                                # Primary build automation entry point
├── go.mod                                  # Go module definition with pinned dependencies
├── go.sum                                  # Cryptographic checksums for all module dependencies
└── README.md                               # This file
```

## 贡献指南

1. **Issue Tracker Discipline** – Before commencing work, search the existing issue tracker for relevant tickets. If none exist, open a new issue with the `proposal` label, clearly describing the problem, the proposed solution, and any backward compatibility implications. For bug reports, include the exact `rina version` output, the operating system, and a minimal reproduction manifest that triggers the unexpected behavior.

2. **Fork and Branch Strategy** – Fork the upstream repository to your personal namespace, then create a feature branch named `feat/<short-description>` or `fix/<issue-number>-<short-description>`. Avoid committing directly to the `main` branch. Keep the branch rebased on the latest upstream `main` to minimize merge conflicts, and run `make lint` and `make test` locally before pushing.

3. **Coding Standards and Commit Messages** – All Go code must pass `golangci-lint` with the project's provided `.golangci.yml` configuration. Commit messages must follow the Conventional Commits specification (e.g., `feat: add retry backoff to probe engine`, `fix: correct YAML unmarshaling for empty tags`). Each commit should be atomic and accompanied by a clear explanation of the "what" and "why".

4. **Test Coverage Requirement** – Every new feature or bug fix must include corresponding unit tests in the `test/` directory, with a minimum incremental coverage of 80% for the changed package. Integration tests that require external HTTP calls should use the mock server provided in `test/mock/` rather than hitting live endpoints.

5. **Documentation and Changelog Updates** – If the change affects user-facing behavior (CLI flags, API responses, manifest schema), update the relevant section in `docs/` and add an entry to `CHANGELOG.md` under the `[Unreleased]` header. For non-trivial changes, include a code comment or a short design note in the pull request description.

## 常见问题

**Q: Why does the project not auto-correct URL schemes or add missing prefixes?**
A: Rina is designed as a faithful aggregation layer, not a normalization proxy. Auto-correcting URLs introduces non-determinism and can mask upstream misconfigurations. By preserving the exact string provided, we allow operators to build deterministic automation that fails explicitly when a URL is malformed, rather than silently succeeding with a potentially incorrect interpretation.

**Q: How do I update the manifest when an external resource changes its domain?**
A: Manifest updates are treated as code changes. You should open a pull request that replaces the old URL with the new one, update the `last_seen` timestamp and `status` field, and add a comment in the `notes` attribute explaining the transition. The project does not support in-place editing of the manifest via the web UI to maintain auditability.

**Q: Can I use Rina behind a corporate proxy that terminates TLS?**
A: Yes. The CLI and the embedded server respect the standard `HTTP_PROXY`, `HTTPS_PROXY`, and `NO_PROXY` environment variables. Additionally, the `pkg/client` package allows custom TLS configuration via the manifest's `tls` block, where you can specify `insecure_skip_verify` (not recommended for production) or a custom CA bundle path using the `ca_cert_file` field.

## 许可证

This project is licensed under the terms of the MIT License. See the LICENSE file in the repository root for the full text. The license applies solely to the source code and documentation of the Rina Aggregator project; it does not imply any rights or permissions regarding the external resources listed in the manifest, which remain subject to their respective owners' terms of service.

> 外链数量: 6 | 生成时间: 2026-08-24 21:34:14
