# Plan: Fix and harden the `notes` repository

This document is the single source of truth for improving this repo: a personal collection of Markdown snippets and examples ([`README.md`](README.md)). Work can be done in the order below or in parallel within each phase.

---

## 1. Goals

| Goal | Success criteria |
|------|------------------|
| **Discoverability** | A new reader can find every note from the root without guessing filenames. |
| **Consistency** | Naming, fences, and tone follow simple conventions across files. |
| **Accuracy** | Typos and obvious wording errors are fixed; external links are checked periodically. |
| **Hygiene** | Ignore rules behave as intended; nothing sensitive is committed; `PLAN.md` is tracked when you are ready. |

Non-goals for this pass: rewriting long articles, pinning every Elastic doc URL to a specific stack version, or turning the repo into a static site (unless you explicitly want that later).

---

## 2. Current state (audit snapshot)

- **Content:** Top-level topic files (`elasticsearch.md`, `logstash.md`, `kibana.md`, …) plus [`elasticsearch-examples/`](elasticsearch-examples/) with deeper examples. [`logstash_examples/`](logstash_examples/) has at least one standalone note.
- **README:** One-line description only; no map of the tree or links into subfolders.
- **`.gitignore`:** Contains `**.DS_Store`. Prefer verifying against real `find` output; the common, battle-tested pattern is a single line: `.DS_Store` (Git ignores that name in any directory).
- **Markdown fences:** Many Elasticsearch console snippets use a custom fence language `` ```eb `` (see [`elasticsearch.md`](elasticsearch.md), [`kibana.md`](kibana.md), and files under `elasticsearch-examples/`). On GitHub this rarely highlights correctly. Decide one convention: e.g. `json` for pure JSON bodies, `http` for `GET`/`PUT` lines, or unlabeled fences for mixed Dev Console content—then apply consistently in a dedicated pass.
- **Typos:** At least one confirmed typo: “speciliased” in [`elasticsearch-examples/text_vs_keyword.md`](elasticsearch-examples/text_vs_keyword.md) (line ~159). Grep for similar issues after edits.
- **LICENSE:** Dated 2023; optional update to a year range (e.g. `2023–2026`) if you still want MIT and an accurate copyright span—legal preference is yours.
- **Git:** `PLAN.md` is currently untracked; add and commit when the plan stabilizes.

---

## 3. Phase A — Navigation and structure (high impact, low risk)

1. **Expand [`README.md`](README.md)** with:
   - A short “what this repo is” (keep the current one-liner or merge it).
   - **Table of contents** linking to every top-level `.md` file.
   - **Subfolders:** explicit links to [`elasticsearch-examples/`](elasticsearch-examples/) and [`logstash_examples/`](logstash_examples/), with a one-line description of each subfolder’s purpose.
2. **Optional index files:** Add minimal `elasticsearch-examples/README.md` (and/or `logstash_examples/README.md`) listing each file with a one-line blurb so GitHub renders a usable directory page.
3. **Cross-links:** Where it helps (e.g. end of [`elasticsearch.md`](elasticsearch.md)), add “See also” links into `elasticsearch-examples/` for related deep dives—only where the relationship is obvious to avoid stale coupling.

---

## 4. Phase B — Content and copy fixes

1. Fix **“speciliased” → “specialised”** (or American spelling **“specialized”**—pick one dialect for the repo) in [`elasticsearch-examples/text_vs_keyword.md`](elasticsearch-examples/text_vs_keyword.md).
2. Run a **project-wide spell pass** (editor spellcheck or `codespell` if you use it) on `*.md` only.
3. **Placeholder safety:** Ensure examples use obvious placeholders (`<PASSWORD>`, `<ELASTICSEARCH_URL>`) and not real credentials. Re-scan after any bulk edit.

---

## 5. Phase C — Markdown and rendering conventions

1. **Fence language policy:** Document the chosen rule in [`markdown.md`](markdown.md) or in README under “Conventions,” then normalize files in batches (start with `elasticsearch-examples/` since they share the same pattern).
2. **Heading hierarchy:** Keep one H1 per file (already mostly true); avoid skipped levels where tooling complains.
3. **Optional automation:** Add a minimal `.markdownlint.json` (or `markdownlint-cli2` in CI) only if you want enforced rules; keep rules loose so personal notes stay low-friction.

---

## 6. Phase D — Repository and tooling hygiene

1. **`.gitignore`:** Replace or supplement `**.DS_Store` with `.DS_Store`; confirm with `git check-ignore -v` on a test path.
2. **Commit `PLAN.md`:** When you agree with this plan, `git add PLAN.md` and commit so history tracks remediation.
3. **Optional CI (GitHub Actions):** A workflow that runs on `push`/`pull_request` to `main`:
   - `markdown-link-check` or `lychee` on `*.md` (allowlist `elastic.co`, etc., if needed).
   - Fail the job only on broken *internal* links if external flakes are annoying.

---

## 7. Phase E — Ongoing maintenance (lightweight)

1. After each **new note**, update README (or folder README) in the same commit.
2. **Quarterly:** Run link check + quick spell grep on new/changed files.
3. When Elastic APIs change, prefer adding a short “stack note” line at the top of affected snippets rather than rewriting entire guides.

---

## 8. Execution checklist (copy into issues or tick off locally)

- [ ] README: TOC + links to all notes and subfolders  
- [ ] Optional: `elasticsearch-examples/README.md`, `logstash_examples/README.md`  
- [ ] Cross-links from `elasticsearch.md` to examples (where natural)  
- [ ] Typo fix + spell pass on `*.md`  
- [ ] Document and apply fence-language convention  
- [ ] Normalize `.gitignore` for `.DS_Store`  
- [ ] (Optional) LICENSE copyright year range  
- [ ] Commit `PLAN.md` + follow-up commits per phase  
- [ ] (Optional) CI: link check for Markdown  

---

## 9. Suggested commit sequence

1. `docs: expand README and add example index readmes`  
2. `docs: fix typos and clarify placeholders`  
3. `chore: normalize gitignore and markdown code fences`  
4. `chore: add optional markdown link check workflow` (if you add CI)  

This keeps reviews small and reversible.

---

## 10. Open decisions (resolve once, then update this file)

| Decision | Options |
|----------|---------|
| English spelling | UK vs US (affects “specialised/specialized”, “normaliser/normalizer” in prose) |
| Code fence tag for Dev Console | `eb` (status quo), `http`, `json`, or plain ``` |
| CI strictness | Internal links only vs all URLs |

When you decide, add a two-line “Conventions” subsection to [`README.md`](README.md) and trim this section accordingly.
