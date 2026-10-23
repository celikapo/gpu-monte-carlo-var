# Snapshot requirements coverage

FR-1..FR-9 and NFR-1..NFR-9 retain the source review draft's identifiers and
full-project meaning. This is a technical coverage map, not a new acceptance
contract or a claim of academic approval. Source identity is in
[provenance](provenance.md). Covered means covered within the stated snapshot
scope; partial coverage never means the full-project requirement is satisfied.

| ID | Full-project requirement | Snapshot coverage |
| --- | --- | --- |
| FR-1 | Daily close CSV import; reject invalid dates, ordering, fields and prices | Covered for the documented strict CSV format and existing malformed fixtures; no provider adapter/calendar |
| FR-2 | Annual GBM calibration from log returns, documented scale and sample variance | Covered; controlled .01,.02,.03 returns test mean .02, variance .0001 and parameters within 1e-12 |
| FR-3 | Analytical single-asset GBM VaR at .95/.99 | Covered; quantile/deterministic/signed references within 1e-12; negative VaR retained |
| FR-4 | Selected serial/OpenMP/CUDA VaR at both confidences | Partially covered: serial only; full accuracy requires NFR-5/6 |
| FR-5 | Identical pre-generated normal per scenario in every compared engine | Partially covered: serial common-input interface and wrong-length rejection; no cross-engine comparison |
| FR-6 | CLI input/N/seed/horizon/annual scale/backend/thread controls | Partially covered: input/N/seed/horizon/scale; no backend or thread selector |
| FR-7 | Results/metadata: model, seed, RNG, version, input checksum, timing scope | Partially covered: JSON model/seed/RNG/version/time and documented timing; no per-run input-hash manifest |
| FR-8 | Automated seeded statistical validation and separate timing campaigns | Outside this snapshot; deterministic tests and small examples do not replace campaigns |
| FR-9 | Labelled GPU batching/hybrid fallback with one global loss quantile | Outside this snapshot; never average batch VaRs |
| NFR-1 | Evaluate 10x transfer-inclusive GPU/serial target at N=10000000 and compare fastest measured OpenMP | Outside this snapshot; no speedup claim |
| NFR-2 | 100% documented invalid-input fixtures fail with explicit error/nonzero exit | Partially covered: existing negative unit fixtures plus explicit CLI failure; no full-project negative suite |
| NFR-3 | Version/examples; 100% English ASCII code/comments/program messages | Covered for maintained CPU implementation and examples; historical evidence bytes preserved |
| NFR-4 | Zero personal/patient records; dataset source/range/reuse/adjustment documented | Covered for the synthetic fixture only; no historical provider data |
| NFR-5 | Per engine, N=10000000/five seeds: error-of-mean <=.01*max(abs(analytical),.01*V0), separately .95/.99 | Outside this snapshot's acceptance evidence; criterion unchanged in numerical-contract.md |
| NFR-6 | Double/common quantile; common-input cross-engine difference <=.00001*V0; separate memory/race checks | Partially covered: double, rank and serial common inputs; no multi-engine or sanitizer certification |
| NFR-7 | N=100000,1000000,10000000; 3 excluded warm-ups +10 measured/config; mean, sample SD, scenarios/s | Outside this snapshot; no formal benchmark |
| NFR-8 | Exact-byte experiment hashes/Git dirty state and two same-build/input/seed/backend repeats | Partially covered: source/fixture hashes and existing same-build repeat unit check; no campaign manifests |
| NFR-9 | Release: zero build errors, all registered tests pass, >=1 successful basic CI | Covered within serial CPU scope: local Release checks passed and initial target exact-SHA CI passed 1/1 job; see validation.md |

Full-project NFR-7 uses sample SD denominator 9 for ten samples, retains slow
samples, and records environment/placement/power/thermal limits. The proposal's
DRAM GB/s and percentage-of-documented-peak reporting is later work, unchanged.
No older R01-R14/B01-B02 labels are copied or renumbered here.
