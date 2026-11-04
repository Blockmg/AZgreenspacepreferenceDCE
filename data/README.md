# Data

| File | What it is |
|---|---|
| `qualtrics_labels_2026-07-31.csv` | Qualtrics export of the Positly survey, **choice text** (labels). Exported July 31, 2026 11:45. |
| `qualtrics_values_2026-07-31.csv` | The same responses exported as **numeric values**. |

Both files are unzipped, unchanged copies of the two exports that used to sit at the repo
root (`Greenspace+Preferences+Survey+-+Positly_July+31,+2026_11.45 (1).zip` for labels and
`Values Greenspace+...(1) (1).zip` for values). Older copies remain in `R/Archive/`.

They are read with `qualtRics::read_survey()`, which expects the standard 3-row Qualtrics
header (column name, question text, ImportId). Do not open and re-save them in Excel:
that changes ZIP codes and dates. `.gitattributes` marks them `-text` so git keeps the bytes
exactly as exported.

The experimental design is `../SCORCH DCE Experimental Design Positly.xlsx`.
