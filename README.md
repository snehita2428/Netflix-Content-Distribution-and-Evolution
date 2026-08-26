# Streaming Success: A Data-Driven Analysis of Netflix Content Distribution and Evolution

An end-to-end data analytics project examining how Netflix's content library has evolved across
geographies, genres, and formats — combining Python, R, SQL, NLP, and AWS cloud services.

> Course project — AIT-580, Department of Applied Information Technology, George Mason University
> Author: **Snehita Vattamwar** · Instructors: Prof. Dr. Harry Foxwell, Prof. Raymond P. Smith

---

## Overview

Netflix's shift from DVD rentals to global streaming reshaped how audiences consume media. This
project analyzes a 40-year catalog of Netflix titles to answer three questions:

1. **Geographic evolution** — How has content distribution across countries changed over time?
2. **Content similarity** — What thematic clusters emerge from text attributes (genres, cast, descriptions)?
3. **Format strategy** — Is Netflix shifting emphasis from movies toward TV series?

## Dataset

| | |
|---|---|
| Source | [Netflix-assignment1 — data.world/vpasupu](https://data.world/vpasupu/netflix-assignment1) |
| Records | 7,788 titles (≈8,790 rows post-processing) |
| Coverage | 1980–2020 |
| Attributes | `show_id`, `type`, `title`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `listed_in`, `description` |

Includes all four measurement levels (nominal, ordinal, interval, ratio), enabling both qualitative
and quantitative analysis.

## Tech Stack

**Python** — pandas, numpy, scikit-learn (`TfidfVectorizer`, `CountVectorizer`), spaCy, NLTK (VADER), matplotlib, seaborn
**R** — RStudio, ggplot2, tm, proxy
**AWS** — S3 (storage), Glue DataBrew (profiling & prep), RDS/MySQL (SQL queries), QuickSight (dashboards)

## Methodology

| Step | Description |
|---|---|
| **A. Data preparation** | Loaded via pandas; imputed missing `director` values as `Unknown`, dropped remaining nulls, cast `date_added`/`release_year` to datetime, engineered `month_added` and `day_added` |
| **B. Cloud profiling** | Uploaded cleaned CSV to an S3 bucket; profiled cardinality, outliers, and completeness in AWS Glue DataBrew |
| **C. Text analysis** | TF-IDF vectorization + cosine similarity on `listed_in` (500-record sample); spaCy named-entity recognition; VADER sentiment scoring on descriptions |
| **D. EDA & visualization** | Distribution plots, correlation heatmaps, boxplots, choropleth world map, and time-series comparisons in R and Python |
| **E. SQL analysis** | Loaded the dataset into MySQL on AWS RDS and queried long-running series, monthly additions, and format breakdowns |

## Key Findings

- **U.S. dominance, but diversifying** — 35% of titles (852 records) originate in the United States; India is second at 11% (294 records). Growth in India, Brazil, and South Korea signals a deliberate regional-content strategy.
- **Movies still outnumber series** — roughly 6,000+ movies vs. ~2,400 TV shows overall, but movie releases peaked around 2018 and declined sharply while TV series rose steadily.
- **Mature-audience skew** — `TV-MA` is the most common rating, followed by `TV-14` and `TV-PG`; `G` and `NC-17` are rarest.
- **~100-minute norm** — movie durations form a near-symmetric bell curve centered around 100 minutes.
- **Even release cadence** — content additions are balanced across seasons (~1,400–1,600 per season); August saw the most additions (769), February the fewest (562).
- **Distinct content niches** — the cosine similarity matrix is predominantly low-similarity with isolated high-similarity clusters, consistent with targeted genre grouping for recommendations.
- **Neutral-to-negative tone** — VADER scoring on descriptions returns largely neutral sentiment with a mild negative lean (sample compound score: −0.296).

## Repository Structure

```
.
├── data/                 # Raw and cleaned datasets
├── notebooks/            # Jupyter notebooks (cleaning, TF-IDF, NLP, EDA)
├── r/                    # R scripts for summary statistics and ggplot2 visuals
├── sql/                  # DDL and analytical queries for AWS RDS
├── figures/              # Exported charts and dashboard screenshots
├── docs/                 # Final paper (PDF)
└── README.md
```

## Getting Started

```bash
git clone https://github.com/<your-username>/netflix-content-analysis.git
cd netflix-content-analysis

pip install pandas numpy scikit-learn spacy nltk matplotlib seaborn
python -m spacy download en_core_web_sm
python -c "import nltk; nltk.download('vader_lexicon')"

jupyter notebook notebooks/
```

For the AWS components, configure your own S3 bucket and RDS instance and update the connection
settings before running the SQL scripts.

## Limitations

The dataset may under-represent regional catalogs due to licensing and access differences. Text
analysis relies on a bounded set of algorithms that can miss finer linguistic nuance, and the study
focuses on aggregate trends rather than demographic segmentation.

## Future Work

Regional preference modeling against subscriber growth and retention; predictive modeling of content
success from pre-release attributes; analysis of original-programming investment against financial
and brand outcomes; sustainability impact of streaming infrastructure.

## References

Selected sources — see the full paper in `docs/` for the complete list.

- Adhikari et al., "Measurement Study of Netflix, Hulu, and a Tale of Three CDNs," *IEEE/ACM Transactions on Networking*, 2015.
- Lotz, Eklund & Soroka, "Netflix, library analysis, and globalization," *Journal of Communication*, 2022.
- Kamarudin, Daheche & Khmag, "Netflix User and Movies Interest Analysis for Asian Countries," ICEEE, 2022.
- Devashree et al., "Analysis and Visualization of Netflix Shows," AIST, 2022.
- Starosta & Izydorczyk, "Understanding the Phenomenon of Binge-Watching," *IJERPH*, 2020.

---

*Academic project. Netflix is a trademark of Netflix, Inc.; this work is independent and unaffiliated.*
