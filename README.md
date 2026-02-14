# SkyGeni Sales Analytics Platform

## Overview

This project provides a comprehensive sales analytics solution designed to help Chief Revenue Officers (CROs) and sales leadership identify win rate drivers, detect performance trends, and optimize sales execution. The analysis focuses on understanding which deal attributes and sales behaviors are statistically associated with win probability.

## Problem Statement

The CRO observes declining win rate despite stable pipeline volume. This project aims to:
- Identify which deal attributes (segment, region, ACV, cycle time, etc.) are associated with win probability
- Detect which factors contributed to win rate decline in recent quarters
- Provide actionable insights for sales team optimization

## Project Structure

```
SkyGeni/
├── data/                           # Sales data files
├── EDA.ipynb                       # Exploratory Data Analysis
├── Win Rate Driver Analysis.ipynb  # Statistical analysis of win rate drivers
├── Reflections.md                  # Critical analysis and future improvements
├── Mini_System_Design_Sales_Insight_Alert_System.docx  # System design document
└── README.md                       # This file
```

## Key Features

### 1. Exploratory Data Analysis (EDA.ipynb)
- **Time-based analysis**: Quarterly win rate trends, revenue metrics, and deal volume
- **Segment analysis**: Performance breakdown by region, industry, product type, and lead source
- **Deal characteristics**: ACV distribution, sales cycle analysis, and conversion patterns
- **Feature engineering**: Created time buckets, ACV segments, and binary outcome variables

**Key Findings:**
- Win rate declined from ~45% (baseline) to ~44% in recent quarters
- APAC region showed the largest negative weighted impact (-10.88)
- EdTech industry experienced the most significant win rate drop (-6.95 weighted impact)
- Deals with sales cycles \u003c2 weeks showed concerning performance trends

### 2. Win Rate Driver Analysis (Win Rate Driver Analysis.ipynb)
- **Structural change detection**: Identifies segments responsible for win rate decline
- **Weighted impact analysis**: Quantifies contribution of each segment to overall performance
- **Statistical significance testing**: Chi-square tests to validate findings
- **Predictive modeling**: Logistic regression for win probability (55% accuracy)

**Methodology:**
```python
weighted_impact = win_rate_delta × deals_decline_period
```
This isolates which segments are responsible for win rate drops and quantifies their impact.

**Key Insights:**
- North America showed positive momentum (+16.19 weighted impact)
- HealthTech industry demonstrated improvement (+5.56 weighted impact)
- Revenue impact analysis revealed significant losses in APAC (-$11.4M) and North America (-$12.8M)

### 3. Critical Reflections (Reflections.md)

**Weakest Assumptions:**
1. **Data Quality**: Assumes CRM data is clean, consistent, and historically stable
2. **Revenue Representation**: Treats deal_amount as realized revenue (may not account for churn)
3. **Deal Comparability**: Assumes all deals progress linearly through stages
4. **Model Performance**: Logistic regression achieved only 55% accuracy (marginal improvement over baseline)

**Production Risks:**
- Data quality drift (nulls, schema changes, duplicates)
- Changing business logic (new pricing models, product bundles)
- Alert fatigue from AI-generated recommendations
- Scale and performance issues with large datasets
- Survivorship bias (focusing only on closed deals)

**Next Steps (1-Month Roadmap):**
1. Deal health \u0026 win probability scoring
2. Closed-lost intelligence \u0026 pattern clustering
3. Cohort \u0026 retention revenue analysis
4. Pipeline health dashboard
5. Data validation \u0026 monitoring layer
6. Controlled alerting \u0026 feedback loop

## How to Run the Project

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
```

### Running the Analysis

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/SkyGeni.git
cd SkyGeni
```

2. **Launch Jupyter Notebook:**
```bash
jupyter notebook
```

3. **Run notebooks in order:**
   - Start with `EDA.ipynb` for exploratory analysis
   - Then run `Win Rate Driver Analysis.ipynb` for statistical insights
   - Review `Reflections.md` for critical analysis

### Data Requirements

The analysis expects a CSV file with the following columns:
- `deal_id`: Unique deal identifier
- `created_date`: Deal creation date
- `closed_date`: Deal close date
- `sales_rep_id`: Sales representative identifier
- `industry`: Customer industry (SaaS, EdTech, FinTech, HealthTech, Ecommerce)
- `region`: Geographic region (North America, Europe, APAC, India)
- `product_type`: Product tier (Core, Pro, Enterprise)
- `lead_source`: Lead origin (Inbound, Outbound, Partner, Referral)
- `deal_stage`: Current deal stage
- `deal_amount`: Deal value in USD
- `sales_cycle_days`: Days from creation to close
- `outcome`: Win/Lost status

## Key Decisions

### 1. Feature Engineering
- **Time buckets**: Segmented sales cycles into meaningful ranges (\u003c2w, 2-4w, 1-2m, 2-3m, 3m+)
- **ACV quartiles**: Used quantile-based bucketing to handle right-skewed revenue distribution
- **Period comparison**: Defined baseline vs. decline periods using last 2 quarters as decline window

### 2. Statistical Approach
- **Chi-square tests**: Validated statistical significance of win rate changes
- **Weighted impact**: Volume-adjusted metrics to prioritize high-impact segments
- **Logistic regression**: Simple, interpretable model for win probability (trade-off: lower accuracy)

### 3. Analysis Focus
- Prioritized actionable insights over model complexity
- Emphasized segment-level analysis for targeted interventions
- Balanced statistical rigor with business interpretability

## Limitations

1. **Model Accuracy**: 55% accuracy indicates weak predictive power
   - Requires additional features (engagement depth, buyer intent, competitive context)
   - May benefit from tree-based models or neural networks

2. **Data Assumptions**: 
   - Assumes clean, consistent CRM data
   - Does not account for reopened deals or label changes
   - Revenue may not reflect realized value (churn, discounts)

3. **Causal Inference**:
   - Analysis identifies correlations, not causation
   - Requires sales interviews and business context for validation

## Future Improvements

### Short-term (1-3 months)
- Improve model accuracy with additional features
- Implement data validation pipeline
- Add pipeline health metrics (forward-looking)
- Build closed-lost pattern clustering

### Long-term (3-6 months)
- Cohort-based revenue analysis
- Real-time alerting system
- AI-driven coaching recommendations
- Automated anomaly detection

## Technical Stack

- **Python 3.x**
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Matplotlib/Seaborn**: Data visualization
- **SciPy**: Statistical testing
- **Scikit-learn**: Machine learning (logistic regression)
- **Jupyter**: Interactive notebooks

## Contributing

This is an analytical project. If you'd like to extend the analysis:
1. Fork the repository
2. Create a feature branch
3. Add your analysis/improvements
4. Submit a pull request with clear documentation

## License

[Specify your license here]

## Contact

For questions or collaboration opportunities, please reach out via [your contact method].

---

**Note**: This project demonstrates analytical thinking, statistical rigor, and business acumen in sales analytics. The focus is on actionable insights rather than model complexity, reflecting real-world CRO priorities.
