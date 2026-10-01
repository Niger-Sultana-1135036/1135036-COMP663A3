### Niger Sultana

ID: 1135036

### Project Title

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

Required packages: 
numpy
pandas
matplotlib
scipy (specifically scipy.stats.binom in Task 2 and scipy.spatial.distance in Task 4), pulled directly from the actual imports in the notebook, not from memory.

Data file: COMP663_Assignment3_PlanningData_2000.csv must be in data folder; Task 5 doesn't need a separate file since it slices the subset in-memory from Task 1's data.

Run order: top to bottom, once, since later tasks reuse variables and functions from earlier ones (there's no task that runs standalone from a fresh kernel).
Random seeds table: every seed used anywhere in the notebook (663 and 42 for Task 2's demos, 42/1/7 for Task 3, 42 for Task 5), with what each is for.
Non-default settings: that the 2,000-cell file is used as-is with no resampling, the NSGA-II settings for both the full problem and the 14-cell subset, and the hypervolume reference point and normalization convention.
