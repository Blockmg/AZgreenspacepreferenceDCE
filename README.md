# AZgreenspacepreferenceDCE

Discrete choice experiment (DCE) on greenspace preferences in Southern Arizona
(Positly sample, July 2026).

## Running the analysis

1. Open `AZgreenspacepreferenceDCE.Rproj` in RStudio (so `here::here()` finds the project root).
2. Install the packages once: `install.packages(c("qualtRics", "tidyverse", "janitor", "apollo", "readxl", "here"))`.
3. Render or run `Positly Survey 10.17.2026.qmd`.

Inputs are all in the repo: the Qualtrics exports in `data/` (see `data/README.md`) and the
design workbook `SCORCH DCE Experimental Design Positly.xlsx`. Nothing is picked by hand.

Outputs go to `output/`: Apollo's own files for each model (`*_output.txt`,
`*_estimates.csv`, ...) and the reporting tables (`mnl_results_table.csv`, ...). Commit
`output/` after each run whose numbers are reported (poster, manuscript), so the reported
results can be traced to code + data.

## Models estimated

| Apollo model name | What it is |
|---|---|
| `MNL_DCE_main` | Headline MNL, no interaction |
| `MNL_DCE_plant_x_AZ` | Adds plant type x 10+ years in AZ (LR test in `lr_test_interaction.csv`) |
| `MNL_DCE_quality` | Headline model without respondents flagged by the data-quality rules (`docs/data-quality.md`) |
| `MNL_DCE_tucson_zip` / `MNL_DCE_non_tucson_zip` | Headline model split by ZIP (856-857 vs. the rest), with a pooling LR test |

`analysis_sample` near the top of the model chunk picks the headline sample:
`"all"` (everyone who said they live in Southern Arizona) or `"tucson_zip"` (856-857 ZIPs only).
