# CISC7201 DATA SCIENCE PROGRAMMING — Course Project Guidelines

## 1. Project Purpose
The course project aims to give students hands-on experience with a full **end-to-end data science workflow**, including data collection, data engineering, data analysis, model development, and presentation of findings. Students are expected to demonstrate both technical competency and the ability to apply data science to real-world contexts.

More importantly, this project emphasizes **the use of programming** rather than relying on **off-the-shelf machine learning methods or automated tools**. Students who provide additional effort in data processing, feature engineering, analysis, and visualization will receive corresponding credit in the assessment. In addition, the good use of programming packages will received credit in the assessment. 

The focus is on programming proficiency, reproducibility, and the correct implementation of data science techniques, not on achieving the highest model accuracy or using complex models.

---

## 2. Team Formation
- Each team should consist of **4–5 students**. 
   - The project will be assessed using the same standard even if your team has fewer members.
   - The project will be assessed using a higher standard if your team has 6 members. 
- Team members are encouraged to bring diverse strengths (programming, analytics, visualization, domain knowledge).  
- Every member must contribute meaningfully; workload distribution should be fair and explicitly documented.
- For **contribution assessment**, each member will be asked to evaluate the contributions of their teammates confidentially.

---

## 3. Project Requirements

### A. Motivation & Team Background (Mandatory Section)
Your report must clearly address:

1. **Motivation**  
   - Why did you choose this topic?  
   - What real problem or question does your project attempt to solve?  
   - Why is this problem important or interesting?

2. **Team Background**  
   - Introduce each team member’s strengths or relevant experience.  
   - Explain how the team’s background influenced the topic choice.  
   - Highlight any domain knowledge that supports the project.

> **A strong motivation section is essential. Projects with unclear motivation will receive lower marks regardless of technical quality.**

---

### B. Data Collection (Benchmark Datasets NOT Allowed)
Your team must **use your own dataset**. Possible sources include:

- Web scraping  
- Sensor/IoT data  
- Manually recorded logs  
- API retrieval (weather, finance, mobility…)  
- Surveys or interviews
- Collected images or videos 

Please keep your dataset size manageable. We will update you on the maximum dataset size that our repository can accommodate.

**Restrictions**
- **No benchmarking datasets** (MNIST, CIFAR, UCI, Kaggle defaults).  

---

### C. Data Engineering, Cleaning, and Management
You may include any relevant tasks from the following areas (not all are required):

#### I. Data Cleaning
- Handling missing or inconsistent values  
- Removing duplicates  
- Normalizing formats and data types  

#### II. Data Engineering
- Feature extraction and creation  
- Image or time-series preprocessing  
- Building reusable pipelines  

#### III. Data Management
- Clear folder/data organization  
- Git/GitHub version control  
- Documentation of workflows and metadata  
- Ensuring reproducibility of results  

---

### D. Data Analysis: Learning, Analytics, Visualization
This is a programming-focused course. The key is to apply programming techniques to analyze data -- **advanced machine learning models are not the main requirement**. You may include any relevant tasks from the following areas (not all are required):

#### Exploratory Analysis
- Statistical summaries  
- Correlation and trend analysis  
- Visualizations (plots, charts, dashboards)  

#### Modeling & Evaluation
- Machine learning models (classification, regression, clustering…)  
- Performance metrics and interpretation  
- Comparison between baseline and improved models  

#### Visualization & Interpretation
- Effective visual storytelling  
- Meaningful insights and explanations  

---

### E. Conclusion
Your conclusion should include:
- Key findings  
- Limitations  
- Reflection on what the team learned  
- Possible future improvements  

---
## Data Analysis: Learning, Analytics, Visualization
This is a programming-focused project; we apply code-first techniques to produce interpretable metrics and visualizations. We summarize results by notebook, integrating printed outputs and saved figures.

### Exploratory Analysis
- Statistical summaries (collection notebooks):
  - ChinaNews: 965 articles (`df.info()`), title/content columns non-null; confirms robust scraping.
  - Sina News: 975 articles (`df.info()`), title/content columns non-null; confirms broad coverage.
- Corpus statistics (analysis notebooks):
  - ChinaNews: ~3,968 unique Chinese characters; 165,590 adjacent pairs with PMI computed.
  - Sina News: ~3,526 unique characters; 181,393 adjacent pairs with PMI computed.
- Word-level EDA (word frequency notebook):
  - Frequency counters yield top 15 content/title words; e.g., Sina content: 我们、公司、市场、产品、中国、企业、可能、罗永浩、亿元、科技。Titles include 股份、中国、AI、公司、科技、市场、目录、证券、创新。
- Article complexity:
  - Lexical richness (unique words / total words) and average word length histograms per dataset; saved as `{basedata}_complexity_analysis.png`.

### Correlation and Trend Analysis (interpretable signals)
- Adjacent character co-occurrence probabilities:
  - Heatmaps summarize conditional P(c_j|c_i) across top characters; axes annotated for leading/following characters; cleaned versions saved (e.g., `chinanews_cleaned_cooccurrence_analysis.png`, `xinlangnews_cleaned_cooccurrence_analysis.png`).
  - Probability matrix statistics (ChinaNews example): min ~0, max ~0.7419, mean ~0.00653, non-zero elements ~1,161 after cleaning.
- PMI distributions:
  - ChinaNews PMI: highest ~21.1805; lowest ~-9.1123; mean ~2.1507; median ~1.6918.
  - Sina PMI: highest ~20.6244; lowest ~-8.5090; mean ~1.6269; median ~1.0865.
  - Histograms of PMI/non-zero probabilities provide distributional insight (see saved figures).
- Document-level mutual information:
  - MI(P,Q)=0.5*(KL(P||M)+KL(Q||M)), M=0.5*(P+Q); heatmap plus histogram of upper-triangle values; stats box with min/max/mean/median and counts (e.g., for Sina: MI range [0, 0.693147], average ~0.4539, median ~0.4560).
  - Results CSV saved for further analysis (e.g., `xinlangnews_document_mutual_info_results.csv`).

### Modeling & Evaluation (lightweight, interpretable metrics)
- While advanced ML models are optional, we implement:
  - Character-level PMI to quantify collocational strength.
  - Document-level MI to assess article similarity; top MI pairs printed with titles.
- Evaluation and comparison:
  - Cross-source PMI comparison on common pairs (~47,189):
    - Scatter vs. y=x line reveals broadly comparable strengths with deviations; average difference (ChinaNews − Sina) ~0.023.
    - Top absolute differences highlight collocations more prominent in one outlet; barh chart saved (`cleaned_pmi_comparison_analysis.png`).
  - Data volumes: totals, common, unique pairs plotted as bars to contextualize comparison.

### Visualization & Interpretation
- Effective visual storytelling:
  - Heatmaps (co-occurrence; MI) for structural overview.
  - Histograms (PMI values; differences; article complexity) for distributions and spread.
  - Bar charts for top co-occurrence pairs and top PMI values—annotated with exact values.
  - Word clouds for intuitive topic emphasis (content vs. title).
  - Network graphs of strongest co-occurrence edges (directional, weighted), highlighting clusters (e.g., ChinaNews: 军→事, 热→点, 体→育; Sina: 投→资, 公→司, 市→场).
- Meaningful insights:
  - ChinaNews emphasizes national/international topical markers (军事、热点、体育、世界、国际), visible in strong pairs and PMI rankings.
  - Sina News leans toward economic/market/tech themes (投资、公司、市场、基金、AI、科技、证券), confirmed across frequency analysis, co-occurrence, and PMI.
  - Document MI reveals groups of similar articles (e.g., finance sector reports), aligning with visible topical clusters.

## Results & Insights (Representative)
- Co-occurrence & PMI
  - ChinaNews: cleaned strong pairs reflect conventional journalistic collocations—e.g., 军→事 (0.7419), 热→点 (0.6546), 体→育 (0.5310), 世→界 (0.4323), 国→际 (0.3879), 中→国 (0.3593).
  - Sina News: economic collocations dominate—投→资 (0.7000), 公→司 (0.6958), 市→场 (0.6004), 基→金 (0.3955), 月→日 (0.3439).
  - Top PMI values surface fixed/formal expressions (e.g., ChinaNews: 妊娠、锱铢、哀悼等；Sina: 淫秽、蜡烛、牺牲、峥嵘等)—indicative of style and formal language.
- Word Frequency & Complexity
  - Title/content frequency confirms outlet tendencies (Sina: 公司/市场/科技/AI；ChinaNews: broader public topics). Word clouds visually emphasize these themes.
  - Lexical richness and average word length distributions characterize article style variability; differences across datasets are consistent with editorial focus.
- Cross-Source Comparison
  - PMI scatter around y=x shows general alignment with notable differences; ChinaNews slightly higher mean PMI post-cleaning.
  - Unique collocations per outlet (large counts) indicate distinctive phraseology and topical emphasis.
- Document-Level Similarity
  - MI matrix shows a central tendency with a tail of near-maximum MI pairs; top document pairs cluster around similar coverage/events (as seen in printed titles), supporting content curation or topic grouping.

## Conclusion & Reflection
- Key findings:
  - A programming-first pipeline reliably transforms raw web news into interpretable analytics: collocational structures (PMI/co-occurrence), topic emphasis (word frequency/word clouds), and article similarity (MI).
  - ChinaNews emphasizes national/international markers; Sina emphasizes market/tech themes—visible across co-occurrence, PMI, and frequency.
- Limitations:
  - Adjacent-character PMI misses multi-character phrases; topic context is only partially captured at character level.
  - Web page structure changes may affect scraping; some pages require template-specific fallbacks.
  - Jaccard-style document similarity approximates overlap; more nuanced topic models could add context (optional per course).
- Reflection:
  - Focusing on interpretable metrics and reproducible code improves transparency and auditability; the pipeline can be extended with limited effort.
  - Visual storytelling (heatmaps, networks, word clouds) effectively communicates insights to non-technical audiences.
- Future improvements:
  - Phrase-level n-grams and PMI; time-series trends; interpretable topic clustering; cross-outlet dashboards; lightweight baselines for classification (optional).
---
## 4. Deliverables

We will create a repository for each project team on Gitea. You only need to **commit your files to the repository** before the deadline.

### A. Jupyter Notebook
- Clear structure following the required sections  
- Professional English writing  
- Proper references 
- Codes
- IMPORTANT: list all important programming packages you use and explain why / how you use them

### B. Code Structure (Optional)
- Organized GitHub repository  
- README with execution instructions  
- Structured notebooks/scripts  

### C. Presentation
- slides in pdf, html, or pptx
- 10–12 minutes in mp4
- Highlight motivation, dataset, engineering pipeline, findings  
- Demo or visualization encouraged  

### D. Readme.md
- Description of your project
- An example can be found in a recent project, https://github.com/showlab/Paper2Video

---

## 5. Timeline

| Stage | Due Date |
|----------|------------|
| Team grouping | 2025-11-21 |
| Project material submissions | 2025-12-14 |

---

## 6. Grading Breakdown

| Component | Percentage |
|----------|------------|
| Motivation & Background | 15% |
| Data Collection, Data Engineering & Cleaning | 35% |
| Data Analysis & Modeling | 35% |
| Conclusion & Reflection | 10% |
| Professionalism | 5% |

In exceptional cases where the data is collected from laboratory, e.g., biology data, it is acceptable to skip the data collection section. **Please note that the use of benchmark datasets remains strictly prohibited.** However, we expect you to contribute significantly more effort to the data analysis component.

| Component | Percentage |
|----------|------------|
| Motivation & Background | 15% |
| Data Analysis & Modeling | 70% |
| Conclusion & Reflection | 10% |
| Professionalism | 5% |
