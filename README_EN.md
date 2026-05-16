# HRV Analysis Pipeline

End-to-end heart rate variability (HRV) analysis pipeline in Python.
Implements statistical, geometric, correlation and spectral methods, plus a composite
PARS score following the Bayevsky standard.

[Русская версия](README.md)

## What is inside

| Section | Method | Metrics |
|---|---|---|
| 1 | Time-domain | HR, SDNN, CV, RMSSD, pNN50 |
| 2 | Geometric | Mode (Mo), AMo, MxDMn, Stress Index (SI) |
| 3 | Correlation analysis | CC1, CC0, Poincaré plot |
| 4 | Spectral analysis (FFT) | VLF, LF, HF, IC, LF/HF, ISCA |
| 5 | Composite assessment | PARS score (1–10) |

## Approach

- **Spectral analysis:** cubic spline interpolation → detrending → Hann window → FFT → trapezoidal integration over VLF / LF / HF bands.
- **Poincaré plot:** one of the key methods used for detection of ectopic beats (extrasystoles).
- **PARS:** composite score for functional state assessment (Bayevsky standard, widely used in Russian clinical and applied physiology).
- **Stack:** NumPy, SciPy (`CubicSpline`, `numpy.fft`), pandas, matplotlib.

## Results on demo data

| Metric | Value | Norm |
|---|---|---|
| HR | 80.5 bpm | 60–80 |
| SDNN | 21.9 ms | 40–80 |
| RMSSD | 24.5 ms | 20–50 |
| pNN50 | 4.7% | > 20 |
| SI (Stress Index) | 343.5 a.u. | 80–150 |
| LF/HF | 0.54 | 0.5–2 |

![HRV spectrum](figures/fig5_spectrum.png)
![Poincaré plot](figures/fig3_scatterogram.png)
![Variational pulsogram](figures/fig1_histogram.png)

## How to run

```bash
git clone https://github.com/<username>/hrv-analysis.git
cd hrv-analysis
pip install -r requirements.txt
jupyter notebook hrv_pipeline.ipynb
```

## Structure

```
hrv-analysis/
├── hrv_pipeline.ipynb      # main notebook
├── data/
│   └── rr_intervals.csv    # sample data (synthetic)
├── figures/                # figures saved by the notebook
├── requirements.txt
├── README.md / README_EN.md
└── LICENSE
```

## Using your own data

Replace `data/rr_intervals.csv` with a single-column file of RR-intervals in milliseconds (no header). Lines starting with `#` are ignored.

## References

- Bayevsky R. M. (2001). Analysis of heart rate variability in space medicine. *Human Physiology*.
- Task Force of the European Society of Cardiology (1996). Heart rate variability. *Circulation*, 93(5), 1043–1065.
- Shaffer F., Ginsberg J. P. (2017). An overview of heart rate variability metrics and norms. *Frontiers in Public Health*, 5:258.

## Author

Anastasiia Birdina · birdinanastia@gmail.com

## License

MIT — see [LICENSE](LICENSE).
