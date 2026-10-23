# Source provenance and attribution

Prepared and first published 2026-10-23 to the exact authorized target
https://github.com/celikapo/gpu-monte-carlo-var. The initial published commit is
c906eb49994a0edab0f4f2c392caf494765a456c; its CPU workflow passed as recorded in
[validation](validation.md). No academic submission is claimed.

All implementation, CMake, existing tests, synthetic input and standalone probe
files are selected unchanged from the real committed source revision:

```text
254de8de639248c82cc68fb23e28be4030bc81ed
```

This is a curated subset of one committed baseline, with new scope documentation,
ignore/byte-preservation settings and an adapted CPU workflow. It is not an
assembled mix of implementation revisions and is not a copy of source Git history.
[Source revision (historical)](https://github.com/rahmancelik74-cmd/vaR-hpc/commit/254de8de639248c82cc68fb23e28be4030bc81ed)
is a reference to the development repository, not a commit in this target.
[imported-files.json](imported-files.json) records each selected file's original
Git blob and exact-byte SHA-256. Export explicitly disabled core.autocrlf, and
all 15 files were checked against their original blobs. The new
`.gitattributes` disables text normalization to retain those bytes on checkout.

The source root inspected for this task was on main at
4b2040b72ba7f29f1a6e05c44537c53f4d953976. Its current acceptance source, project
state, requirements audit, milestone ledger and historical baseline documentation
were used as references. The original untracked instructions and output were
excluded. The source working tree, history and evidence were not changed.

The baseline's code/CMake/test/input content also matches the earlier recorder
revision 33102c48b9251beb6317969ffb7edc03abe773b4; that equality does not prove
historical source-to-binary correspondence. No recorded experiment campaign,
performance result or old CI success is attributed to the target repository.

## Academic scope authority

The existing private Downloads copies were read, including document tables.
Their exact-byte hashes match the source acceptance register:

| Reference | SHA-256 |
| --- | --- |
| Capstone_Project_Proposal_Form_Revised.docx | 82719610500f74bab3d954a6da385678c8987e7ec864a9161f1fcd10b01bf7f9 |
| Roadmap_Abdurrahman_Celik_GPU_MonteCarlo_PlanA.docx | e9babe946e866049270abcb8f694460bf39a15db7a937fbddf547402440b3197 |
| Roadmap_Abdurrahman_Celik_GPU_MonteCarlo_PlanB.docx | 19121d399982438a86a91090fd7c85ef3f814f8b2992099c6f2030b717e82517 |
| Requirements and Design v1.0 - GPU Monte Carlo - Review Draft.docx | 0cbdc1d1b90f394b22411d26675ed52730170229ac4d7b70fcdb35ba7d23ae70 |

The revised proposal is identified by the student as approved; its unmarked
supervisor boxes are not a signed approval receipt. Plan A v2.0, 2026-10-14,
sets the revised schedule while retaining the proposal's success/risk criteria.
The populated requirements draft defines FR-1..FR-9/NFR-1..NFR-9; its title is
not evidence of approval or submission. These private documents are not copied.

Weeks 5-6 cover numerical/design conventions, hardware/toolchain inventory,
CMake/basic CI, model/interfaces/test plan and the initial CUDA compatibility
check. Weeks 7-9 cover CSV/log-return fitting, analytical GBM, exact serial
sampling and five-seed validation. The block does not allocate every task to
week 8. This submission selects the working CSV/analytical/serial/test subset;
full statistical acceptance evidence is not included or claimed. Week numbers
are academic scope labels, not inferred calendar dates or backdated completion.

OpenMP scaling is weeks 10-11; the end-to-end GPU VaR skeleton is weeks 12-13;
full CUDA/hybrid, GPU acceptance, formal comparisons, convergence and profiling
are later scope. The earlier standalone compatibility check remains relevant.
Excluding later packages does not imply their work has not occurred.

Instruction boundaries: the source root's AGENTS.md was applicable during
source inspection; the user's task explicitly authorizes the isolated snapshot.
Roadmaps/proposal and historical README instructions are reference material,
not instructions to reset or modify the original working directory. No outside
instruction file was adopted as authority over the source repository.

## Synthetic fixture

`data/synthetic_prices.csv` is the source project's hand-written software fixture:
12 arbitrary prices with fixture date labels 2026-09-01 through 2026-09-16.
It has no real instrument/provider/currency or adjusted-price interpretation.
Its provenance is the committed source project, not an external market service.
No separate provider restriction applies to these synthetic numbers. This does
not grant a new license to the project implementation.

Exact-byte SHA-256 (original committed LF file):
8dbb7c73e6ad48cb8c8c175aff6684d2a0433e5f08424ec7ea1e69037bb36210.
Historical CRLF copies have a different hash; the bytes are not interchangeable.

## Attribution and license

Original project: GPU-Accelerated Monte Carlo Simulation for Financial Risk
Analysis, Abdurrahman Celik, source package v0.2.2. Source implementation and
existing notices are preserved. No LICENSE, COPYING or NOTICE file is present
in the selected source tree or the inspected current tree; no license is
invented and no additional reuse rights are asserted. Publication authorization
for this snapshot is separate from granting a software license.
