# 5.2 Treatment & Survivorship Cost Replication

This folder is a self-contained copy of the files that were used to derive the
annual CRC treatment-and-survivorship cost inputs.  It walks from the original
extracted data (US & Canadian studies) to the cleaned yearly costs that were
fed into the Phase 4 costing pipeline.

## Directory layout

- `00_raw/` &mdash; original source spreadsheets that were copied from the
  working directory (`Treatemant Survivorship cost.xlsx`, the Canadian/US
  extraction, plus the helper workbooks that document the inputs).
- `01_scripts/` &mdash; copies of the Python scripts that process the raw data.
  They can be run directly from inside this replication folder so the original
  code never needs to be touched.
    - `estimate_costs.py` (from *Treatment Survivorship Costing*) rebuilds the
      US Study sheet with the <65 age-band estimates that use Canadian ratios.
    - `calculate_costs_from_csv.py` / `calculate_costs_final_v3.py` are kept for
      reference; they were later iterations that apply simulation weights to
      generate all-age subgroup costs.
    - `build_yearly_cost_table.py` (new helper) reads the exported CSV and the
      Phase 4 current-age groupmeans to add the weighted `Under65` and `65plus`
      rows while converting all currency fields to numeric values.
- `02_outputs/` &mdash; stepwise results.  Each artefact is a direct copy of
  what the original pipeline produced, plus the rebuilt final CSV.
    - `US_Estimated_Costs.xlsx` (output of `estimate_costs.py`).
    - `US_Estimated_Costs_CSV.csv` (Excel sheet exported to CSV).
    - `US_Estimated_Costs_Calculated_V2.csv` (clean numeric table with 5-year
      age bands, race, sex, CRC stage, and the added Under65/65plus rows).
    - `US_Estimated_Costs_Calculated_V2.xlsx` (archival copy of the workbook).
- `03_support/` &mdash; supporting data copied from the Phase 4 run that are
  needed for weighting (`phase4_groupmeans_currage_full.csv`).

## Re-running the pipeline

1. From `01_scripts/`, run `estimate_costs.py` (requires `pandas` and
   `xlsxwriter`).  It reads the raw Excel file in `00_raw/` and reproduces
   `02_outputs/US_Estimated_Costs.xlsx`.
2. Export the “US Study Estimated Costs” sheet to CSV (already copied here as
   `US_Estimated_Costs_CSV.csv`).
3. Run `build_yearly_cost_table.py` (standard library only).  It consumes the
   CSV plus the current-age groupmeans weights to regenerate
   `US_Estimated_Costs_Calculated_V2.csv`, appending the Under65 and 65plus
   weighted averages.

No files are modified outside of this replication folder, so the original
analysis assets remain untouched.  The resulting CSV delivers the yearly phase
costs by 5-year age bands, race, sex, CRC stage, and the aggregate Under65 /
65plus groupings ready for downstream use.
