# Weeks 7-8 academic submission snapshot

Single-asset GBM Value at Risk in C++17: strict CSV input, log-return calibration,
exact terminal serial Monte Carlo, an analytical reference and 95%/99% outputs.
The contribution is computational correctness; no predictive market validity or
investment suitability is claimed.


## Build and test

Requires CMake >=3.18 and a C++17 compiler. No downloaded dependencies, GPU,
CUDA Toolkit or private input is needed. The root build has only a serial CPU
engine, with no optional CUDA configuration or Toolkit discovery.

```sh
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=ON
cmake --build build --config Release --parallel
ctest --test-dir build -C Release --output-on-failure
```

For Visual Studio 2022, add `-G "Visual Studio 17 2022" -A x64` to configure.
The existing four CTests cover core mathematics/common inputs, CSV/calibration,
JSON serialization and CSV CLI smoke. See [validation](docs/validation.md).

## Run

Linux / single-configuration build:

```sh
./build/mc_var --version
./build/mc_var 10000 42
./build/mc_var --csv data/synthetic_prices.csv 10000 42 10 252
./build/mc_var --csv data/synthetic_prices.csv 10000 42 10 252 --json
```

Windows Visual Studio: replace `./build/mc_var` with
`.\build\Release\mc_var.exe`. Fixed mode uses V0=100, annual mu=0.05,
sigma=0.20 and T=1 year. CSV mode holds one unit, uses the latest close for V0,
and takes horizon trading days and observations/year (defaults 10 and 252).
Each successful run returns simulated and analytical VaR at both confidences.
Zero scenarios, for example `mc_var 0 42`, must return a useful error and exit 1.
Backend/thread selection is outside this version; extra arguments fail explicitly.

CSV requires the exact header `date,close`, two columns, increasing unique valid
YYYY-MM-DD dates, finite positive prices, decimal dots and at least three prices.
BOM/CRLF are supported; malformed rows are rejected, never skipped. No sorting,
filling, price adjustment or missing-trading-session detection is performed.

[data/synthetic_prices.csv](data/synthetic_prices.csv) is the existing hand-written
12-price software fixture, not historical market data. Its dates are fixture
labels, not evidence of market observations. Prices use arbitrary units; there
is no ticker, currency, provider adjustment or external redistribution condition.
No provider data or private correspondence is included. See its exact-byte hash
and origin in [provenance](docs/provenance.md).

## Scope and evidence

- [Numerical contract and architecture](docs/numerical-contract.md)
- [Requirements coverage with stable FR/NFR IDs](docs/requirements.md)
- [Source provenance, schedule sources and attribution](docs/provenance.md)
- [Validation and historical CUDA compatibility limits](docs/validation.md)
- [Target CPU workflow](https://github.com/celikapo/gpu-monte-carlo-var/actions/workflows/build.yml)
  runs one Ubuntu Release job. The initial exact-SHA run passed (see validation).

OpenMP, an end-to-end CUDA VaR skeleton, full CUDA/hybrid engines, full statistical
acceptance campaigns, formal performance benchmarks, convergence, DRAM profiling
and final-demo packages are outside this snapshot. The standalone historical CUDA
compatibility probe is an early foundation record, not a VaR engine. Academic
reports, slides and submission uploads are outside this repository.
