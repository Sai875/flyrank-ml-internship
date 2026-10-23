---
name: flyrank-data
description: FlyRank internship datasets, gotchas, panel warnings, access, and iteration rules. Load for every task that touches the data.
---

# FlyRank internship data

Two datasets are used in this track: the 30k-row starter CSV and the gated ~79M-row warehouse release.

## 1. Starter dataset

`data/raw/content_refresh_anonymized.csv` — 30,000 rows × 44 columns, one row per pseudonymized content item, 32 clients, trailing-90-day metrics. See `docs/data-dictionary.md`.

- **Rate columns are 0–100 percentages:** `ctr = 0.76` means 0.76%, not 76%. This applies to ctr, engagement_rate, scroll_rate, ai_traffic_pct, and trend_pct.
- **`avg_position = 0` means no data**, not rank zero.
- **`scroll_rate` and `ai_traffic_pct` can exceed 100** because numerator and denominator can come from different measurement systems.
- **Label trap:** `is_declining_label` is derived from `trend_direction`, which is computed from `trend_pct`. Never use `trend_direction` or `trend_pct` as features.
- **Missingness follows content_type:** avoid blind `fillna(0)`; use explicit missingness indicators where appropriate.
- **IDs are pseudonyms:** `content_id` and `client_id` are for grouping/joining/splitting only, never predictors.

## 2. Warehouse release

`hf://datasets/FlyRank/internship-warehouse` — build v20260703.

| Table | Rows | Grain |
|---|---:|---|
| `dim_clients` | 104 | one per pseudonymized client |
| `dim_content` | 519,606 | one per content item |
| `fact_content_daily_performance` | 78,835,655 | report_date × client × content |
| `fact_content_daily_performance_sample` | ~11.7M | final month (June 2026) only |
| `fact_content_query_90d` | 2,414,248 | client × content × query hash |

The warehouse spans 2025-01-27 to 2026-06-30. Position column: `gsc_avg_position`.

## Panel warnings

- History depth differs by client; inspect `dim_clients.gsc_data_start` and prefer per-client windows.
- Before a client's `ga4_data_start`, GA4 columns may be zero-filled while `ga4_data_available = FALSE`; those zeros are not true zero engagement.
- Some clients have little or no usable search/analytics history; expect to filter.
- Query-table per-content context columns repeat across rows: use `ANY_VALUE()`, never `SUM()`.
- The query table's 90-day window overlaps the snapshot's final months; align feature windows with the label window.

## Access and iteration rules

Request gated access and use a READ token through Colab Secrets (`HF_TOKEN`) or an environment variable; never paste tokens into notebook code. Iterate on a mid-panel month (for example, March 2026), not the final-month sample, when developing label logic. Treat the final month as a sealed test window. Run a full warehouse scan only once the query is final and cache approved outputs under `work/outputs/`.

## Verification

- Start with row count and min/max report date.
- Probe the intended grain for duplicates before aggregating.
- If a metric looks absurd, re-check rate scaling, missingness, grain, and window alignment.
