# Bladder Efficiency Tracker (BET) v4.2

A web-based tool for quantitative assessment of bladder storage and voiding efficiency from standard voiding diary data.

**Live calculator:** [https://cherryurol.github.io/bladder-calculator/](https://cherryurol.github.io/bladder-calculator/)

## Overview

The Bladder Efficiency Tracker derives two composite biomechanical indices — Storage Efficiency Index (SEI) and Voiding Efficiency Index (VEI) — from voiding diary entries (time, volume, voiding duration). The theoretical foundation is the hydrostatic skeleton (HSK) principle applied to bladder mechanics.

**Associated publications:**
> Vishnevskyi I. Urinary Bladder Mechanics: Potential Role of Hydrostatic Skeleton Design Principle. Open Discussion ePosters 790, ICS 2024.

## Core Indices

### Storage Efficiency Index (SEI)

```
SEI = MA × DA × 100%
```

- **MA (Mechanical Advantage)** = clamp((V − Vmin) / (Vopt − Vmin), 0, 1)
  - Reflects volume adequacy relative to calibrated target
- **DA (Displacement Advantage)** = min(1.0, (V / Tfill) / RFR)
  - Reflects whether the fill interval allowed adequate distension
  - Set to 1.0 for nocturnal voids to prevent sleep-related artifacts

### Voiding Efficiency Index (VEI)

```
VEI = clamp(√(Qavg / Qref) × MA, 0, 1) × 100%
```

- **Qavg** = V / Duration (average flow rate)
- **Qref** = reference flow rate (default 12.0 ml/s)

## Calibration Parameters

| Parameter | Description | Default | Range |
|-----------|-------------|---------|-------|
| Vmin | Minimum functional volume (ml) | 100 | 50–150 |
| Vopt | Target optimal volume (ml) | 350 | 150–500 |
| Qref | Reference flow rate (ml/s) | 12.0 | 8–15 |
| RFR | Reference fill rate (ml/min) | 2.0 | 1.0–3.0 |

Defaults represent typical adult values. Calibration should be adjusted based on the patient's clinical profile (age, sex, diagnosis).

## Trend Analysis Metrics

| Metric | Formula | Interpretation |
|--------|---------|---------------|
| Δ SEI | Median(last 7) − Median(previous 7) | ≥ +5: improvement; ≤ −5: deterioration |
| IQR | Q75 − Q25 of SEI | < 15: stable; ≥ 15: high variability |
| AF Ratio | Proportion of entries with fill rate > 1.5× median | > 0.4: possible pseudo-improvement |
| D/N Ratio | Median(night SEI) / Median(day SEI) | < 0.7: nocturia concern |

Trend analysis requires a minimum of 21 entries for reliable interpretation.

## Efficiency Patterns

The associated simulation study defines five patterns:

| Code | Name | SEI | VEI | Description |
|------|------|-----|-----|-------------|
| HH | High–High | >70% | >70% | Efficient storage and voiding |
| HL | High–Low | >50% | <35% | Preserved storage, impaired voiding |
| LH | Low–High | <35% | Variable | Impaired storage, variable voiding |
| LL | Low–Low | <25% | <25% | Both severely impaired |
| MM | Moderate | 40–60% | 35–55% | Both moderately reduced |

## Usage

### As a web application

1. Open [the calculator](https://cherryurol.github.io/bladder-calculator/)
2. Enter voiding events (time, volume, duration)
3. View real-time SEI/VEI calculations and trend analysis
4. Export data as JSON for backup or sharing

### Running locally

```bash
git clone https://github.com/cherryurol/bladder-calculator.git
cd bladder-calculator
# Open index.html in any browser — no dependencies required
```

## Test Scenarios

Built-in test generators validate algorithm behavior:

- **Positive Trend** — simulates improving storage over 14 entries
- **Pseudo-Improvement** — simulates artificially high volumes with shortened intervals (AF Ratio detection)
- **Negative Trend** — simulates declining storage capacity

## Technical Details

- Pure HTML/CSS/JavaScript — no external dependencies
- Data stored locally in browser (localStorage)
- JSON import/export for data portability
- No server communication — all computation is client-side

## Important Notice

This tool is designed for research and self-monitoring purposes. It is **not a diagnostic device**. BET generates biomechanical efficiency patterns, not clinical diagnoses. Abnormal patterns should be evaluated by a qualified healthcare provider in the context of the patient's history, examination, and confirmatory testing.

## References

1. Vishnevskyi I. Urinary Bladder Mechanics: Potential Role of Hydrostatic Skeleton Design Principle. Open Discussion ePosters 790, ICS 2024.
2. Abrams P, et al. The standardisation of terminology of lower urinary tract function. Neurourol Urodyn. 2002;21(2):167–178.
3. Rosier PF, et al. International Continence Society Good Urodynamic Practices and Terms 2016. Neurourol Urodyn. 2017;36(5):1243–1260.

## License

MIT License — see [LICENSE](LICENSE) file.

## Authors

- **Igor O. Vishnevskyi, MD, PhD** — Department of Urology, Drohobych City Hospital No. 1, Ukraine
- **Maxim I. Vishnevskyi, MD** — Department of Urology, Drohobych City Hospital No. 1, Ukraine

## Citation

If you use this tool in your research, please cite:

```
Vishnevskyi I. Urinary Bladder Mechanics: Potential Role of Hydrostatic
Skeleton Design Principle. Open Discussion ePosters 790, ICS 2024.
```
