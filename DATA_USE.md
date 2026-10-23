# Data Use & Public-Safety Rules

The one dataset used by the starter workflow is:

```text
data/raw/content_refresh_anonymized.csv
```

It is a small, anonymized slice of content-performance data — one row per pseudonymized content item, with observed search/engagement metrics, content metadata, freshness fields, and derived comparison windows.

## Data interpretation

- Rate columns (`ctr`, `engagement_rate`, `scroll_rate`, `ai_traffic_pct`, `trend_pct`) use a 0–100 percentage scale: `ctr = 0.76` means 0.76%, not 76%.
- Hashed `content_id` / `client_id` values are pseudonyms, not features. Use them for grouping, joining, and validation only; never attempt to map them back.
- `avg_position = 0` means no position data, not rank zero.
- The label `is_declining_label` is derived from `trend_direction`, which is computed from `trend_pct`; those fields are never predictors.
- The starter data does not include client names, domains, URLs, page titles, keywords, or raw search queries.

## Rules while working

1. Do not add raw private client data to this repository or a fork. Request an approved release from your mentor instead of exporting additional data.
2. Do not paste private client data into third-party tools or APIs beyond what the approved release allows.
3. Use pseudonymous IDs for grouped splits and joins only, not as model features.
4. Build from observable evidence; do not rely on product decision flags or scores as ground truth.
5. Use careful language in public outputs: observed, measured, directional, and decision-support. Never claim to have predicted Google's algorithm or proved causal refresh impact.
6. Keep row-level queues containing pseudonymous identifiers out of Git. Commit aggregate metrics and report-safe figures only.

## Before publishing

- Confirm no client identifiers, URLs, private queries, credentials, or raw data appear in the repository.
- Confirm no larger dataset or row-level queue was committed.
- Keep claims honest and decision-support framed.

The repository's CI leak guard is part of the public-safety discipline; do not work around it.
