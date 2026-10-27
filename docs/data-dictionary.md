# Data dictionary and schema notes

This guide documents fields confirmed in the repository's W03 notebook and the March 2026 warehouse sample. The live warehouse schema is authoritative: inspect it before relying on additional fields, because upstream schemas can change.

## Source and scope

- **Warehouse:** [FlyRank/internship-warehouse](https://huggingface.co/datasets/FlyRank/internship-warehouse) (gated).
- **Daily fact table:** `fact_content_daily_performance`.
- **Dimensions:** `dim_content` and `dim_clients`.
- **Development partition used by W03:** `month=2026-03`.
- **Sealed period:** June 2026 `_sample` partition; do not use it while developing the target definition.

## Confirmed fact-table fields

| Field | Meaning / safe interpretation |
|---|---|
| `report_date` | Date of the daily observation. |
| `client_hash_id` | Pseudonymous client grouping key; use for joins and grouped validation, never as a predictive feature. |
| `content_hash_id` | Pseudonymous content grouping key; use for joins and grouped validation, never as a predictive feature. |
| `month` | Month partition label. |
| `client_has_gsc`, `client_has_ga4` | Client-level source availability indicators. |
| `gsc_data_available`, `ga4_data_available` | Availability flags for the corresponding source. Treat only explicit `TRUE` as available; `FALSE` and unknown/null are not evidence of availability. |
| `gsc_clicks` | Observed Google Search Console clicks for the content-day. |
| `gsc_impressions` | Observed GSC impressions for the content-day. |
| `gsc_sum_position` | Position accumulator used with impressions to derive a weighted position where the denominator and value are valid. A raw zero is not a rank of zero; treat it as missing/no valid position. |
| `sessions_ai` | Observed AI-referred sessions field; interpret only when its source availability and null semantics are understood. |
| `ai_chatgpt`, `ai_perplexity`, `ai_gemini`, `ai_copilot`, `ai_claude`, `ai_meta`, `ai_other` | Source-specific AI referral fields visible in the sampled schema. Check their availability flags before interpreting null or zero values. |
| `scroll_events` | Observed scroll-event field; confirm its null/availability semantics before using it. |

## Schema verification in DuckDB

Run this only after you have accepted the warehouse's access terms and configured `HF_TOKEN` in Colab Secrets. Never paste the token into a notebook cell.

```python
con.sql(f"DESCRIBE SELECT * FROM {FACT}").df()
con.sql(f"SELECT * FROM {FACT} LIMIT 5").df()
```

Before building a query, verify column spelling and types from the live schema. In particular, the fact table uses `gsc_sum_position`; do not assume that a field named `gsc_avg_position` exists.

## Modeling and privacy rules

- One fact row is intended to represent a content item on a reporting date; W03 checks uniqueness of `(client_hash_id, content_hash_id, report_date)`.
- Keep pseudonymous IDs for grouping, joining, and holdout splits only.
- Use only features that would be available at the decision date.
- Do not use future-window values, target fields, or label-derived fields as predictive inputs.
- Do not infer source availability from numeric zeros.
- Never commit the raw warehouse, row-level action queues, client-level records, credentials, or tokens. Commit aggregate metrics and report-safe figures only.
