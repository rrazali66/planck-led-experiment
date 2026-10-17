# Measuring Planck's Constant from LED Threshold Voltages

An interactive, dependency-free web tool for the classic LED determination of Planck's constant.
Single `index.html` — no build step, no CDN, works offline.

## Physics

An LED emits when the applied forward voltage supplies enough energy to lift an electron across
the junction band gap:

```
e·V₀ = h·ν = h·c/λ        →        1/λ = (e/hc)·V₀
```

Plotting `1/λ` against the threshold voltage `V₀` gives a straight line whose gradient is `e/hc`,
so

```
h = e / (m·c)
```

The tool fits `1/λ = m·V₀ + b` by **unweighted least squares** and propagates the standard error
of the slope into `h`:

```
σ_h = h · (σ_m / m)
```

The intercept `b` is deliberately **not** forced to zero. A real LED's first-glow threshold sits
below `E_g/e`, so `b > 0` is physically expected; it does not bias the gradient, which is why the
gradient — never an individual data point — is the quantity that gives `h`.

## Features

- Editable data table (wavelength, threshold voltage) with add / reset / clear
- Per-row `1/λ`, `E_g`, `V₀/E_g`, single-point `h` and residual columns
- Include/exclude checkbox per LED for "what if I drop this point?" experiments
- Live scatter + fit chart with optional axis extension to `V₀ = 0` to expose the intercept,
  and an optional line forced through the origin for comparison
- Diagnostic flags that fire only when the data actually warrant them
- CSV export, plain-text summary copy, and print/PDF stylesheet

## Usage

Open `index.html` in any browser. Replace the example data with your own; the fit, the diagnostics
and the graph update as you type.

## Reference

`e = 1.602176634×10⁻¹⁹ C`, `c = 2.99792458×10⁸ m/s`, `h_CODATA = 6.62607015×10⁻³⁴ J·s`.
