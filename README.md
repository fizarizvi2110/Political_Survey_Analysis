# Religion, Party ID, and Abortion Attitudes (GSS 2021)

OLS analysis of how religiosity and party identification jointly shape
self-identification as pro-choice, using the 2021 General Social Survey
(n = 4,032; analytic n = 2,718 after listwise deletion).

## Question

Religiosity and Republican identification are correlated, and both correlate
with abortion attitudes. The analysis separates their contributions: does
religiosity predict abortion stance independently of party, and does the
effect of each depend on the level of the other?

## Data and measurement

| Original | Recoded | Scale |
|---|---|---|
| `relpersn` | `religiousness` | 0 = not at all, 1 = somewhat, 2 = very |
| `partyid` | `republican` | 0 = Democrat, 1 = Independent, 2 = Republican (other party → NA) |
| `prochoic` | `prochoice` | 0 = strongly disagree … 3 = strongly agree ("neither" → NA) |

Collapsing the 7-point `partyid` into three categories and dropping the
neutral midpoint of `prochoic` are the two consequential measurement
decisions; both are documented in the paper with the resulting frequency
distributions.

## Approach

1. **Bivariate** — each path in the triangle estimated separately.
2. **Conditional** — the religiosity effect within each party, and the party
   effect within each religiosity level, to check for heterogeneity before
   specifying an interaction.
3. **Multivariate** — additive model, then a `religiousness × republican`
   interaction.

## Results

Additive model: Both coefficients shrink relative to their bivariate counterparts
(−0.703 and −0.625), consistent with the two predictors carrying
overlapping information (r = 0.248).

Interaction model (R² = 0.344, interaction term −0.121, p < .001) implies
separate slopes by party:

| Party | Intercept | Religiosity slope |
|---|---|---|
| Democrat | 2.771 | −0.452 |
| Independent | 2.370 | −0.572 |
| Republican | 1.968 | −0.706 |

Religiosity depresses pro-choice identification in every party, but the
gradient is steepest among Republicans, and non-religious Republicans start
from the lowest baseline.

## Limitations

- **Cross-sectional.** The path diagram is a framing device for the
  estimation order, not identified mediation. Nothing here supports a
  causal reading.
- **OLS on an ordinal outcome.** Treating a 4-category agreement scale as
  interval assumes equal spacing between adjacent categories. An ordered
  logit is the appropriate robustness check and is not run here.
- **Unweighted.** GSS design weights are not applied, so estimates are
  sample- rather than population-representative.
- **Listwise deletion.** `prochoic` is missing for ~30% of respondents,
  partly by questionnaire design. Missingness is not modelled.
- **No covariates.** Age, education, region, and denomination are all
  plausible confounders and none are included.

## Reproducing

Place `gss2021.dta` in `data/` (see `data/README.md`), then knit
`analysis/abortion_attitudes.Rmd`. Requires `haven`, `car`, `descr`,
`tidyr`.
