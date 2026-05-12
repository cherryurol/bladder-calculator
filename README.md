# Bladder Efficiency Tracker (BET) v4.3

A web-based tool for quantitative assessment of bladder storage and voiding efficiency from standard voiding diary data.

**Live calculator:** https://cherryurol.github.io/bladder-calculator/

**Parameter calibrator:** https://cherryurol.github.io/bladder-calculator/Parameter%20Calibrator.html

## Overview

BET derives two biomechanical indices from a standard frequency–volume chart:

- **SEI** (Storage Efficiency Index) = `MA × DA × 100%`
- **VEI** (Voiding Efficiency Index) = `√(Qavg / Qref) × MA × 100%`

where:

- **MA** (Magnitude Adjustment) is a piecewise-linear function of voided volume, anchored at Vmin and Vopt
- **DA** (Diuresis Adjustment) penalises filling conditions that fall outside the physiological window
- **Qavg** is the average flow rate (volume / duration); **Qref** is the reference flow

The framework is grounded in a hydrostatic skeleton biomechanical model of bladder accommodation.

## What's new in v4.3

The Diuresis Adjustment function is extended to a symmetric dual-penalty formulation:

| Fill rate | DA value |
|---|---|
| < RFR | FillRate / RFR (slow-filling penalty — unchanged from v4.2) |
| RFR ≤ FillRate ≤ 1.5 × RFR | 1.0 (physiological window) |
| > 1.5 × RFR | max(0.6, 1.0 − 0.05 × (FillRate − 1.5 × RFR)) (induced-diuresis penalty) |

This corrects an asymmetry in v4.2, where DA was capped at 1.0 for rapid filling and induced diuresis (excess fluid intake, polyuria, diuretic effect) was not penalised at the per-event SEI level. The Parameter Calibrator is unchanged.

A technical addendum demonstrating (i) equivalence of v4.2 and v4.3 in the physiological filling regime and (ii) corrective behaviour of v4.3 outside that regime is available on request.

## Reproducibility of the Monte Carlo validation study

The exact version of the calculator used to generate the validation results reported in our manuscript is preserved as a tagged release:

→ **[v4.2-validation](https://github.com/cherryurol/bladder-calculator/releases/tag/v4.2-validation)**

The validation cohort operates entirely within the physiological filling regime (maximum patient-mean fill rate 2.26 mL/min, against the v4.3 penalty threshold of 3.0 mL/min); v4.2 and v4.3 produce mathematically identical SEI/VEI values under these conditions, and the published discrimination results apply to v4.3 without re-computation.

## Usage

1. Enter the time, voided volume (mL), and duration (seconds) for each voiding event
2. The calculator returns the per-event SEI, VEI, and session averages
3. After 7+ entries, a trend panel becomes available (Δ SEI, IQR, AF Ratio, D/N Ratio) with a verdict on improvement, pseudo-improvement, deterioration, or stable state
4. Reliable longitudinal interpretation requires ≥ 21 entries

Calculator parameters (Vmin, Vopt, Qref, RFR) may be adjusted via the Parameter Calibrator using the patient's own physiological baseline.

## Disclaimer

This tool is intended for research and educational use. It is not a medical device, has not been cleared by any regulatory authority, and is not a substitute for clinical evaluation by a qualified healthcare professional. See [DISCLAIMER.md](DISCLAIMER.md).

## License

Released under the [MIT License](LICENSE).

## Contact

**Igor O. Vishnevskyi, MD, PhD**
Department of Urology, Drohobych City Hospital No. 1, Ukraine
cherryurol@gmail.com
ORCID: [0000-0003-0561-7678](https://orcid.org/0000-0003-0561-7678)
