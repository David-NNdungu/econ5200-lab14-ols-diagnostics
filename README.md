# OLS Diagnostics: Robust and Clustered Standard Errors

## Objective

I examine when OLS confidence intervals give reliable coverage and how heteroskedasticity, within-firm dependence and influential observations affect inference.

## Methodology

- I simulate 500 heteroskedastic samples and compare classical, HC1 and HC3 confidence-interval coverage.
- I simulate 300 panels with 40 firms and 25 employees per firm, then compare classical, HC3 and firm-clustered intervals.
- I compare classical, HC0, HC1, HC2, HC3 and clustered standard errors on the same complete-case regression.
- I examine leverage, externally studentised residuals and Cook’s distance for three planted observations.
- I check an AI-generated standard-error table against all 18 reference values and repeat the check after renaming the columns.
- I use the provided diagnostics module to recommend covariance estimation from the study design.
- In the optional extension, I simulate 500 eight-firm panels and compare classical, normal-reference clustered and null-imposed wild cluster bootstrap tests, using all 256 sign patterns per panel.

## Key Findings

### Heteroskedasticity

My nominal 95% intervals cover the true slope in 92.4% of samples with classical standard errors, 94.2% with HC1 and 94.4% with HC3.

The point estimate remains unbiased, but the classical variance formula is inappropriate for this error structure.

### Within-Firm Dependence

With 40 firms, my coverage is:

- Classical: 49.0%.
- HC3: 50.3%.
- Clustered by firm: 93.7%.

In the seed-42 panel, all three methods give the same slope of 1.4927, but their standard errors are 0.0254, 0.0264 and 0.0879, respectively.

HC3 allows unequal error variances but does not account for shared firm shocks.

### Influential Observations

Adding the three planted rows moves my slope from 1.4927 to 1.4468.

A has the highest leverage among the planted rows. C has the largest absolute studentised residual and Cook’s distance, and mainly drives the slope change.

My Cook’s-distance rule flags 44 observations, including 42 unplanted rows. My leverage rule flags 28 observations, including 26 unplanted rows.

I treat these flags as reasons to investigate observations rather than automatically delete them.

### AI-Generated Standard-Error Table

The function passes in one round: all 18 standard errors match statsmodels, and all 18 also match after renaming the columns.

I retain 960 complete regression rows, ignore missing values in unused columns and align firm labels with the estimation sample.

My notebook records the prompt, code, checking log and limitations.

### Optional Few-Cluster Extension

With 8 firms, my rejection rates under a true zero slope are:

| Method | Rejection rate | Monte Carlo SE |
|---|---:|---:|
| Classical | 54.0% | 2.2% |
| Normal-reference clustered | 12.6% | 1.5% |
| Wild cluster bootstrap | 5.2% | 1.0% |

The nominal rejection rate is 5%. Only the wild cluster bootstrap is within two Monte Carlo standard errors of that target in this simulation.

## Files

- `lab-ch14-diagnostic.ipynb`: worked explanations, executed simulations, influence measures and the AI checking log.
- `src/diagnostics.py`: the covariance-recommendation module supplied in the lab.
- `src/se_table.py`: the reusable AI-generated standard-error table function.
- `requirements.txt`: packages used to run the notebook.

## Reproducing the Results

I open the notebook in Google Colab and run the cells in order.

The data are simulated in the notebook, so I need no external dataset or API key. The optional bootstrap may take longer than the core sections.

Round 2 is left unrun because round 1 passed every check.

## AI Assistance

I used ChatGPT to prepare this worked draft, including explanations, Diagnosis 3 code, the expansion prompt and function, and the optional bootstrap code.

The lab restricts AI-written code to the AI-Assisted Expansion and asks for a self-written prompt in a fresh chat. This draft records assisted reference work rather than completion of those independent process requirements.
