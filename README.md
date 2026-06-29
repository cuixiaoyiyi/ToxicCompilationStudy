# Toxic Compilation Dataset

An **incident-centered, multi-layer** dataset for the empirical study of *toxic
compilation* — security or correctness problems that are introduced **not in the
reviewed source code** but during dependency resolution, configuration,
compilation, code generation, linking, packaging, install, JIT, caching, CI/CD,
or release.

> Defining test: *the source looks fine, but the produced / installed / executed
> artifact does not match it.*

Every incident is linked to a **concrete code segment** on disk
(`snippets/<incident_id>/...`) plus structured evidence, artifacts, and taxonomy
labels.

## Layout
```
toxic-compilation-dataset/
├── schema/                 JSON Schemas (one per layer) + annotation_guideline.md
├── taxonomy/taxonomy.json  controlled vocabulary + keyword classification rules
├── data/                   CANONICAL data (JSONL, one record per line)
│   ├── incidents.jsonl         Layer 1 — the unit of study
│   ├── evidence.jsonl          Layer 2 — CVE/GHSA/OSV/advisory/report/paper
│   ├── artifacts.jsonl         Layer 3 — tarball/wheel/gem/cache/binary…
│   ├── code_evidence.jsonl     Layer 4 — concrete code segment (snippet_path)
│   ├── labels.jsonl            Layer 5 — taxonomy annotation (multi-annotator)
│   └── defense_coverage.jsonl  Layer 6 — per-incident defense coverage (RQ4)
├── snippets/<incident_id>/ the actual code file(s) for each incident
├── raw/                    cached source data (DataDog tree, intermediate jsonl)
├── exports/                DERIVED: *.csv + statistics.sqlite (for stats/plots)
└── scripts/                the reproducible pipeline
```

## Data sources
| Source | What it gives | Code? |
|---|---|---|
| **OSV advisories** (CVE/GHSA/PYSEC/RUSTSEC, keyword-filtered) | build/install/packaging/codegen/supply-chain advisories across PyPI, Maven, Go, Packagist, NuGet, RubyGems, crates.io, Hex | usually no (advisory text; sometimes a fenced excerpt) |
| **GitHub Issues** | AI-compiler codegen / JIT-cache / compile-cache correctness (Triton, TorchInductor/PyTorch, TVM, vLLM, TileLang, XLA, LLVM) + build-cache/install | sometimes (issue repro block) |
| **DataDog `malicious-software-packages-dataset`** | archived malicious npm / PyPI / AI-skill packages | **yes — real archived code** |
| **Curated landmark + AI set** | XZ, Trusting Trust, SolarWinds, event-stream, ua-parser-js, torchtriton, node-ipc, Triton/vLLM/TileLang cache … | yes (published / reconstructed, labelled) |

NVD is network-blocked in some environments; CVE/GHSA come via **OSV** (which
carries CVE aliases) instead. Code is **not required** for every entry — each
incident has a boolean `code_available`. `snippet_provenance` in
`code_evidence.jsonl` records the code kind: `actual_archived`, `actual_published`,
`advisory_excerpt`, `issue_excerpt`, or `reconstructed`.

### Two orthogonal evidence axes (see the left-panel dropdowns in readme.html)
- **`evidence_type`** (document kind): `advisory`, `sample_archive`, `vendor_report`,
  `issue`, `pull_request`, `commit`, `blog`, `paper`, `web`.
- **`id_namespace`** (ID scheme): `CVE`, `GHSA`, `MAL`, `PYSEC`, `RUSTSEC`, `OSV`, `none`.

### LLM relevance & reconstructed code
Keyword-collected advisories are noisy, so each is LLM-judged into
`llm_relevance` = `toxic_compilation` (in scope) or `off_topic` (false positive,
`confidence=excluded`). For in-scope CVEs without crawlable code, an LLM produces an
**illustrative reconstruction** (`snippet_provenance=llm_reconstructed`, header
comment says "not the exact published code"). CVE and code are independent: an entry
can be `id_namespace=CVE` **and** `code_available=true`.

### Quality metrics (filterable numeric ranges in readme.html)
Per `incidents.jsonl` `metrics`: GitHub issues carry `repo_stars`, `repo_forks`,
`issue_reactions`, `issue_comments`; advisories carry `cvss_score`, `severity`,
`n_references`; DataDog samples carry `n_files`.

Corpus size is tunable via `TC_DATADOG_CAP` / `TC_ADVISORY_CAP` env vars (see
`03_build_dataset.py`).

## Reproduce
```bash
cd scripts
python run_all.py            # fetch → seed → build → export
# or, if raw/dd_records.jsonl already exists:
python run_all.py --no-fetch
```
Pure Python standard library — no `pip install` required. Tune corpus size via the
`QUOTA` dict in `01_fetch_datadog.py`.

## Query examples (SQLite)
```sql
SELECT ecosystem, COUNT(*) FROM incidents GROUP BY ecosystem;     -- or: SELECT * FROM v_by_ecosystem;
SELECT incident_type, COUNT(*) FROM incidents GROUP BY incident_type;
SELECT * FROM incidents WHERE maliciousness='correctness_only';   -- AI-compiler cases
```
```python
import pandas as pd
inc = pd.read_json("data/incidents.jsonl", lines=True)
```

## Research framing (see `../有毒编译案例分析.pdf`)
- **RQ1** which build stages are most exploited? (`injection_stage`)
- **RQ2** what are the attack carriers? (`carrier`)
- **RQ3** what visibility gaps hide them? (`visibility_gap`)
- **RQ4** what do current defenses cover? (`detectability`)

## Provenance & ethics — SAMPLES ARE NEUTRALIZED
Malicious code is included **for defensive research only**.
- Every code segment under `snippets/<id>/` is saved with a **`.txt` suffix** (e.g.
  `index.min.js.txt`) so it is **not executable** and won't run on a double-click.
- Each file begins with a banner: `DEFENSIVE-RESEARCH SAMPLE - DO NOT EXECUTE.
  Original name: <original>`. The real filename is preserved in `code_evidence.jsonl`
  `file_path`.
- No malware archives (`.zip`/`.tar.gz`) are kept on disk — sample zips are fetched
  to memory, the representative file is extracted, and only its text is stored.
- `raw/*.jsonl` are data caches that quote sample code as JSON strings (inert data,
  not runnable). Your antivirus may still flag them by signature; treat the whole
  `snippets/` and `raw/` trees as quarantined research material. **Do not execute.**

## License / release
Intended for release as a GitHub repository + Zenodo DOI. Respect upstream
licenses of the DataDog dataset and any quoted advisories.
