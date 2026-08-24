# Wuma Resource Aggregator

Wuma Resource Aggregator is a community-driven navigation and documentation project designed for researchers, cultural analysts, and media professionals who require structured access to specialized digital media resources. The project serves as a curated metadata index that organizes, categorizes, and provides stable referencing points for externally hosted audiovisual collections with specific regional and linguistic characteristics.

This project does not host, store, or distribute any copyrighted or proprietary content. It functions exclusively as a reference layer that maps external resource identifiers to human-readable metadata records. The intended audience includes academic researchers conducting media studies, linguists analyzing regional language variants, and archival professionals performing content provenance tracking. By maintaining a rigorous, version-controlled catalog of resource pointers, the project reduces discovery friction and provides a reproducible foundation for scholarly citation and automated retrieval workflows.

## 功能概览

- **Resource Pointer Registry** – Maintains a versioned registry of external resource identifiers with timestamps and checksum annotations for provenance verification.

- **Metadata Normalization Pipeline** – Transforms raw input references into structured records with standardized fields including language tags, regional origin markers, and format signatures.

- **Batch Import Interface** – Supports ingestion of resource lists in plaintext, JSON, and CSV formats with automatic deduplication and conflict resolution.

- **Search and Filter Engine** – Provides full-text search over metadata fields with facet filtering by content type, region, language variant, and publication date range.

- **Change Audit Logging** – Records every addition, modification, or deletion event with operator identity and ISO-8601 timestamps for compliance and rollback purposes.

- **Export Module** – Generates reference reports in Markdown, JSON, and BibTeX formats for integration with external citation managers and archival systems.

- **Health Check Scheduler** – Periodically probes registered resource endpoints for availability and response latency, flagging stale or unreachable entries for review.

- **User Permission Control** – Implements role-based access tiers (viewer, contributor, maintainer, admin) with granular permissions on resource operations.

## 应用场景

- **Academic Media Corpus Compilation** – Researchers constructing a longitudinal corpus of regional audiovisual materials can use the aggregator to maintain a stable reference list that persists across publication revisions. The audit trail ensures that corpus composition changes are fully documented and citable.

- **Language Variation Analysis** – Linguists studying dialectal and orthographic variations across regional media outputs can leverage the metadata normalization pipeline to enforce consistent labeling, enabling cross-corpus comparisons without manual re-tagging of source materials.

- **Archival Provenance Tracking** – Archivists responsible for preserving culturally significant digital assets can employ the registry to track the provenance of external pointers, distinguishing between original sources, mirror locations, and derivative works.

- **Automated Retrieval Workflows** – System integrators building automated media ingestion pipelines can consume the registry via the export module, retrieving updated resource lists on a scheduled basis without manual intervention.

- **Compliance Documentation** – Organizations needing to demonstrate due diligence in content sourcing can generate audit reports from the change log, providing verifiable evidence of resource selection and review processes.

## 快速开始

```bash
# Step 1: Clone the repository
git clone https://github.com/wuma-aggregator/wuma-resource-aggregator.git
cd wuma-resource-aggregator

# Step 2: Install dependencies
pip install -r requirements.txt
npm install --prefix frontend

# Step 3: Initialize the database and run migrations
python manage.py migrate
python manage.py loaddata initial_metadata

# Step 4: Start the development server
python manage.py runserver --host 0.0.0.0 --port 8080
```

The service will be available at `http://localhost:8080`. The default administrator credentials are printed to the console during first startup. Change these immediately in production deployments.

## 安装要求

| Dependency | Minimum Version | Required For |
|------------|----------------|--------------|
| Python | 3.10 | Core backend runtime and ORM layer |
| PostgreSQL | 14.0 | Primary metadata store with full-text search support |
| Node.js | 18.0 | Frontend asset compilation and development server |
| Redis | 6.2 | Caching layer and scheduled task broker |
| Elasticsearch | 7.17 | Advanced search indexing and query acceleration |
| libpq-dev | Latest | PostgreSQL client library for Python binding compilation |
| openssl | 1.1.1 | TLS certificate management and secure token generation |
| git | 2.30 | Version control for source tree and contributor workflows |
| docker | 20.10 | Containerized deployment (optional production mode) |
| docker-compose | 2.0 | Multi-container orchestration (optional production mode) |

## 文档导航

| Layer | Directory | Questions Addressed |
|-------|-----------|---------------------|
| User Guide | docs/user-guide/ | How do I search for resources? How do I export reference lists? What are the permission tiers and how do I request access? |
| Administrator Manual | docs/admin/ | How do I configure the health check scheduler? How do I perform bulk imports? How do I audit the change log for compliance reporting? |
| Developer Reference | docs/developer/ | What is the data model for resource records? How do I extend the metadata normalization pipeline? Which API endpoints are available for integration? |
| Deployment Guide | docs/deployment/ | What are the production deployment prerequisites? How do I configure TLS termination? How do I set up backup and disaster recovery for the metadata store? |
| Contribution Guidelines | CONTRIBUTING.md | How do I submit a resource addition or correction? What is the code review process? How are changes versioned and released? |

## 资源列表

### Primary Resource Index

The following resource identifiers constitute the core registry maintained by this project. These entries have been curated from the submitted batch and are presented exactly as provided.

<code>ribenwumarenqizhuanqu.com.cn</code>

<code>renqiwumazhongwenzimu.com.cn</code>

<code>renqiwumawanzhengban.com.cn</code>

<code>renqiwumamianfeibofang.com.cn</code>

<code>renqiwumagaoqingxiazai.com.cn</code>

<code>ribenwumarenqiheji.com.cn</code>

## 项目结构

```
wuma-resource-aggregator/
├── backend/                              # Core Python application
│   ├── api/                              # RESTful endpoint definitions (versioned)
│   │   ├── v1/                           # API version 1 resources
│   │   │   ├── resources.py              # CRUD operations for resource registry
│   │   │   ├── search.py                 # Full-text and facet search handlers
│   │   │   ├── audit.py                  # Change log retrieval endpoints
│   │   │   └── health.py                 # Endpoint status check triggers
│   │   └── middleware/                   # Authentication and rate limiting
│   ├── models/                           # SQLAlchemy ORM definitions
│   │   ├── resource.py                   # Resource pointer entity schema
│   │   ├── metadata.py                   # Extended metadata fields schema
│   │   ├── audit_log.py                  # Change entry schema with actor and timestamp
│   │   └── user.py                       # Credential and permission schema
│   ├── pipelines/                        # Data transformation workflows
│   │   ├── normalizer.py                 # Input normalization and standardization
│   │   ├── deduplicator.py               # Duplicate detection and merging logic
│   │   └── importer.py                   # Batch ingestion from CSV/JSON/plaintext
│   ├── scheduler/                        # Background task definitions (Celery)
│   │   ├── health_check.py               # Periodic endpoint availability probes
│   │   ├── index_rebuild.py              # Elasticsearch index refresh tasks
│   │   └── backup.py                     # Automated metadata store dumps
│   └── config/                           # Configuration profiles (dev, staging, prod)
├── frontend/                             # React-based user interface
│   ├── src/
│   │   ├── components/                   # Reusable UI components (search bar, table, filters)
│   │   ├── pages/                        # Route-level page definitions
│   │   ├── hooks/                        # Custom React hooks for API interactions
│   │   └── state/                        # Redux slices and state management
│   └── public/                           # Static assets and build entry point
├── docs/                                 # Project documentation by audience layer
│   ├── user-guide/                       # End-user tutorials and feature walkthroughs
│   ├── admin/                            # Operational runbooks and configuration guides
│   ├── developer/                        # API documentation, data model, and extension points
│   └── deployment/                       # Production provisioning and scaling advice
├── scripts/                              # Maintenance and utility automation
│   ├── migrate_db.py                     # Schema migration runner
│   ├── seed_initial_data.py              # Populate database with starter resource records
│   └── export_snapshot.py                # Generate timestamped reference export
├── tests/                                # Unit and integration test suites
│   ├── unit/                             # Isolated component tests
│   ├── integration/                      # API and database round-trip tests
│   └── fixtures/                         # Test data stubs and mock responses
├── docker-compose.yml                    # Production container orchestration definition
├── Dockerfile                            # Multi-stage build definition for container image
├── requirements.txt                      # Python dependencies with pinned versions
├── package.json                          # Node.js dependencies for frontend build
└── README.md                             # This document
```

## 贡献指南

1. **Fork and Clone** – Fork the repository to your personal account, then clone your fork locally. Set up the upstream remote to track the main repository for synchronization. Ensure your local environment meets all installation requirements before proceeding.

2. **Identify Contribution Type** – Determine whether your contribution involves adding new resource entries, correcting existing metadata, improving documentation, or addressing a software defect. For resource additions, verify that the entries are publicly accessible and properly categorized.

3. **Create a Feature Branch** – Create a descriptive branch name from the latest `main` branch. Use the format `feature/resource-batch-YYYYMMDD` or `fix/description` to clearly communicate the purpose of your changes.

4. **Submit a Pull Request** – Push your branch and open a pull request against the `main` branch. Fill in the provided PR template completely, including a summary of changes, testing performed, and any issues closed. For resource additions, include the source of your references in the PR description.

5. **Await Review and Sign-off** – Maintainers will review your submission within five business days. Address any requested changes promptly. Once all checks pass and at least one maintainer has approved, your changes will be merged and included in the next release.

## 常见问题

**Q: How does this project handle resource availability changes when external endpoints become unreachable?**

A: The health check scheduler runs every 24 hours and attempts to connect to each registered endpoint. When an endpoint fails to respond within the configured timeout window, the entry is flagged with a `stale` status in the metadata. Maintainers are notified via the dashboard alert panel. Stale entries are not automatically removed; they remain in the registry with the `stale` flag so that researchers can still reference them for historical citation purposes. A separate task generates weekly reports listing all stale entries for manual review.

**Q: Can I import my own list of resources beyond the ones shown in the resource list section?**

A: Yes. The import module supports batch ingestion from three formats: plaintext (one identifier per line), CSV (with columns for identifier, language tag, region, and notes), and JSON (array of objects following the resource schema). You must have contributor-level permission to initiate an import. The system automatically runs deduplication against existing entries and produces a conflict report for manual resolution before finalizing the import. Detailed instructions are available in the Administrator Manual under the bulk import section.

**Q: What is the recommended backup strategy for the metadata stored in this system?**

A: The project includes an automated backup task that performs a full database dump to a configurable storage location every six hours. For production deployments, we recommend configuring the backup destination to a separate physical volume or cloud storage bucket with versioning enabled. Additionally, the audit log provides a complete chronological history of all changes, which means the database can be rebuilt from the initial seed plus the audit trail if the primary store becomes corrupted. Refer to the Deployment Guide for example backup cron configurations and restoration procedures.

## 许可证

This project is licensed under the MIT License. See the LICENSE file in the repository root for the full license text. In brief, you are permitted to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to retaining the original copyright notice and permission notice in all copies or substantial portions of the software. The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement.

> 外链数量: 6 | 生成时间: 2026-08-24 21:34:14
