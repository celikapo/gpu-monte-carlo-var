# Validation and evidence limits

## Local snapshot checks, 2026-10-23

The selected snapshot configured and built successfully with CMake
3.31.6-msvc6, Visual Studio 17 2022 x64, MSVC 19.44.35227.0 and Windows SDK
10.0.26100.0. Release flags: /O2 /Ob2 /DNDEBUG. The first sandboxed configure
and build attempts could not access the installed Windows SDK; the same commands
succeeded with approved SDK access. No source correction was needed.
MSBuild emitted MSB8029 because the isolated build was under the local temporary
directory; this was not a compilation failure. The final independent copy outside the temporary
directory configured/built successfully and passed all four CTests again
(0 failures; 0.20 s); its build emitted no MSB8029 warning. No general
warning-free portability claim is made.

All four existing CTests passed: core_tests, json_output_tests,
csv_calibration_tests and csv_cli_smoke (0 failures; 0.24 s total).
These exercise known normal quantiles, zero horizon/volatility, retained negative
VaR, nearest rank, common inputs, same-build seed repeatability, malformed CSV,
controlled calibration/sample variance and JSON output.

The representative fixed-parameter N=10000/seed42 run produced both confidence
outputs. The CSV run used N=10000, seed42, horizon10, annual scale252:

| Confidence | Simulated VaR | Analytical VaR |
| --- | --- | --- |
| 0.95 | 6.0379874525407811 | 6.1435769394189581 |
| 0.99 | 8.5870161133789473 | 8.7154467162009475 |

These are small synthetic smoke results, not a five-seed acceptance or formal
benchmark. The CSV JSON reported 12 observations/11 returns, V0=100.4,
annual mu=0.11221749496730603, sigma=0.2037837912712771 and T=10/252.
`mc_var 0 42 --json` returned exit1 with
`Error: Nonzero scenarios and confidence levels required` and no partial JSON.
`--version` returned `mc_var 0.2.2 (CSV support enabled)`.
Local raw logs/build outputs remain ignored; this file is a reviewed summary,
not an edited historical log or a claim of remote CI.

Reproduce using the README commands. No GPU, benchmark, convergence, profiling,
provider acquisition or five-seed campaign was run for this task. No new
sanitizer/race or thermal/power measurements are claimed.

## Historical early CUDA compatibility record

The unchanged [probe source](../evidence/cuda-probe-20261016/probe.cu),
[standalone CMake](../evidence/cuda-probe-20261016/CMakeLists.txt) and
[execution log](../evidence/cuda-probe-20261016/execution.log) are imported from
254de8de639248c82cc68fb23e28be4030bc81ed. The probe was originally archived at
1acfee39a70e526c9f22ae422be8ef3a106b4254 on 2026-10-16. Its timestamp identifies
the recorded check, not an inferred academic completion week.

It reports RTX 4060 Laptop, compute capability8.9, 8187 MiB VRAM and
driver/runtime API values13030. The historical inventory separately reports
nvcc13.4.92 and MSVC19.44.35227.0; compiler version and runtime API integers
are distinct observations. The log records correct doubling of 1024 integers,
with device allocation, transfer, launch, synchronization and cleanup checks.
It does not execute CSV/calibration, cuRAND, a GPU quantile or GPU VaR, and does
not certify full GPU acceptance, memory/race freedom or performance.

Historical target inventory from the selected source: i7-12650H,
10 physical cores/16 logical processors, reported 16 GB RAM, Windows11,
NVIDIA Windows driver32.0.16.1088. Serial build common flags were
/DWIN32 /D_WINDOWS /GR /EHsc and Release /O2 /Ob2 /DNDEBUG.
These are historical machine observations, not hosted runner properties;
clocks, temperatures and thermal equilibrium are not established.

Optional manual reproduction on a compatible CUDA system requires CMake>=3.24
and its CUDA toolchain. This is an independent build and is never part of CPU CI:

```sh
cmake -S evidence/cuda-probe-20261016 -B build-probe
cmake --build build-probe --config Release
```

Run `build-probe/cuda_probe` (Visual Studio: `build-probe/Release/cuda_probe.exe`).
This task reused the record without running the probe or modifying its raw bytes.

## Target GitHub Actions

[build.yml](../.github/workflows/build.yml) adapts the baseline's suitable basic
workflow. One Ubuntu CPU job configures Release, builds, runs the four existing
CTests, exercises fixed/CSV CLI calls and checks explicit invalid-input rejection.
Root CMake does not enable CUDA/OpenMP or discover a Toolkit. The standalone
CUDA subproject is not configured in CI. No unavailable advanced scripts,
private data or source history is required.

The initial preparation encountered a genuine write-permission barrier. After
the collaborator invitation was accepted, the existing identity rahmancelik74-cmd
was verified with push=true on the exact target. No account was switched.

First publication: 2026-10-23 (push confirmation at 02:40:00 UTC), using a normal
push of c906eb49994a0edab0f4f2c392caf494765a456c to main. Remote main matched
that exact SHA. Its [actual target Actions run](https://github.com/celikapo/gpu-monte-carlo-var/actions/runs/39890809091)
completed successfully at 02:40:14 UTC: 1/1 job, cpu, passed. Configure, build,
existing CTest suite and representative serial/CSV/invalid-input steps passed.
This is hosted CPU execution, not CUDA execution or statistical acceptance.

This follow-up documentation commit records the verified initial publication;
the run above belongs specifically to the initial SHA. Subsequent revisions
have their own exact-SHA workflow runs. No force-push, history transfer or
academic submission was performed.
