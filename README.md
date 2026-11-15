# CS Project 8: Decision Trees vs Neural Networks on Hazardous Asteroids

We classify near Earth asteroids from NASA's Small Body Database as potentially hazardous (PHA) or not, using decision trees and neural networks, and compare what each model learns. NASA's PHA label comes from a known rule (MOID ≤ 0.05 au and H ≤ 22.0), so we can check whether the models pick up the right features.

## Files

| File | What it is |
|---|---|
| `Project8_Asteroid_Hazard_Classification.ipynb` | main notebook with all the code and outputs |
| `Project8_Report.docx` | technical report |
| `Project8_Presentation.pptx` | slides |
| `data/` | data snapshot from the JPL Small Body Database (43,090 asteroids, 14 Nov 2026) |
| `figures/` | all figures as PNG |
| `results/` | `results.json` with every number and `scoreboard.csv` |
| `requirements.txt` | Python packages (exact versions we used) |
| `.venv/` | virtual environment with everything installed |

## How to run

Using the included venv (macOS):

```
source .venv/bin/activate
jupyter notebook Project8_Asteroid_Hazard_Classification.ipynb
```

In VS Code you can also open the notebook and pick the kernel "Python (Cs_Project8 venv)" or the `.venv` interpreter, then Run All. A full run takes about 6 minutes.

The `.venv` folder only works on this Mac in this folder. On another computer, make a new one:

```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

If `data/neo_asteroids_sbdb.csv` is deleted, the notebook downloads a fresh copy from the JPL API. The numbers can change a little since new asteroids keep getting added.

## What the notebook covers

1. Dataset: download, cleaning, checking the label against NASA's rule, plots
2. Decision trees: depth sweep, trees at max_depth 2 and 4 (and 3 and 5 without MOID) drawn with `plot_tree`, bias and variance with bootstrap trees, and which attribute each level splits on
3. Neural networks: four architectures (2, 8, 16 and 8, and 32, 16 and 8 hidden nodes) with 5 seeds each, plus a diagram of each one
4. Edge weights compared with the tree splits
5. Extra experiments without MOID, and some famous asteroids

## Main results

| Model | F1 with MOID | F1 without MOID |
|---|---|---|
| Decision tree (best depth) | 0.989 | 0.778 |
| Network, 2 hidden nodes | 0.936 | 0.066 |
| Network, 8 | 0.979 | 0.662 |
| Network, 16 and 8 | 0.973 | 0.846 |
| Network, 32, 16 and 8 | 0.963 | 0.865 |

Test set scores. Network scores are the mean of 5 seeds.

## Data source

NASA JPL Small Body Database Query API: https://ssd-api.jpl.nasa.gov/doc/sbdb_query.html
