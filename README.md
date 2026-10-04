# Bangladesh Macroeconomic Analysis (2000–2024)

**Author:** Sabahun Salam · Columbia SIPA (MPA, International Finance & Economic Policy) · UC Berkeley B.A. Economics
**Data:** World Bank Open Data API (World Development Indicators), pulled live in the notebook
**Stack:** Python · pandas · NumPy · matplotlib · seaborn · requests

A 13-section, reproducible study of Bangladesh's growth model and its external vulnerabilities, benchmarked against Vietnam, Pakistan, and Cambodia. Sections 1–8 establish the empirical record; Sections 9–13 apply the questions a sovereign-credit or development-finance analyst would ask next.

**Read the findings memo:** [Bangladesh's External Debt Is a Liquidity Problem, Not a Solvency Problem](Salam_Sabahun_BDExternalDebtLiquidityProblem.pdf) (writing sample, October 2026)

## Headline findings

| # | Question | Finding |
|---|----------|---------|
| 1 | What did growth deliver? | Real GDP growth averaged 6.1% (2000–2019); the $2.15/day poverty rate fell from 41.4% (2000) to 5.9% (2022). |
| 3 | What funds the external account? | Remittances ($27.5bn, 6.1% of GDP in 2024) dwarf FDI (0.28% of GDP in 2024, down from 1.74% in 2013). |
| 9 | Is the debt path safe? | Solvency looks moderate (external debt 22.3% of GNI) but liquidity has deteriorated: debt service rose from 4.9% of exports (2016) to 15.8% (2024), above the IMF/WB 15% threshold for medium debt-carrying capacity; reserves fell from 6.3 to 3.1 months of imports (2021→2024). |
| 10 | What breaks the model? | A 20% remittance shock ($5.5bn, 1.22pp of GDP) widens the current-account deficit from 0.67% to 1.89% of GDP; a 25% shock takes it to 2.20%. |
| 13 | How large is that shock against the buffer? | Reserves halved from $46.2bn (2021) to $21.4bn (2024); short-term debt rose from 39.2% to 60.5% of reserves. A 20% remittance shock equals 25.7% of 2024 reserves; a 25% shock equals 32.2%. |
| 11 | How big is the FDI gap? | Cumulative FDI 2010–2024: Bangladesh $28bn vs. Vietnam $200bn, a $172bn gap between economies of similar size. |
| 12 | How does the currency feed prices? | Bivariate OLS, 2001–2024 (24 obs.): inflation = 6.47 + 0.105 × depreciation (%), a weak positive association (R² = 0.05) that is not statistically significant. Household consumption fell from 75.0% to 70.1% of GDP while investment rose from 23.8% to 30.7%. |
| 6 | Does education lift female LFP? | Literacy rose from 47.5% to 74.7% (2001–2019), but female LFP five years later rose far less and fell after 2022 (43.7% → 38.7%): the education-to-work channel is not closing. |

## Sections

| Section | Content | Chart |
|---------|---------|-------|
| 1 | Macro overview: GDP growth, inflation, poverty, FDI (2×2 grid + normalized view) | `chart_01_macro_overview.png` |
| 2 | Peer comparison: GDP growth and poverty vs. Vietnam, Pakistan, Cambodia | `chart_02_peer_comparison.png` |
| 3 | Remittances vs. FDI as capital inflows | `chart_03_remittances_vs_fdi.png` |
| 4 | Female labor-force participation and Human Capital Index (peer comparison) | `chart_04_female_lfp_hci.png` |
| 5 | Exchange rate and external debt | `chart_05_exchange_rate_debt.png` |
| 6 | Literacy → female LFP with a 5-year lag (10 lagged pairs) | `chart_06_literacy_lfp_lag.png` |
| 7 | Political-cycle overlay on six indicators | `chart_07_political_cycle_overlay.png` |
| 8 | COVID-19 shock and recovery vs. peers | `chart_08_covid_resilience.png` |
| 9 | External debt sustainability: debt service/exports, debt/GNI, reserves cover vs. IMF/WB thresholds | `chart_09_debt_sustainability.png` |
| 10 | Remittance shock stress test (partial-equilibrium current-account effect) | `chart_10_remittance_stress_test.png` |
| 11 | FDI gap with Vietnam (cumulative 2010–2024) | `chart_11_vietnam_fdi_counterfactual.png` |
| 12 | Exchange-rate pass-through OLS and demand-side growth decomposition | `chart_12_passthrough_decomposition.png` |
| 13 | Liquidity extensions: reserves in US$, short-term debt, remittance shock as a share of reserves; supporting figures cited in the memo | printed output |

## Reproduce

```bash
pip install -r requirements.txt
jupyter notebook Bangladesh_Analysis.ipynb   # Run All; charts regenerate into the working directory
```

The notebook fetches every series from `api.worldbank.org/v2` with retry logic; no local data files are required. The API can be slow, so a full run may take several minutes. Indicator codes are listed in each pull cell (e.g. `NY.GDP.MKTP.KD.ZG`, `BX.TRF.PWKR.DT.GD.ZS`, `DT.TDS.DECT.EX.ZS`, `FI.RES.TOTL.CD`, `DT.DOD.DSTC.IR.ZS`).

## Method notes and limitations

- **2016 data break:** Bangladesh's GDP in current dollars rises 36% in 2016 ($195.1bn → $265.2bn) because of the official national-accounts rebasing. Ratios with GDP or GNI in the denominator (remittances, external debt, demand shares) drop in 2016 for statistical rather than economic reasons. Comparisons within 2016–2024 are consistent; across that break, use dollar figures.
- The 15% debt-service threshold in the IMF/World Bank framework applies to public and publicly guaranteed debt service; `DT.TDS.DECT.EX.ZS` covers total external debt service, so the comparison is indicative.
- Poverty (`SI.POV.DDAY`) is survey-based and available only for 2000, 2005, 2010, 2016, 2022.
- The remittance stress test is partial-equilibrium: it holds imports and other flows fixed and reports the first-round current-account effect only.
- The pass-through regression is a bivariate OLS on 24 annual observations (2001–2024; the first depreciation value needs a prior year). R² = 0.05 and the slope is not statistically significant (t ≈ 1.1). It is descriptive, not causal, and does not control for global commodity prices or monetary policy. The taka was managed for most of 2020–2024 (a crawling peg was introduced in 2024), so 2020–2024 is shown separately as a recent period, not a free float.
- The 5-year literacy→LFP lag is a correlation exercise on 10 pairs; it is meant to motivate, not test, a causal channel.
- Political-period boundaries follow election dates; the overlay is descriptive. The 2024 shading is approximate (the government changed in August 2024).

## License

MIT for code; World Bank data under CC BY 4.0.
