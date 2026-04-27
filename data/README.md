# Data

This folder contains the output of Phase B analysis.

## Source

The primary data (`avall.mdb`, ~546 MB) is the NTSB Aviation Accident Database, available from:
https://www.ntsb.gov/Pages/AviationDownloadDataFiles.aspx

The database itself is not redistributed here. To reproduce, download `avall.zip` from NTSB and place `avall.mdb` on your local Desktop, then run the notebooks in order.

## Files in this folder

- **phase_b_actors_v2.csv** — Per-statement actor extraction. Columns: `ev_id`, `narr_cause`, `actor_v2`, `actor_category`. n = 23,742 (statements with > 50 characters of narrative text).
- **phase_b_temporal.csv** — Actor category distribution by 5-year bucket. Five buckets total: 2005, 2010, 2015, 2020 (each covering 5 full years), and 2025 (single calendar year, n = 617). All five buckets are reported in the project README; the 2025 bucket is identified as a single-year sample wherever it appears.
- **phase_b_severity.csv** — Actor category distribution by accident injury severity (NONE / MINR / SERS / FATL). Restricted to 2008–2024 to align with the clean window for severity coding.
- **phase_b_validation_sample.csv** — Random sample of n = 100 statements (`random_state=42`) drawn from `phase_b_actors_v2.csv`, manually annotated for extraction correctness. The `correct?` column records the per-statement annotation that supports the ~91% accuracy estimate reported in the project README.

## License

Data outputs in this folder are derived from publicly available NTSB records and are released under the same MIT license as the rest of this repository.
