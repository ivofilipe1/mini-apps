# Trajectory

A single-file weight and calorie tracker that smooths your scale readings, fits your
real energy expenditure from your own logs, and projects your weight forward.

No build step, no dependencies, no server, no accounts. `index.html` is the whole
application: open it in a browser, or host it as a static file.

## Running it

Open `index.html`. That is all.

The profile ships with placeholder values (35, 175 cm, 80 kg, 2,000 kcal). The setup
dialog opens by itself the first time you load the page so you can replace them.
Skipping it is fine; the values are editable from Settings at any point.

It is also served from GitHub Pages at
[ivofilipe1.github.io/mini-apps/trajectory/](https://ivofilipe1.github.io/mini-apps/trajectory/).
Nothing needs compiling — Pages serves this directory's `index.html` as-is.

Data is stored per browser origin. The hosted copy and a local copy of the file keep
separate stores, and they do not sync.

## What it does

1. Log a date, a scale weight, and a calorie intake.
2. The scale reading is smoothed into a trend line.
3. Your actual burn is fitted from the relationship between what you ate and how the
   weight moved, and blended against a formula estimate by how much data exists.
4. The trend is projected forward, with burn recalculated each simulated day.

## The model

### Trend: gap-aware exponentially weighted average

α is the weight given to **one day**, so a reading decays by `(1 − α)` per day of gap
rather than per logged entry. Two weigh-ins fourteen days apart leave the older one at
`0.8^14 ≈ 4%` influence, not 80%.

```
decay = (1 − α)^(days since previous weigh-in)
num   = num · decay + weight
den   = den · decay + 1
trend = num / den
```

The numerator/denominator pair normalises by the weight actually accumulated, so the
early trend is not anchored to the seed value. With one entry the trend equals that
entry. With daily logging it reduces exactly to `EWMA_t = α·W_t + (1−α)·EWMA_(t−1)`.

### Burn: weighted least squares on the energy-balance identity

```
E_t = ρ · W_t                 body energy store, ρ = 7,700 kcal/kg
E_t = E_0 + C_t − TDEE · t    C_t = cumulative intake since day 0
→     z_t = ρ·W_t − C_t = E_0 − TDEE·t
```

Regressing `z` on `t` over a 28-day window gives burn as the negative slope. Every
weigh-in contributes, weighted by a 14-day exponential decay on age, so one
water-weight day nudges the answer instead of swinging it the way an endpoint
difference does. The standard error of the slope is reported alongside the estimate.

The regression uses **raw** scale readings, not the smoothed trend: least squares
already does the smoothing, and the trend's lag would shrink the observed change
across the window and bias burn roughly 60 kcal low at half a kilo per week.

The fit is bounded to 0.55–1.75× the formula estimate, then blended:

```
burn = confidence · fitted + (1 − confidence) · formula
```

Confidence rises with window span, weigh-in count, and the share of days with intake
logged. Two weigh-ins barely move the number; a month of daily logs replaces the
formula almost entirely.

### Formula fallback: Mifflin-St Jeor

```
BMR = 10·kg + 6.25·cm − 5·age + 5   (male)
BMR = 10·kg + 6.25·cm − 5·age − 161 (female)
TDEE = BMR × activity factor
```

Used alone until there is enough data to fit, and as the anchor the fitted value is
blended against.

### Projection

Day-by-day simulation over the chosen horizon. BMR is recomputed from the simulated
weight every day, so resting burn falls about 10 kcal per kilogram lost and the curve
flattens rather than running in a straight line to zero.

## Known limitations

- **Garbage in, garbage out.** The fit cannot distinguish under-reported food from a
  slower metabolism. Systematic under-reporting averages 12–16% in research and
  inflates the burn estimate proportionally.
- **7,700 kcal/kg assumes fat.** Early loss is largely glycogen and water, so the
  fitted burn reads high in the first weeks and settles as data accumulates.
- **The standard error is internal precision, not accuracy.** It describes how well
  the line fits your points, not how close the answer is to your true expenditure.
- **Not the full dynamic model.** Burn falling with mass is modelled; fat/lean
  partitioning and adaptive thermogenesis are not. See the NIH Body Weight Planner
  for a research-grade treatment.

## Privacy

- Everything is computed and stored in the browser via `localStorage`. Nothing is
  uploaded.
- Zero external requests: no CDN, no webfont, no analytics, no tracking pixel. Verify
  with `grep -c 'https\?://' index.html` — the answer is 0.
- A Content-Security-Policy meta tag sets `connect-src 'none'`, so the page cannot
  make a network request even if markup were somehow injected into it.
- Imported JSON is whitelist-validated. Entries outside physiological bounds are
  dropped; profile and settings keys not in the spec are discarded.
- Exported JSON contains personal health data. `.gitignore` excludes it. Keep it that
  way.

## References

The equations are published science and are not covered by copyright. Listed for
provenance and so the choices can be checked.

- Mifflin MD, St Jeor ST, Hill LA, Scott BJ, Daugherty SA, Koh YO. A new predictive
  equation for resting energy expenditure in healthy individuals. *Am J Clin Nutr*
  1990;51(2):241–247.
- Hall KD, Chow CC. Why is the 3500 kcal per pound weight loss rule wrong?
  *Int J Obes* 2013;37(12):1614.
- Hall KD, et al. Quantification of the effect of energy imbalance on bodyweight.
  *The Lancet* 2011;378(9793):826–837. (NIH Body Weight Planner)
- NIH Body Weight Planner: https://www.niddk.nih.gov/bwp

## Disclaimer

This is a personal tool, not a medical device. It produces estimates from noisy inputs
and is not a substitute for advice from a doctor or dietitian. Do not use it to
justify an aggressive calorie deficit.

## Licence

MIT. See [LICENSE](../LICENSE).
