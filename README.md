# Business Impact of Chatbot Interactions

## 📂 Project Deep Dive
### Project Overview
An interactive business intelligence report designed to answer one central question: **What business impact is the chatbot driving, and what factors influence that impact?** The project connects perceived business impact with departments, analysis types, response speed, and user satisfaction to support exploratory analysis and inform discussions about where conversational analytics tools deliver the most value.

## 🛠️ Tech Stack & Core Competencies
* **Languages & Frameworks:** DAX
* **Analytics & Visualization:** Power BI Desktop, Advanced Data Visualization, Dashboard Design
* **Domain Focus:** AI & Chatbot Performance Analytics, Business Value Assessment, Exploratory Data Analysis

---
### Key Achievements & Objectives
* **Profiled Business Impact Distribution:** Quantified how chatbot interactions are spread across high, medium, and low perceived business impact, with missing values retained and labelled transparently.
* **Benchmarked Departmental Value:** Built stacked comparisons showing which departments generate more high‑impact interactions relative to low‑impact ones.
* **Engineered a High‑Impact Rate Measure:** Developed a DAX measure calculating the percentage of high‑impact interactions to compare value across descriptive, predictive, and trend‑analysis queries on a like‑for‑like basis.
* **Linked Speed, Satisfaction & Value:** Mapped response time against user feedback ratings, segmented by impact level, to explore whether faster or slower responses tend to be perceived as more valuable.
* **Designed Interactive Filtering:** Added department, analysis type, and date slicers so users can isolate specific segments and time periods.

---
## 📊 Dashboard Page & Preview
### Business Impact Overview
A single analytical page combining headline KPIs with four supporting visuals.

**Headline KPIs**
* **High‑Impact Interaction Rate:** Share of all interactions classified as high business impact.
* **Average User Feedback Rating:** Mean satisfaction score across interactions (1–5 scale).
* **Typical / Median Response Time:** Median chatbot response time in milliseconds, used to reduce the influence of outliers.

**Visuals**
| # | Visual | Chart Type | Fields | Purpose |
|---|--------|-----------|--------|---------|
| 1 | Business Impact Level Distribution | Bar chart | X: `estimated_business_impact` · Y: Count of `interaction_id` | Shows how many interactions are perceived as high, medium, or low impact |
| 2 | Business Impact by Department | Stacked bar chart | X: `department` · Legend: `estimated_business_impact` · Y: Count of `interaction_id` | Identifies which departments see more high‑impact vs low‑impact interactions |
| 3 | High‑Impact % by Analysis Type | Clustered bar chart | X: `analysis_type` · Y: `High_Impact_Pct` (DAX) | Compares whether predictive, descriptive, or trend analysis generates higher perceived value |
| 4 | Impact vs Response Time and Rating | Bubble / scatter chart | X: `response_time_ms` · Y: `user_feedback_rating` · Colour: `estimated_business_impact` | Explores how speed and satisfaction together relate to business impact |

**Slicers:** Department (Finance, HR, Marketing, Operations, Sales) · Analysis Type (Descriptive, Predictive, Trend Analysis) · Date range (Feb 2025 – Feb 2026)

![Business impact dashboard](visuals/business-impact-dashboard.png)

### Key DAX Measure
```DAX
High_Impact_Pct =
DIVIDE(
    CALCULATE( COUNT( 'chatbot'[interaction_id] ), 'chatbot'[Impact_Clean] = "High" ),
    COUNT( 'chatbot'[interaction_id] )
)
```

---

## 💡 Selected Observations & Insights
* **Medium Impact Dominates:** Of 3,200 interactions, 1,240 (39%) are rated medium impact, 932 (29%) low, and 691 (22%) high, with 337 (11%) unrated. Overall, the high‑impact interaction rate is about 22%.
* **Advanced Analytics Edge Ahead:** Predictive (22.3%) and trend‑analysis (22.2%) queries show slightly higher high‑impact rates than descriptive queries (20.2%), suggesting more advanced analytics are perceived as somewhat more valuable. The gap is small, so it should be read as a mild tendency rather than a strong effect.
* **Usage Drives Volume:** HR and Operations are the heaviest chatbot users (660 and 658 interactions) and generate a substantial volume of both medium‑ and high‑impact interactions. HR records the most high‑impact interactions (150), while Finance records the fewest (119).
* **Speed and Satisfaction Show Little Separation:** Median response times are similar across impact levels (about 1.3–1.5 seconds), and the average feedback rating sits at roughly 3.2 out of 5 for high, medium, and low impact alike. This suggests response speed and satisfaction are not strongly associated with perceived business impact in this dataset.
* **Stable Model Confidence:** Supporting analysis shows average bot confidence scores tightly clustered at around 0.79–0.80 across Customer, Finance, Marketing, Revenue, and Sales query categories, indicating consistent model performance regardless of topic.

*Note: These observations describe descriptive patterns within the dataset and do not establish that department, analysis type, or response speed directly causes changes in perceived business impact.*

---

## ⚙️ Repository Architecture & Usage

### Repository Contents
* `dashboard/`: Contains the primary Power BI report file (`Business-Impact-of-Chatbot-Interactions.pbix`).
* `visuals/`: Contains high‑resolution screenshots of the report page.
* `data/`: Contains the source dataset (`BI_Chatbot_Interactions.xlsx`).
* `README.md`: Project overview, structured methodology, and data documentation.

### How to View the Project
1. **Quick Preview:** Review the high‑resolution dashboard screenshot embedded in the section above.
2. **Download File:** Clone this repository or download the `.pbix` file directly from the `dashboard` folder.
3. **Launch Environment:** Open the file locally using **Power BI Desktop**.
4. **Interactive Exploration:** Use the department, analysis type, and date slicers to filter every visual and KPI on the page.

---

## 📋 Data Source & Technical Limitations

### Dataset Profile
This project utilizes the **Business Intelligence Chatbot Interaction Dataset** published by `jawadaahmed` on Kaggle (file: `data/BI_Chatbot_Interactions.xlsx`). The dataset contains **3,200 chatbot interaction records** across **12 fields**, covering **27 February 2025 to 9 February 2026**.

| Field | Description |
|-------|-------------|
| `interaction_id` | Unique interaction identifier (e.g. INT‑100000) |
| `timestamp` | Date and time of the interaction |
| `department` | Finance, HR, Marketing, Operations, Sales |
| `user_role` | Analyst, Executive, Intern, Manager |
| `user_query` | Natural‑language question asked of the chatbot |
| `query_category` | Customer, Finance, Marketing, Revenue, Sales |
| `metrics_requested` | Churn Rate, Conversion Rate, Profit Margin, Revenue, ROI |
| `analysis_type` | Descriptive, Predictive, Trend Analysis |
| `bot_response_confidence` | Model confidence score (0.60–0.99) |
| `response_time_ms` | Response time in milliseconds (200–2,499) |
| `user_feedback_rating` | User satisfaction rating (1–5) |
| `estimated_business_impact` | High, Medium, Low |

**Data Preparation:** The `estimated_business_impact` field was standardized into a cleaned column (`Impact_Clean`). The 337 records with no recorded impact are retained and shown as a separate missing (`nan`) category rather than being dropped, so totals remain transparent. The `user_feedback_rating` field also has 339 missing values, which are excluded from rating averages.

The source is a simulated dataset devoid of personally identifiable information (PII). It is applied strictly for educational evaluation, technical portfolio demonstration, and exploratory analysis rather than to assert definitive findings about a live organization or production chatbot.
* **Source:** [Business Intelligence Chatbot Interaction Dataset — jawadaahmed via Kaggle](https://www.kaggle.com/datasets/jawadaahmed/business-intelligence-chatbot-interaction-dataset)
* **Dataset License:** [License]

### Limitations & Scope Constraints
* **Perceived, Not Measured, Value:** Business impact is an estimated rating rather than a measured financial or operational outcome.
* **Descriptive Scope:** The report delivers descriptive patterns rather than prescriptive recommendations or validated predictive modelling.
* **Missing Values:** About 11% of interactions lack an impact rating and about 11% lack a feedback rating, which may affect the distribution of impact categories and satisfaction averages.
* **Data Dependency:** Analytical accuracy depends on the source dataset's quality, definitions, and population coverage.
* **Non‑Causal Insights:** Identified associations represent correlations and should not be interpreted as causal relationships.

---

## 🛡️ Academic & Data Integrity Notice
The materials hosted in this public repository represent independent applications of data analytics methodologies using publicly available, synthesized data. They do not contain proprietary corporate materials, protected institutional data, or restricted commercial information.

**Author:** Takudzwa Melody Mazhambe | [LinkedIn](https://www.linkedin.com/in/takudzwa-melody-mazhambe-80b0501a1/)
