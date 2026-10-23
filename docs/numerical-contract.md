# Numerical contract and architecture

Use double precision and a positive long holding V0=q*S0, q>0, S0>0. CSV uses
q=1; the calibration API also accepts positive units. Annual price drift mu is
not mean log return; volatility sigma is per sqrt(year), and horizon T is years.

For n log returns r_i=log(P_i/P_(i-1)), use sample variance:

```text
m = sum(r_i)/n
s2 = sum((r_i-m)^2)/(n-1)
dt = 1 / observations_per_year
sigma = sqrt(s2/dt)
mu = m/dt + 0.5*sigma*sigma
T = horizon_trading_days / observations_per_year
VT = V0*exp((mu-0.5*sigma*sigma)*T + sigma*sqrt(T)*Z)
L = V0-VT
```

Z is standard normal. Exact terminal sampling needs no time discretization.
Sort losses ascending and take zero-based rank ceil(alpha*N)-1 without
interpolation, alpha=0.95 and 0.99. Retain negative VaR. Analytical VaR is:

```text
V0 - V0*exp((mu-0.5*sigma*sigma)*T
           + sigma*sqrt(T)*Phi_inverse(1-alpha))
```

The unchanged full-project statistical acceptance is, separately per engine
and confidence, N=10000000 and five independent seed settings 42,123,456,789,2026:

```text
abs(mean(VaR)-analytical_VaR)
<= 0.01*max(abs(analytical_VaR),0.01*V0)
```

This is error of the mean, not mean absolute error or an individual-seed rule.
It is not certified by this snapshot's small runs or deterministic tests.
The unchanged common-input cross-engine tolerance is absolute VaR difference
<=0.00001*V0. Only one engine is included, so no cross-engine acceptance is
claimed. Memory/race checks are separate from numerical agreement.

CLI -> validated prices -> calibration/Model -> Request -> Engine::run -> Result
-> analytical comparison/text or JSON. The shared Engine boundary accepts
optional read-only caller-owned common normals of exactly N elements. The serial
backend owns RNG, temporary losses, simulation and sorting. This interface does
not mandate per-scenario host callbacks or a host loss vector for future engines.

Native RNG uses mt19937_64 and std::normal_distribution. Repetition is expected
within the same build; distribution output need not match across standard
libraries or other backends. Equal seeds across engines would not imply common
samples. Common-input tests bypass native RNG.

The engine's monotonic wall timer includes per-run allocation, RNG, simulation,
quantile and temporary-buffer cleanup. Shared CSV/calibration, process startup
and output are excluded. CLI invocations use fresh processes; a small elapsed
value is illustrative, not a performance campaign or thermal-equilibrium claim.

GBM assumes constant drift/volatility and independent normal log increments.
Jumps, heavy tails and volatility clustering limit real-market validity. VaR
is a model quantile, not a maximum possible loss.
