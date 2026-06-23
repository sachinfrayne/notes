# Suggestions: content to add to this repo

Ideas for new notes or examples. Use this as a backlog; remove or move items into [`PLAN.md`](PLAN.md) when you commit to doing them.

**Already covered (do not duplicate without a clear angle):** top-level [`elasticsearch.md`](elasticsearch.md), [`logstash.md`](logstash.md), [`docker.md`](docker.md), [`bash.md`](bash.md), [`kibana.md`](kibana.md), [`jq.md`](jq.md), [`openssl.md`](openssl.md), [`esrally.md`](esrally.md), [`markdown.md`](markdown.md), and the files under [`elasticsearch-examples/`](elasticsearch-examples/) and [`logstash_examples/`](logstash_examples/).

---

## Elasticsearch — new `elasticsearch-examples/` ideas

These complement topics like data streams, ILM, field collapse, rescoring, rollups, nested aggs, synonyms, and `text` vs `keyword`.

- **Ingest pipelines:** common `set` / `remove` / `rename` / `script` / `pipeline` routing; testing with `_simulate`; failure handling.
- **Reindex:** same-cluster and remote reindex; throttling (`requests_per_second`); slice parallelisation; common `conflicts` patterns.
- **Runtime fields:** `long` / `keyword` / `geo_point` from `_source`; when to prefer runtime vs indexed.
- **ES|QL or SQL:** a few “reporting” queries that mirror what you already show with `_sql` in [`elasticsearch.md`](elasticsearch.md), plus CSV/TSV export patterns.
- **Shard allocation:** exclude/include nodes, awareness zones, forced allocation for a stuck shard (with strong warnings).
- **Cluster state / red index triage:** `_cluster/allocation/explain`, `_cat/shards`, interpreting unassigned reasons in one flowchart-style note.
- **Snapshots and restore:** SLM policy sketch, restore to another index name, partial restore pitfalls (if not already elsewhere).
- **Security (non-secret):** API key creation with scoped roles; service accounts at a high level; TLS-related *diagnostic* snippets only (no private keys in repo).
- **Transforms / anomaly detection:** minimal “what to call and what to watch” if you use these in anger.
- **Vector / dense_vector:** a tiny, version-tagged example (mapping + one `knn` query) if you want this repo to track stack-specific syntax.
- **Cross-cluster search / CCS:** remote cluster alias + one search example.
- **Watcher / alerting (Elastic Stack):** one JSON example of a threshold alert if you still maintain Watcher-style content.

---

## Logstash — new `logstash_examples/` ideas

You already have [`remove_boolean_if_field_name_matches_regex.md`](logstash_examples/remove_boolean_if_field_name_matches_regex.md) and a unit-test skeleton in [`logstash.md`](logstash.md).

- **Grok:** building and testing grok against sample lines; `GROK_PATTERNS_DIR` / custom patterns file.
- **Date filter:** multiple formats, `locale` / `timezone`, handling failure tags.
- **Mutate / copy / rename:** order of operations pitfalls (e.g. rename then mutate).
- **Conditional routing:** `if` on field, tag, or metadata; multiple pipelines vs single pipeline branches.
- **Dead letter queue (DLQ):** enabling DLQ, reading entries, replay strategy outline.
- **Jdbc input:** jdbc_streaming vs paging; tracking column; scheduler hygiene (no passwords in repo—placeholders only).
- **Elasticsearch output:** `action` types, `pipeline` parameter, bulk failure behaviour, `ilm_enabled` interaction at a glance.
- **Multiline codec / filter:** filebeat vs logstash multiline; when to push multiline to ingest instead.
- **Aggregate filter:** one worked “sessionise by key” example with clear edge-case notes.
- **Pipeline-to-pipeline:** `pipeline` input/output with a minimal two-file example.
- **Performance:** `-w` workers, batch size / delay tuning checklist (bullet list, not a novel).

---

## Docker — additions to or beside [`docker.md`](docker.md)

- **Compose:** `docker compose` profiles, override files, `depends_on` with healthchecks, one “stack up / down” cheat block.
- **Build:** multi-stage build minimal pattern; buildx and a single “cross-build” example if you use Apple Silicon → linux/amd64.
- **Run constraints:** `--memory`, `--cpus`, `--ulimit`, `--tmpfs` for Elasticsearch-style workloads (values as placeholders).
- **Networking:** user-defined bridge vs host; publishing ports; `docker network inspect` debugging one-liners.
- **Logs:** `docker logs --since`, `--tail`, driver overview (local vs json-file vs something centralised).
- **Cleanup (advanced):** `docker system df`, pruning by filter, dangling images—extend your existing cleanup section rather than repeating it.
- **Exec / debug:** `docker exec -it`, copying files in/out with `docker cp`, inspecting an unhealthy container.
- **Registry auth:** `docker login` / credential helper mention only—no tokens in notes.

---

## Bash — additions to [`bash.md`](bash.md)

- **Strict mode:** `set -euo pipefail` in functions vs scripts; when `set -e` is surprising.
- **Traps:** `trap` on `EXIT` / `ERR` for tempdir cleanup.
- **Arrays:** indexed and associative; iterating safely with `"${arr[@]}"`.
- **Process substitution** and **here-strings** where they beat pipes.
- **`xargs`:** `-0` with `find -print0`; `-P` for bounded parallelism.
- **`flock`:** single-instance script pattern.
- **`mktemp` / `tmpdir`:** safe temp files and directories.
- **Dates:** `date` formats for log filenames (you already have related patterns elsewhere—link or consolidate).

---

## General “stack ops” snippets (new top-level or small folders)

- **curl + jq:** authenticated `curl` patterns (placeholders), pretty-print, `jq` empty vs null (you have [`jq.md`](jq.md)—add cross-links from Elasticsearch examples where useful).
- **systemd / launchd:** one minimal unit file for “run this exporter” or “restart on failure” if you care about laptops vs servers separately.
- **Git:** cherry-pick, revert, bisect one-liners for ops repos (only if you want this repo to be general “workstation” notes).
- **Kubernetes (light):** `kubectl` debug snippets—only if you want to blur the boundary with work repos; otherwise skip.

---

## Kibana, OpenSSL, Rally — shallow follow-ups

- **Kibana:** saved object export/import API or `kbn` URLs for common dashboards (version-tagged).
- **OpenSSL:** cert chain inspection, `s_client` SNI, converting PEM/PKCS12—short additions to [`openssl.md`](openssl.md).
- **Rally:** one race for indexing-only vs search-only; custom track directory layout—extend [`esrally.md`](esrally.md).

---

## Housekeeping suggestions (content quality)

- When adding an example, add **one line at the top**: product (Elasticsearch/Logstash/Docker), and **major version** the snippet was written for, if syntax drifts often.
- Prefer **placeholders** (`<CLUSTER_URL>`, `<API_KEY>`) over realistic-looking hosts.
- Link new deep dives from [`README.md`](README.md) (see [`PLAN.md`](PLAN.md) Phase A).
