# Electrode porosity feasibility assessment

Can non-destructive plasma measurements (optical emission, thermal imaging, electrical waveforms) estimate electrode porosity? 

Analysis notebook: `SirenOpt_Assesment.ipynb`.

## Environment / setup

Python 3.10 or newer. Only standard open-source scientific packages are used.

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install numpy pandas scipy scikit-learn matplotlib jupyter
```

Versions used: numpy 2.x, pandas 2.x, scipy 1.10+, scikit-learn 1.3+, matplotlib 3.7+.
Nothing depends on a specific version.

## Data

The three provided CSVs are not included in this repository. Place them in a `data/` folder next to the notebook:

```
.
├── SirenOpt_Assesment.ipynb
├── README.md
└── data/
    ├── Sample_Info(in).csv
    ├── OES_Wavelengths(in).csv
    └── Measurement_Data(in).csv
```

If it cannot find the files it raises a `FileNotFoundError` naming the folder it expects.

## How to reproduce the results

Run every cell in order, top to bottom:

```bash
jupyter lab SirenOpt_Assesment.ipynb
```


**Runtime:** about 30 seconds end to end on a Macbook Air M4, dominated by the two shuffle-based checks (1,000 iterations in the thermal section, 500 in the model confidence section).

**Reproducibility:** all random operations draw from a single seeded generator (`RNG = np.random.default_rng(0)`, first cell), so the shuffle checks return identical values on every run. Cells must be run in order, since the generator is consumed sequentially; running cells out of order will change the shuffle results by a small amount.

Every number quoted in the markdown commentary is printed by the notebook itself. Nothing is transcribed by hand.

## Headline results

| Quantity | Value |
|---|---|
| Electrodes / measurements | 20 / 2,000 (100 repeats each) |
| Optical: peak emission vs porosity | r = +0.52, 95% CI +0.10 to +0.78 |
| Thermal: image mean vs porosity | r = +0.41, 95% CI −0.04 to +0.72 (includes zero) |
| Electrical: current crest factor vs porosity | r = −0.58, 95% CI −0.81 to −0.18 |
| R², random split over rows | +0.77 |
| R², split by electrode | +0.17 |
| Best model, typical error | 2.85 vs 3.41 percentage points for guessing the average |
| Electrodes needed for a conclusive study | ~21 to ~38 |

**Conclusion:** the measurements respond to porosity in three independent and mutually consistent ways, but 20 electrodes establish plausibility rather than predictive capability. A study of roughly 40 to 60 electrodes would settle it.