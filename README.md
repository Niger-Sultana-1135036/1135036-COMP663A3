### Niger Sultana

ID: 1135036

### Project Title :Multi-Objective Optimisation

Transform the land-use modelling work developed in Assignment 1 and 2 into
a constrained multi-objective land-use planning system. You will work with a supplied fixed sample of
2,000 land cells from the original forest-cover dataset. Each cell must be allocated to exactly one of two
purposes: economic use or environmental preservation.
Your goal is to produce a feasible set of land-use plans and analyse the trade-off between total economic
benefit and total environmental benefit. Economic use is subject to a finite budget, while environmental
preservation must satisfy a minimum representation requirement for every forest cover type. You will
implement the supplied formulation, justify a Pareto-based multi-objective method, and generate and
analyze a Pareto front.

The normalised Inverted Generational Distance (IGD) is small (well under 1% of the front's own objective range), and the hypervolume ratio is very close to 100%, so NSGA-II's front dominates almost the same region of $(f_1,f_2)$-space as the exact optimum despite evaluating roughly 55% as many candidates as full enumeration ($9{,}060$ vs. $16{,}384$) and never being told which candidates were infeasible in advance. The exact-recovery count is lower than 100%, which is expected and not a failure: with only $60$ individuals representing a $54$-point front, the population cannot hold every exact point simultaneously, and small gaps between the true front and its nearest NSGA-II neighbour (visible as the orange points sitting just inside some green circles in the plot above) are enough to miss an exact match while still being very close in objective terms, which is exactly why IGD and hypervolume, not just an exact-match count, are the appropriate measures of approximation quality here. Because this validation is only possible where the *exact* answer is known (the 14-cell instance), it gives good evidence that the same NSGA-II configuration, run at the much larger scale used in Task 3 for the full 2,000-cell problem, is a trustworthy approximation method rather than a black box of unknown quality.

### Required packages: 
numpy
pandas
matplotlib
pandas as pd
math
binom
time
scipy (specifically scipy.stats.binom in Task 2 and scipy.spatial.distance in Task 4), pulled directly from the actual imports in the notebook, not from memory.

### How to run this notebook:

**Environment.** Python 3.14, with:

- `numpy`, `pandas`, `matplotlib`- data handling and plotting (all tasks)
- `scipy`, specifically `scipy.stats.binom` (Task 2, constraint-restrictiveness check) and `scipy.spatial.distance.pdist`/`squareform` (Task 4, front-spacing metric)

No other packages, no GPU.

**Data.** `COMP663_Assignment3_PlanningData_2000.csv` must sit in the **data folder** as this notebook. No other input files are needed.

**Run order.** Cells must be run top to bottom, once, in order (`Kernel → Restart & Run All`). Later tasks reuse variables, arrays and functions created earlier (e.g. `E`, `V`, `C`, `cells`, `B`, `req`, and the NSGA-II building blocks from Task 3 are reused by Task 5), there is no task that can be run in isolation from a fresh kernel.

**Random seeds (fixed, for reproducibility).**
| Where | Seed(s) | Purpose |
|---|---|---|
| Task 2 demos (`rng = np.random.default_rng(663)` / `rng(42)`) | 663, 42 | illustrative decoding example and the 1,000-flip incremental-update check |
| Task 2 feasibility simulation | `rng` seeded via the Task-2 demo cell (5,000 random allocations) | estimating how often a random allocation is feasible |
| Task 3 primary NSGA-II run | **42** | the main reported run (front, hypervolume curve, front evolution plot) |
| Task 3 robustness check | 1, 7 | confirms the seed-42 result is not an artefact |
| Task 5 NSGA-II run on the 14-cell subset | **42** | kept the same as Task 3's primary seed for consistency |

Re-running with a different seed will shift the exact numbers slightly but should not change the qualitative conclusions (Task 3 §3.9 shows final hypervolume is stable to within ±0.002 across seeds 1/7/42).

**Non-default settings worth knowing about** (all stated and justified where they first appear):

- Sampling: the assignment's 2,000-cell file (`DATA_FILE`) is used exactly as supplied, with **no resampling**, min–max scaling in Task 1 is computed over all 2,000 cells as given.
- 
- NSGA-II (Task 3, full 2,000-cell problem): population 150, 300 generations, uniform crossover $p_c=0.9$, bit-flip mutation $p_m=1/n$, binary tournament selection, repair-based constraint handling (§3.4) — all non-default relative to a textbook/library NSGA-II, and justified in §3.2.
- 
- NSGA-II (Task 5, 14-cell subset): population 60, 150 generations, $p_m=1/14$ — deliberately scaled down from Task 3's settings; justified in §5.4's table.
- 
- Hypervolume reference point: $(0,0)$ in both Task 3 and Task 5, normalised by dividing by $\sum E_i\times\sum V_i$ (stated in §3.6 / §5.5).

**Outputs.** Everything the notebook produces (tables, plots, printed summaries) is generated in-place when the notebook runs; nothing needs to be loaded from an external results file.
