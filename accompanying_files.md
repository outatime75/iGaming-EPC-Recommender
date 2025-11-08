
# ML Demo — Recommender + Propensity

**Files** :

- `affiliates.csv` — 200 synthetic affiliates with geo focus, vertical, traffic source, and quality score.
- `brands.csv` — 50 synthetic brands with vertical, payout type (CPA/RevShare/Hybrid), baseline conversion, FTD value, and allowed GEOs.
- `events.csv` — 180 days of daily aggregates: clicks, registrations, FTDs, NGR by affiliate×brand×geo×device×campaign.

**Notebooks/Code in this chat**:

1) Build **SVD recommender** from `events.csv` (implicit feedback = FTDs + 0.005×NGR).
2) Train **Gradient Boosting classifier** to predict FTD propensity per lead (context features = geo, device, hour, affiliate traits, brand baselines).
3) Blend both into a **contextual ranking** with expected EPC(expected revenue per click) using brand payout type.

**Key functions**:
- `recommend_offers(affiliate_id, geo, device, top_k)` → returns a contextual, compliance-aware ranked list of brands with estimated EPC and FTD probability.

**Suggested KPI for pilot**:
- Hit@K on last-30-days (offline), lift in EPC/FTD rate in A/B test (online), operator acceptance, and compliance match rate.


**Contents of affiliates.csv**

| Column           | Type   | Description                                                            |
| ---------------- | ------ | ---------------------------------------------------------------------- |
| `affiliate_id`   | int    | Unique ID of the affiliate.                                            |
| `geo_focus`      | string | Primary GEO market the affiliate targets (e.g., DE, SE, CA).           |
| `traffic_source` | string | Main channel used (e.g., SEO, PPC, Social, Email, Messenger).          |
| `vertical_focus` | string | Preferred vertical (Casino, Sports, Poker, Bingo).                     |
| `avg_quality`    | float  | Normalized quality score (0–1), representing historic traffic quality. |

**Contents of brands.csv**

| Column          | Type   | Description                                                                    |
| --------------- | ------ | ------------------------------------------------------------------------------ |
| `brand_id`      | int    | Unique ID of the operator/brand.                                               |
| `brand_name`    | string | Brand label (synthetic in demo).                                               |
| `vertical`      | string | Product vertical (Casino, Sports, Poker, Bingo).                               |
| `payout_type`   | string | Deal type: CPA, RevShare, or Hybrid.                                           |
| `baseline_cr`   | float  | Baseline registration→FTD conversion rate.                                     |
| `baseline_ftd`  | float  | Baseline FTDs per 100 registrations (synthetic).                               |
| `avg_ftd_value` | float  | Average net gaming revenue (NGR) per FTD (used for RevShare EPC).              |
| `allowed_geos`  | string | List of GEOs where this brand allows traffic (compliance filter).              |
| `cpa_eur`       | float  | Payout per FTD if CPA is active (synthetic; added in notebook).                |
| `revshare_pct`  | float  | Revenue share percentage if RevShare is active (synthetic; added in notebook). |

**Contents of events.csv**

| Column          | Type   | Description                                     |
| --------------- | ------ | ----------------------------------------------- |
| `date`          | date   | Calendar day of the record.                     |
| `affiliate_id`  | int    | Affiliate ID (foreign key to `affiliates.csv`). |
| `brand_id`      | int    | Brand ID (foreign key to `brands.csv`).         |
| `geo`           | string | GEO market of the traffic (DE, SE, NO, etc.).   |
| `device`        | string | Device type (desktop, android, ios).            |
| `campaign_id`   | int    | Identifier for the campaign/creative.           |
| `clicks`        | int    | Number of clicks recorded.                      |
| `registrations` | int    | Number of player registrations.                 |
| `ftds`          | int    | Number of first-time depositors.                |
| `ngr`           | float  | Net Gaming Revenue (synthetic), in euros.       |
