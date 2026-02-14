## Part 5 – Reflection

### 1. What assumptions in my solution are weakest?

**a) `is_won` is clean and binary (0/1)**
I assumed the win flag is perfectly labeled and consistent across time. In reality:

* Definitions of “won” may change.
* Some deals may be reopened, split, or partially closed.
* Data entry inconsistencies may exist.

If labeling logic changed historically, trend-based insights (win rate, velocity) could be misleading.

**b) Revenue equals realized value**
I treated `deal_amount` as actual revenue. In production:

* Deals may churn early.
* Revenue may be recognized over time.
* Discounts, refunds, and upsells may not be reflected.

This weakens revenue-based conclusions and ROI calculations.

**c) Time grouping (closed_year_and_quarter) is correct and stable**
I assumed:

* Close date is reliable.
* No timezone or backfilling issues.
* Historical deals were not batch-updated.

In reality, pipeline reporting often suffers from delayed CRM updates.

**d) All deals are comparable**
I treated all deals equally regardless of:

* Segment
* Sales rep
* Geography
* Channel
* Product mix

This simplifies analysis but hides structural drivers.

---

### 2. What would break in real-world production?

**1. Data Quality Drift**

* Null values in `deal_amount`
* Unexpected values in `is_won`
* Missing close dates
* Duplicated `deal_id`

Without validation checks, dashboards would silently produce wrong KPIs.

**2. Changing Business Logic**

* New pricing models
* Multi-product deals
* Subscription vs one-time revenue
* New CRM fields

Hard-coded aggregations would become outdated quickly.

**3. Scale & Performance**
If this runs on:

* Millions of deals
* Live BI dashboards

Groupby operations and recalculations could become slow without:

* Materialized tables
* Incremental aggregation
* Precomputed metrics

**4. Survivorship Bias**
If we only analyze closed deals:

* We miss pipeline risk
* We ignore time-to-close skew
* We lose forward-looking signals

That limits predictive value.

---

### 3. What would I build next if given 1 month?

If given 1 month, I would shift from descriptive EDA → decision-enabling system.

#### 1️⃣ Build a Deal Quality Scoring Model

* Predict probability of win at deal creation.
* Identify high-risk deals early.
* Help sales prioritize.

Impact: Improves win rate and sales efficiency.

---

#### 2️⃣ Build Cohort & Retention Revenue Analysis

* Cohort by quarter won.
* Track revenue expansion or contraction.
* Measure LTV instead of just deal value.

Impact: Aligns sales incentives with long-term revenue.

---

#### 3️⃣ Pipeline Health Dashboard

Add:

* Stage conversion rates
* Average time per stage
* Deal aging risk
* Forecast confidence bands

Impact: Moves leadership from reactive to proactive.

---

#### 4️⃣ Data Validation Layer

* Schema validation
* Null monitoring
* Metric sanity checks
* Automated anomaly detection

Impact: Production reliability.

---

### 4. What part of my solution am I least confident about?

**Custom Metrics Interpretation**

While the invented metrics (e.g., revenue efficiency, momentum indicators) are analytically valid, I am least confident about:

* Whether they align with how the business actually sells.
* Whether leadership would find them intuitive.
* Whether they correlate with real strategic outcomes.

Without:

* Sales interviews
* Product context
* Pricing model understanding

There is risk of optimizing the wrong KPI.

---

## Final Reflection

Technically, the EDA is solid.
Strategically, it is only a starting point.

The biggest risk is not code correctness —
it is **business misalignment**.

In real-world data science:

* The math is rarely the hardest part.
* The modeling is rarely the failure point.
* The weak link is usually assumptions about how the business truly works.

If this were a production system, my priority would shift from deeper analysis to:

* Data reliability
* Metric governance
* Business alignment
* Forward-looking modeling

That is where real leverage exists.
