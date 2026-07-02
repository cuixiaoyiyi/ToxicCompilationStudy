# Toxic Compilation Dataset — Statistics

Record-level incidents: **1703**  ·  campaign-level (deduplicated): **1142**  ·  with code: **1463 (86%)**

_Report incident-level counts (1142 campaigns) to avoid double-counting multi-CVE/multi-version events._
_Single-valued dims sum to N; multi-label dims (stage/carrier/payload/...) may exceed 100%._

## Incidents by ecosystem

| ecosystem | Count | % of incidents |
|---|---:|---:|
| AI-compiler | 509 | 29.9% |
| npm | 394 | 23.1% |
| PyPI | 321 | 18.8% |
| build-tool | 140 | 8.2% |
| AI-skill | 105 | 6.2% |
| crates.io | 64 | 3.8% |
| Go | 61 | 3.6% |
| Maven | 43 | 2.5% |
| Bitnami | 27 | 1.6% |
| RubyGems | 17 | 1.0% |
| Packagist | 16 | 0.9% |
| C/C++ | 2 | 0.1% |
| CI/CD | 2 | 0.1% |
| NuGet | 1 | 0.1% |
| Hex | 1 | 0.1% |


## Incidents by incident type

| incident_type | Count | % of incidents |
|---|---:|---:|
| dependency_confusion_or_typosquat | 732 | 43.0% |
| compilation_inconsistency | 286 | 16.8% |
| jit_cache_poisoning | 209 | 12.3% |
| malicious_package | 122 | 7.2% |
| maintainer_account_compromise | 112 | 6.6% |
| install_lifecycle_abuse | 106 | 6.2% |
| generated_code_injection | 72 | 4.2% |
| release_tarball_poisoning | 32 | 1.9% |
| build_cache_poisoning | 27 | 1.6% |
| build_environment_compromise | 2 | 0.1% |
| compiler_backdoor | 1 | 0.1% |
| maintainer_self_sabotage | 1 | 0.1% |
| supply_chain_advisory | 1 | 0.1% |


## Incidents by root cause

| root_cause | Count | % of incidents |
|---|---:|---:|
| untrusted_dependency_resolution | 732 | 43.0% |
| codegen_semantic_deviation | 358 | 21.0% |
| cache_integrity_failure | 236 | 13.9% |
| malicious_dependency | 122 | 7.2% |
| account_compromise | 113 | 6.6% |
| unsafe_install_hook | 106 | 6.2% |
| source_artifact_divergence | 32 | 1.9% |
| build_pipeline_compromise | 2 | 0.1% |
| compromised_compiler | 1 | 0.1% |
| supply_chain_weakness | 1 | 0.1% |


## Incidents by severity

| severity | Count | % of incidents |
|---|---:|---:|
| high | 892 | 52.4% |
| medium | 541 | 31.8% |
| unknown | 180 | 10.6% |
| critical | 68 | 4.0% |
| low | 22 | 1.3% |


## Occurrences by impact scope

| impact_scope | Count | % of incidents (multi-label) |
|---|---:|---:|
| developer_machine | 1019 | 59.8% |
| released_artifact | 981 | 57.6% |
| downstream_users | 964 | 56.6% |
| ci_runner | 948 | 55.7% |
| model_output | 479 | 28.1% |
| gpu_kernel_execution | 479 | 28.1% |
| build_environment | 365 | 21.4% |


## Incidents by intent (maliciousness)

| maliciousness | Count | % of incidents |
|---|---:|---:|
| malicious | 1029 | 60.4% |
| correctness_only | 493 | 28.9% |
| unknown | 181 | 10.6% |


## Incidents by confidence

| confidence | Count | % of incidents |
|---|---:|---:|
| confirmed | 710 | 41.7% |
| candidate | 651 | 38.2% |
| likely | 342 | 20.1% |


## Incidents by data source

| source | Count | % of incidents |
|---|---:|---:|
| datadog | 700 | 41.1% |
| github_issue | 645 | 37.9% |
| osv_advisory | 344 | 20.2% |
| curated | 14 | 0.8% |


## Code-segment availability

| code_available | Count | % of incidents |
|---|---:|---:|
| True | 1463 | 85.9% |
| False | 240 | 14.1% |


## Occurrences by injection stage

| injection_stage | Count | % of incidents (multi-label) |
|---|---:|---:|
| dependency_resolution | 868 | 51.0% |
| install | 852 | 50.0% |
| compilation | 552 | 32.4% |
| packaging | 350 | 20.6% |
| jit | 287 | 16.9% |
| code_generation | 181 | 10.6% |
| ci_cd | 159 | 9.3% |
| configuration | 106 | 6.2% |
| caching | 66 | 3.9% |
| source_acquisition | 62 | 3.6% |
| release | 35 | 2.1% |
| linking | 24 | 1.4% |
| runtime_codegen | 3 | 0.2% |


## Occurrences by carrier

| carrier | Count | % of incidents (multi-label) |
|---|---:|---:|
| dependency | 928 | 54.5% |
| lifecycle_script | 814 | 47.8% |
| package_manifest | 586 | 34.4% |
| generated_code | 548 | 32.2% |
| build_script | 103 | 6.0% |
| wheel | 65 | 3.8% |
| ci_workflow | 60 | 3.5% |
| prebuilt_object | 37 | 2.2% |
| release_tarball | 35 | 2.1% |
| container_image | 35 | 2.1% |
| compiler_plugin | 33 | 1.9% |
| build_cache | 28 | 1.6% |
| source_tarball | 26 | 1.5% |
| jit_cache | 16 | 0.9% |
| configure_script | 8 | 0.5% |
| makefile | 8 | 0.5% |
| jar | 4 | 0.2% |
| m4_macro | 1 | 0.1% |
| compiler_backdoor | 1 | 0.1% |


## Occurrences by payload

| payload | Count | % of incidents (multi-label) |
|---|---:|---:|
| rce | 924 | 54.3% |
| wrong_code | 462 | 27.1% |
| data_exfiltration | 418 | 24.5% |
| credential_theft | 327 | 19.2% |
| unknown_malicious | 161 | 9.5% |
| backdoor | 75 | 4.4% |
| supply_chain_persistence | 75 | 4.4% |
| info_stealer | 62 | 3.6% |
| artifact_substitution | 34 | 2.0% |
| downloader | 23 | 1.4% |
| authentication_bypass | 8 | 0.5% |
| cryptominer | 8 | 0.5% |
| reverse_shell | 8 | 0.5% |
| data_destruction | 1 | 0.1% |
| ransomware | 1 | 0.1% |


## Occurrences by visibility gap

| visibility_gap | Count | % of incidents (multi-label) |
|---|---:|---:|
| source_artifact_gap | 994 | 58.4% |
| typosquat_namespace | 808 | 47.4% |
| transitive_dependency | 725 | 42.6% |
| cache_opacity | 343 | 20.1% |
| generated_code_gap | 242 | 14.2% |
| binary_only_gap | 191 | 11.2% |
| build_env_opacity | 7 | 0.4% |
| repo_release_mismatch | 1 | 0.1% |

## Occurrences by applicable defense

| detectability | Count | % of incidents (multi-label) |
|---|---:|---:|
| manual_review | 1003 | 58.9% |
| build_script_analysis | 769 | 45.2% |
| behavioral_analysis | 733 | 43.0% |
| build_provenance | 20 | 1.2% |
| reproducible_build | 7 | 0.4% |
| sbom | 7 | 0.4% |


## Incidents by advisory ID namespace

| id_namespace | Count | % of incidents (multi-label) |
|---|---:|---:|
| MAL | 405 | 23.8% |
| CVE | 294 | 17.3% |
| GHSA | 278 | 16.3% |
| PYSEC | 30 | 1.8% |
| RUSTSEC | 20 | 1.2% |


## Incidents by evidence type

| evidence_type | Count | % of incidents (multi-label) |
|---|---:|---:|
| advisory | 754 | 44.3% |
| sample_archive | 700 | 41.1% |
| issue | 648 | 38.1% |
| paper | 2 | 0.1% |
| vendor_report | 1 | 0.1% |
| web | 1 | 0.1% |


## Cross-tabulations
See `tables/crosstab_*.csv`:

- ecosystem × maliciousness
- ecosystem × injection_stage
- source × injection_stage

## Defense coverage matrix (RQ4 — N=1703)

| defense | covered | partially_covered | not_covered | not_applicable | unknown |
|---|---:|---:|---:|---:|---:|
| source_review | 0 | 541 | 1162 | 0 | 0 |
| dependency_scanning | 1104 | 90 | 0 | 509 | 0 |
| package_signature | 144 | 794 | 765 | 0 | 0 |
| sbom | 0 | 1525 | 0 | 178 | 0 |
| slsa_provenance | 215 | 1488 | 0 | 0 | 0 |
| in_toto | 215 | 1488 | 0 | 0 | 0 |
| reproducible_build | 938 | 229 | 0 | 536 | 0 |
| hermetic_build | 1014 | 689 | 0 | 0 | 0 |
| sandboxed_build | 943 | 760 | 0 | 0 | 0 |
| artifact_diffing | 994 | 709 | 0 | 0 | 0 |
| binary_analysis | 211 | 1492 | 0 | 0 | 0 |
| jit_cache_validation | 383 | 0 | 0 | 1320 | 0 |
| behavioral_sandbox | 1120 | 109 | 0 | 474 | 0 |
