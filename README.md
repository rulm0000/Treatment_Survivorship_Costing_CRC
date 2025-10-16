# Treatment & Survivorship Cost Replication

CRC treatment cost analysis pipeline.

## How to Run

**Requirements:** Python with `pandas`, `numpy`, `xlsxwriter`

1. Extract `5.2 T_S_replication.zip`
2. Navigate to the extracted folder
3. Run these commands:
   ```bash
   python 01_scripts/estimate_costs.py
   python 01_scripts/build_yearly_cost_table.py
   ```

**Output:** Final results in `02_outputs/US_Estimated_Costs_Calculated_V2.csv`

## What It Does

Takes cancer cost data and calculates weighted averages by age group, race, sex, and stage.
