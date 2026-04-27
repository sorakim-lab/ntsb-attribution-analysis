# Data

This folder contains the output of Phase B analysis.

## Source

The primary data (`avall.mdb`, ~546 MB) is the NTSB Aviation Accident Database, available from:
https://www.ntsb.gov/Pages/AviationDownloadDataFiles.aspx

The database itself is not redistributed here. To reproduce, download `avall.zip` from NTSB and place `avall.mdb` on your local Desktop, then run the notebooks in order.

## Files in this folder

- **phase_b_actors_v2.csv** — Per-statement actor extraction. Columns: `ev_id`, `narr_cause`, `actor_v2`, `actor_category`. n = 23,742.
- **phase_b_temporal.csv** — Actor category distribution by 5-year bucket.
- **phase_b_severity.csv** — Actor category distribution by accident injury severity (NONE / MINR / SERS / FATL).

## License

Data outputs in this folder are derived from publicly available NTSB records and are released under the same MIT license as the rest of this repository.
