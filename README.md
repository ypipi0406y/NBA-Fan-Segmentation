# NBA Fan Segmentation & Season Ticket Renewal Prediction

##  Live Dashboard
[View on Tableau Public](https://public.tableau.com/app/profile/yuning.yang/viz/Book1_17734682027090/Dashboard1)

---

## Project Overview
Built an end-to-end fan analytics pipeline using Python, Tableau, and Microsoft Dynamics 365 to segment NBA teams into behavioral cohorts and predict season ticket renewal probability enabling data-driven CRM campaign strategies for sports organizations.

This project simulates the type of fan analytics work done by CRM and business strategy teams at NBA franchises, directly applicable to roles in sports analytics, fan engagement, and CRM operations.

---

## Key Assumptions & Research Framework

Since individual-level fan purchase data is not publicly available, this project uses **team performance metrics as a proxy for fan behavior**  a standard methodology in sports business research.

The core premise is:
> **Fan loyalty and season ticket renewal intent is strongly correlated with team performance quality, consistency, and trajectory.**

Specifically:
- **Core Fans** are defined as fans of teams with consistently high win rates AND high scoring output — both winning and entertaining play drive deep loyalty
- **Renewal** is modeled as: if a team's win rate does not decline the following season, fans are assumed to renew (1), otherwise lapsed (0)
- **Revenue estimates** are simulations based on assumed inputs: $150 average ticket price × 41 home games × estimated attendance rate per segment
- **CRM strategies** are designed frameworks simulated in Microsoft Dynamics 365 — not live campaign data

These assumptions are clearly scoped to team-level analysis and documented throughout the notebook.

---

## Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | Data collection, cleaning, feature engineering |
| Scikit-learn | K-Means clustering, Random Forest, Logistic Regression |
| nba_api | Real-time NBA game log data retrieval |
| Kaggle Datasets | Historical team stats and summaries |
| Tableau Desktop | Interactive dashboard and data visualization |
| Microsoft Dynamics 365 | CRM campaign framework design & workflow simulation |

---

## Data Sources
- **NBA Game Logs** — via `nba_api` (2015–2022 regular seasons, 30 teams)
- **NBA Team Summaries** — Kaggle: `sumitrodatta/nba-aba-baa-stats`
- **NBA Games Dataset** — Kaggle: `nathanlauga/nba-games`

---

## Methodology

### Module 1 — Data Collection & Cleaning
- Retrieved 8 seasons of game logs via `nba_api` (19,038 records)
- Merged team-level stats with historical summaries
- Engineered features: win rate, win rate trend, playoff status, scoring tier
- Built master dataset: 240 rows (30 teams × 8 seasons)

### Module 2 — Fan Segmentation (K-Means Clustering)
- Applied K-Means clustering (K=4) on 6 performance features
- Validated optimal K using Elbow Method and Silhouette Score
- **Segmentation uses team performance as a proxy for fan engagement level**
- Core Fans defined by teams with high win rate AND high avg scoring — reflecting that fans respond to both winning and entertaining basketball

| Segment | Win Rate Range | Description |
|---------|---------------|-------------|
| Core Fans | 60%+ | Consistent winners with high scoring — highest loyalty |
| Engaged Fans | 50–60% | Competitive teams, strong growth potential |
| Casual Fans | 40–50% | Mid-tier teams, attendance-sensitive to performance |
| Lapsed Fans | <40% | Struggling teams, high churn risk |

### Module 3 — Season Ticket Renewal Prediction
- Built and compared 3 models: Logistic Regression, Random Forest, Gradient Boosting
- **Best model: Random Forest (AUC = 0.681)**
- Renewal label: next season win rate ≥ current season win rate → renewed (1), else lapsed (0)
- Top predictors:
  1. `avg_plus_minus` — net scoring margin (most important)
  2. `win_rate` — season win percentage
  3. `win_rate_trend` — year-over-year improvement
- Generated renewal probability score (0–100) for each team-season

### Module 4 — CRM Strategy Framework (Dynamics 365 Simulation)
Designed targeted campaign strategies per segment, simulated as Dynamics 365 contact segments and campaign workflows:

| Segment | CRM Action | Channel |
|---------|-----------|---------|
| Core Fans | Retention: Early Bird Renewal Offer | VIP Email + Personal Call |
| Engaged Fans | Upsell: Premium Package Upgrade | Email + Push Notification |
| Casual Fans | Win-back: Loyalty Incentive Campaign | Social Media + SMS |
| Lapsed Fans | Re-engagement: New Fan Intro Package | Retargeting Ad + Email |

> Note: CRM workflows are simulated frameworks designed to reflect real Dynamics 365 campaign logic. Revenue figures are model estimates based on assumed ticket pricing inputs.

---

## Key Findings
- **Top renewal predictor is net scoring margin** (`avg_plus_minus`) — fans respond to dominance and entertainment quality, not just win/loss record
- **Win rate trend matters more than absolute win rate** — an improving team retains fans better than a declining one, even at higher win rates
- **Simulated revenue opportunity**: Lapsed Fan → Core Fan conversion = estimated **+$4,238 revenue per fan annually** (simulation based on $150 avg ticket × 41 home games × assumed attendance rates)
- Core Fan segment shows 60%+ win rate with low variance across all 8 seasons, confirming segment stability

---

## Dashboard Features
- **Fan Segments** — Scatter plot: Win Rate vs Avg Points, colored by segment, sized by renewal score
- **Renewal Ranking** — All 30 teams ranked by renewal probability score
- **Win Rate Trend** — Team trajectories across 8 seasons by fan segment
- **CRM Action Plan** — Campaign strategy table per team
- **Interactive** — Season filter + click-to-filter by segment across all charts

---

## Repository Structure
```
├── NBA_Fan_Segmentation.ipynb         # Full analysis notebook (Google Colab)
├── README.md                          # Project documentation
├── data/
│   ├── tableau_fan_segmentation.csv   # Cleaned master dataset
│   └── crm_action_plan.csv            # CRM strategy output
```

---

## About
**Yuning Yang** | MS Business Analytics, Pepperdine University
Champion, 2026 MIT Sloan Sports Analytics Conference Hackathon
[LinkedIn](https://linkedin.com/in/yuning-y-a0b766206)
