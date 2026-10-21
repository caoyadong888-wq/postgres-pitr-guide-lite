# PostgreSQL PITR Guide (lite)

## English

### Purpose

A free preview of the archiving half of point-in-time recovery. It quotes the PostgreSQL 18 continuous-archiving chapter on `wal_level`, `archive_mode`, `archive_command`, and `archive_timeout`. Recovery settings, `pg_basebackup` flags, timeline history files, and the local checker are not in this preview.

No server is started. No container image is named. Values that depend on the major version stay marked `check-upstream-docs`. The lab host is `db.example.com` (`192.0.2.20`). The lab mailbox is `dba@example.com`.

### Deliverables

- `deliverables/ARCHIVE_NOTES.md` — archiving notes only.
- `deliverables/postgresql.archive.snippet` — archiving fragment with variables.
- `examples/postgresql.archive.example` — the same fragment filled for the lab.
- `examples/lab-cluster.env` — the lab names and the documentation address.

### Quick start

Read `deliverables/ARCHIVE_NOTES.md`, then compare the snippet to `examples/postgresql.archive.example`. Do not paste the snippet over a live `postgresql.conf` until each `{{CHECK_UPSTREAM_DOCS:NAME}}` value has been checked against your major version.

Python is not required for this preview. No network and no database client.

## 中文

### 用途

时间点恢复里“打开归档”这一半的免费预览。它引用 PostgreSQL 18 连续归档一章里关于 `wal_level`、`archive_mode`、`archive_command` 和 `archive_timeout` 的说明。恢复参数、`pg_basebackup` 参数、时间线历史文件和本地检查器不在这个预览里。

不会启动服务器，也不指定容器镜像。随大版本变化的取值仍标为 `check-upstream-docs`。实验主机是 `db.example.com`（`192.0.2.20`）。实验邮箱是 `dba@example.com`。

### 交付清单

- `deliverables/ARCHIVE_NOTES.md` — 只讲归档。
- `deliverables/postgresql.archive.snippet` — 带变量的归档片段。
- `examples/postgresql.archive.example` — 给实验填好的同一片段。
- `examples/lab-cluster.env` — 实验名称和文档地址。

### 快速开始

先读 `deliverables/ARCHIVE_NOTES.md`，再把片段和 `examples/postgresql.archive.example` 对照。在每个 `{{CHECK_UPSTREAM_DOCS:NAME}}` 都对照过你的大版本文档之前，不要把片段覆盖到正在使用的 `postgresql.conf` 上。

这个预览不需要 Python，也不需要网络或数据库客户端。

PostgreSQL 18 文档要求：归档时 `wal_level` 为 `replica` 或更高，`archive_mode` 设为 `on`，并写上 `archive_command` 或 `archive_library`。`%p` 是相对于数据目录的路径，`%f` 是文件名，`%%` 是百分号本身。`archive_timeout` 用来在服务器空闲时也切出一段日志；提前切出的段仍然是完整长度。一分钟左右是该章认为通常合适的量级。裸整数的单位要核对上游文档。

完整版另外包含 PostgreSQL 12 及更新版本的恢复片段、旧版 `recovery.conf` 的警告、`pg_basebackup` 参数清单，以及一个分成两条时间线的例子。

Full version: GUMROAD_URL
