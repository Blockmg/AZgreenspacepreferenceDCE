# Data quality: rules, results and a known design flaw

The analysis script flags respondents with four documented rules (chunk
`quality flags` in `Positly Survey 10.17.2026.qmd`) and writes the flags to
`output/quality_flags.csv`.

| Rule | Definition | Flagged (July 31, 2026 data, n = 84) |
|---|---|---|
| Bot risk | reCAPTCHA score < 0.5 | 4 (scores 0.3, 0.3, 0.3, 0.4) |
| Straight-lining | Same side (all A or all B) in every choice task | 1 (all Park A; also has a low reCAPTCHA score) |
| Failed attention check | `QC_agree` answered with anything but "Agree" | 0 (all 41 who saw it passed) |
| Speeder | Duration < 1/3 of the median (median 586 s, cut-off ≈ 195 s) | 0 (fastest was 231 s) |

In total 4 respondents (36 choices) are flagged. The headline model keeps everyone. The `MNL_DCE_quality` model drops the
flagged respondents as a sensitivity analysis
(`output/sensitivity_quality_exclusions.csv`). In the review of 2026-10-23 every
conclusion was unchanged after these exclusions.

## Known design flaw: attention check shown to one block only

`QC_agree` was answered by 40 of 41 block-2 respondents but by 1 of 43 block-1
respondents. The question almost certainly sits inside the block-2 branch of the
Qualtrics survey flow. Block-1 respondents therefore were never screened for
attention, and nothing in the analysis can recover that.

How to report it: say the attention check was shown to block 2 only because of
a survey-flow error, that every respondent who saw it passed, and that the other
three screens (reCAPTCHA, straight-lining, speed) were applied to everyone.

How to fix it for the next wave: move `QC_agree` out of the randomizer/branch so
it sits in a block that every respondent sees (for example right after the
practice choice task, before the randomizer splits into the two DCE blocks), then
use Preview with each block forced to confirm both paths show it.
