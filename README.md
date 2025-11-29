# Digital-Marketing-Campaign
This project demonstrates a comprehensive SQL workflow to clean, enrich, and analyze a raw digital marketing dataset. The goal is to transform messy, incomplete data into clear, actionable Key Performance Indicators (KPIs) like Revenue, ROAS (Return on Ad Spend), and CPA (Cost per Acquisition) to support strategic decision-making.


## 🔹 Steps Implemented

### 1. **Data Cleaning**
- Fixed inconsistent values in `company_size`:
  - `"Nov-50"` → `"11-50"`
  - `"10-Jan"` → `"1-10"`

### 2. **Derived Metrics**

- **Total Conversions**  
  Formula:  Total Conversions = Engagement Metric × Conversion Rate
- Added as a new column (`total_conversions`).
- Rounded to 2 decimal places.

- **Revenue**  
Since raw revenue was missing, applied **Average Conversion Value (ACV)** assumptions by industry:  
- Finance / Healthcare → 150  
- Technology / Services → 80  
- E-commerce / Retail → 30  
- Default (Manufacturing, etc.) → 50  
  Formula:  Revenue = Total Conversions × ACV
- Added as a new column (`revenue`).

- **ROAS (Return on Ad Spend)**  
  Formula:  ROAS = Revenue ÷ Ad Spend
- Division-by-zero handled: if `ad_spend = 0`, ROAS = 0.  
- Added as a new column (`ROAS`).

- **CPA (Cost per Acquisition)**  
  Formula:  CPA = Ad Spend ÷ Total Conversions
- Division-by-zero handled: if `total_conversions = 0`, CPA = 99999 (penalty marker).  
- Added as a new column (`CPA`).

---

## 🔹 Strategic Analysis Queries

1. **Audience ROI**  
 - Grouped by `target_audience`.  
 - Calculated **weighted ROAS**:  
   ```
   Weighted ROAS = SUM(Revenue) ÷ SUM(Ad Spend)
   ```
 - Identifies which audience segments deliver the highest ROI.

2. **Channel Profitability**  
 - Grouped by `marketing_channel`.  
 - Metrics:  
   - Total Spend  
   - Total Revenue  
   - Weighted ROAS  
   - Average CPA  
 - Helps allocate budget to the most profitable channels.

3. **Campaign Performance (Top vs Bottom)**  
 - Ranked campaigns by ROAS.  
 - Selected **Top 5** and **Bottom 5** campaigns.  
 - Bottom campaigns filtered to exclude `ad_spend = 0`.

---

## 🔹 Key Learnings
- **Weighted ROAS** is more accurate than simple averages because it accounts for spend size.  
- **Penalty CPA values** isolate non-performing campaigns for immediate budget cuts.  
- Using **ACV assumptions** allows realistic revenue modeling when raw data is incomplete.  
- This workflow demonstrates **data cleaning → enrichment → analysis → strategic insights** in SQL.

---

## 🔹 Business Impact

This SQL workflow is designed to bridge the gap between **raw marketing data** and **strategic decision-making**. By cleaning, enriching, and analyzing the dataset, the project enables marketing teams to:

- **Optimize Budget Allocation**  
- Weighted ROAS highlights which audience segments and channels deliver the highest return.  
- Teams can reallocate spend toward high-performing segments and cut waste from underperformers.

- **Identify Winning Campaigns**  
- Top campaigns (ranked by ROAS) can be replicated or scaled.  
- Bottom campaigns are flagged for review or termination, ensuring resources aren’t wasted.

- **Improve Cost Efficiency**  
- CPA analysis isolates campaigns with prohibitively high acquisition costs.  
- Penalty values (99999) act as red flags for immediate corrective action.

- **Strategic Forecasting**  
- Revenue proxies (via ACV assumptions) allow realistic financial modeling even when raw revenue data is missing.  
- This enables scenario planning and ROI forecasting for future campaigns.

- **Data-Driven Storytelling**  
- Clean, structured metrics (Conversions, Revenue, ROAS, CPA) can be directly fed into BI tools like Power BI or Looker.  
- Stakeholders get clear dashboards that support evidence-based decisions.

---

## 🔹 Why This Matters
Marketing leaders often struggle with incomplete or inconsistent data. This project demonstrates how **SQL transformations** can:
- Turn messy inputs into actionable KPIs.  
- Provide a framework for **scalable campaign analysis**.  
- Support **business analyst and data analyst roles** by showcasing both technical skill and strategic thinking.
