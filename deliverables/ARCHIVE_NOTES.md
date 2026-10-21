# Archiving notes (lite)

This preview covers only how the PostgreSQL 18 docs describe turning WAL archiving on. Recovery targets, `pg_basebackup` flags, timeline history files, and the snippet checker are in the full version.

It does not start PostgreSQL and does not name a container image. check-upstream-docs.

## What to set

The PostgreSQL 18 continuous-archiving chapter says to set `wal_level` to `replica` or higher, set `archive_mode` to `on`, and set `archive_command` or `archive_library`. In practice those lines go in `postgresql.conf`.

`archive_mode` cannot be enabled when `wal_level` is `minimal`. It can only be set at server start. Besides `off`, the modes are `on` and `always`. `always` also archives during archive recovery or standby.

In `archive_command`, `%p` is the path relative to the data directory, `%f` is the file name, and `%%` is a literal percent. The chapter's Unix example is:

```
archive_command = 'test ! -f /mnt/server/archivedir/%f && cp %p /mnt/server/archivedir/%f'
```

`archive_timeout` forces a new segment on a quiet server. An early segment is still full length. The chapter says settings of a minute or so are usually reasonable. The unit of a bare integer is check-upstream-docs.

If the command or `archive_library` keeps failing, old segments accumulate in `pg_wal` (the directory name in the PostgreSQL 18 docs). Older directory names: check-upstream-docs.

## The lab fragment

`examples/postgresql.archive.example` fills a fictional lab on `db.example.com` (`192.0.2.20`):

- `wal_level = replica`
- `archive_mode = on`
- archive directory `/var/backups/wal-lab`
- `archive_timeout = 60`

`deliverables/postgresql.archive.snippet` leaves every assigned value as `{{CHECK_UPSTREAM_DOCS:NAME}}`. Replace one only after you have read the page for the major version you run. The mailbox recorded for the lab is `dba@example.com`.

The full version adds the PostgreSQL 12+ recovery fragment, the legacy `recovery.conf` warning, the `pg_basebackup` flag list, and a two-branch timeline example.
