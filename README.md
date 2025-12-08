# End-to-End Chinese News Analytics: From Web Crawling to Co-occurrence, PMI, and Document Similarity

## Overview
This repository implements a programming-first, end-to-end data science workflow on contemporary Chinese news. We collect our own datasets from ChinaNews and Sina News via web crawling, perform rigorous data cleaning and management, and conduct interpretable analytics including adjacent character co-occurrence probabilities, pointwise mutual information (PMI), word frequency analysis, and document-level mutual information. The pipeline emphasizes reproducibility, code-driven analysis, and visual storytelling through heatmaps, histograms, network graphs, and word clouds.

Key contributions:
- Self-collected datasets from two major Chinese news sources (ChinaNews and Sina News).
- Clean, reproducible pipeline for co-occurrence and PMI analysis at the character level.
- Word-level insights (frequency distributions, word clouds) and article complexity metrics.
- Document-level mutual information and comprehensive visualizations for comparative analysis.

## Motivation & Team Background
- Motivation: Public news streams capture evolving narratives across markets, policy, and society. Analyzing linguistic patterns—at both character and word levels—reveals common collocations, topic markers, and stylistic trends. We focus on interpretable, programming-driven analytics rather than model complexity, ensuring transparency and reproducibility aligned with course guidelines.
- Team Background: The team combines strengths in Python programming, web scraping, Chinese NLP preprocessing, and visualization. Roles span data collection, cleaning/engineering, exploratory analysis, PMI and co-occurrence modeling, and report/presentation.
- Contributions: Each member contributes meaningfully to the pipeline; workload distribution is fair and recorded. (Detailed names and roles to be appended in the final version.)

## Data
### Sources and scale
- ChinaNews: 10 scroll pages crawled (news1.html to news10.html); titles and article content collected into `data/chinanews.csv` (965 articles).
- Sina News: 20 roll pages crawled; titles and article content collected into `data/xinlangnews.csv` (975 articles).

### Collection methodology
- Dynamic pages: Headless Chrome via `selenium` and `webdriver-manager`; standardized User-Agent; randomized delays (`time.sleep` with uniform/rand) to reduce bot detection.
- Content extraction: `requests` for article pages; `BeautifulSoup` + `lxml` parsing; removal of ads/script/style/image/iframe blocks; fallbacks for multiple page templates (e.g., `id='artibody'`, `class='article'`, `class='content'`).
- Cleaning: HTML stripping, whitespace normalization, retention of Chinese characters and common punctuation; removal of specific trailing promotional segments (e.g., “海量资讯、精准解读”), editor notes (e.g., `【编辑:...】`).

### Data artifacts (examples)
- Raw CSVs: `data/chinanews.csv`, `data/xinlangnews.csv`
- Analysis results: `data/*_analysis_results_{corpus,cooccur_prob,char_count,pmi_result}.{txt,json,csv}`
- Cleaned artifacts: `data/*_cleaned_{char_count,cooccur_prob}.json`
- PMI special outputs: `data/*_pmi_analysis.{json,csv}`
- Document MI outputs: `data/*_document_mutual_info_results.csv`
- PMI comparison: `data/cleaned_pmi_comparison_results.csv`, `data/cleaned_pmi1.json`, `data/cleaned_pmi2.json`

### Ethics & licensing
- Publicly accessible content collected strictly for academic coursework.
- Respectful scraping: randomized delays, standard UA, exclusion of non-content and ads.
- No benchmark datasets; all data is self-collected per Course_Project_Guidelines.
- For removal requests or additional licensing clarifications, please open an issue.

## Repository Structure
```
.
├── Data_Collection_ChinaNews.ipynb         # web crawling: ChinaNews
├── Data_Collection_XinlangNews.ipynb       # web crawling: Sina News
├── Data_Analysis_ChinaNews.ipynb           # corpus cleaning, co-occurrence, PMI (ChinaNews)
├── Data_Analysis_XinlangNews.ipynb         # corpus cleaning, co-occurrence, PMI (Sina)
├── Data_Processing_corpus_prob_analysis_ChinaNews.ipynb   # cleaned co-occurrence + viz (ChinaNews)
├── Data_Processing_corpus_prob_analysis_XinlangNews.ipynb # cleaned co-occurrence + viz (Sina)
├── Data_Processing_pmi_analysis.ipynb      # cleaned PMI comparison (Sina vs. ChinaNews)
├── Data_Visualization_word_frequency_analysis.ipynb       # word frequency, word clouds, complexity
├── Data_Visualization_articles_avg_pmi_analysis.ipynb     # document-level MI matrix & viz
├── data/                                   # datasets & derived artifacts (CSV/JSON/TXT)
├── picture/                                # saved figures (PNG)
├── part_introduction.md                    # project introduction (complementary)
├── README.md                               # Description of Our Project
└── requirements.txt                        # environment dependencies
```

## Environment & Installation
```bash
# Create and activate a virtual environment
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows PowerShell
# .venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt
```
Dependencies include:
- Web scraping: `selenium`, `webdriver-manager`, `requests`, `beautifulsoup4`, `lxml`
- Processing & analysis: `pandas`, `numpy`, `jieba`
- Visualization: `matplotlib`, `seaborn`, `networkx`, `wordcloud`, `Pillow`

## How to Reproduce (Run Order)
You can run the full pipeline from scratch or start from provided data artifacts.

### Option A: Full pipeline (from raw collection)
1) Data collection
   - `Data_Collection_ChinaNews.ipynb`
   - `Data_Collection_XinlangNews.ipynb`
   - Outputs: `data/chinanews.csv`, `data/xinlangnews.csv`
2) Base analysis and PMI computation
   - `Data_Analysis_ChinaNews.ipynb` → `data/chinanews_analysis_results_*`, `data/chinanews_pmi_analysis.{json,csv}`
   - `Data_Analysis_XinlangNews.ipynb` → `data/xinlangnews_analysis_results_*`, `data/xinlangnews_pmi_analysis.{json,csv}`
3) Cleaned co-occurrence and visualization
   - `Data_Processing_corpus_prob_analysis_ChinaNews.ipynb` → `data/chinanews_cleaned_*`, `picture/chinanews_cleaned_*`
   - `Data_Processing_corpus_prob_analysis_XinlangNews.ipynb` → `data/xinlangnews_cleaned_*`, `picture/xinlangnews_cleaned_*`
4) Cleaned PMI comparison (cross-source)
   - `Data_Processing_pmi_analysis.ipynb` → `data/cleaned_pmi_*`, `picture/cleaned_pmi_comparison_analysis.png`
5) Word frequency and article complexity
   - `Data_Visualization_word_frequency_analysis.ipynb` → `picture/{basedata}_xlres.png`, `picture/{basedata}_wordclouds.png`, `picture/{basedata}_complexity_analysis.png`
6) Document mutual information (pairwise article MI)
   - `Data_Visualization_articles_avg_pmi_analysis.ipynb` → `data/{basedata}_document_mutual_info_results.csv`, `picture/{basedata}_document_mutual_info_analysis.png`

### Option B: Use existing data artifacts
- Skip step 1; start from step 2 using `data/*.csv` and `data/*_analysis_results_*` already in the repository.

## Dependencies & Why/How (Key Packages)
- `selenium`, `webdriver-manager`: Headless browser automation for dynamic pages and robust navigation.
- `requests`, `beautifulsoup4`, `lxml`: HTTP retrieval and structured HTML parsing for content extraction.
- `pandas`, `numpy`: Tabular manipulation, numeric computations, and pipeline-friendly data handling.
- `jieba`: Chinese word segmentation for word-level frequency analysis and complexity metrics.
- `matplotlib`, `seaborn`: Plotting distributions, heatmaps, bar charts, and annotated figures.
- `networkx`: Building and rendering directed co-occurrence network graphs.
- `wordcloud`, `Pillow`: Chinese word cloud generation with font support and high-quality image output.

## Data Engineering, Cleaning, and Management
- Cleaning & engineering:
  - Strip HTML tags/script/style; remove ads or non-content blocks; normalize whitespace; retain Chinese characters and common punctuation.
  - Adjacent character co-occurrence counts and conditional probabilities; PMI computed as `log2(P(c1,c2)/(P(c1)P(c2)))` with `P(c1,c2)=P(c2|c1)*P(c1)`.
  - Tokenization with `jieba` for word frequency analysis; word clouds and complexity metrics (lexical richness, average word length).
- Management & reproducibility:
  - Clear directory structure (`data/` and `picture/`) with intermediate and final artifacts saved as CSV/JSON/TXT.
  - Metadata files and cleaned versions to support inspection and re-use.
  - Requirements file and consistent notebook file paths for reproducible runs.

## Data Analysis: Learning, Analytics, Visualization
- Learning (interpretable metrics):
  - Character-level co-occurrence and PMI for collocational strength; document-level MI for cross-article similarity.
- Analytics:
  - Statistical summaries: unique characters, total pairs, PMI distributions (min/max/mean/median), common vs. unique pairs across sources.
  - Thresholding strong co-occurrence pairs (e.g., 10% of maximum) to surface salient relationships.
- Visualization:
  - Heatmaps (co-occurrence matrices; document MI), histograms (probabilities/PMI/differences), bar charts (top words/pairs), network graphs (directed co-occurrence), word clouds (content/title).

## Results & Insights (Representative)
- ChinaNews: frequent strong pairs reflect broad news topicality (军事/热点/体育/世界/国际). High-PMI pairs include formal fixed expressions and journalistic terms, suggesting tighter collocational patterns.
- Sina News: strong economic/market collocations (投资/公司/市场/基金/月日) and tech themes (AI、科技、证券). Word frequency analysis corroborates the topical lean.
- Cross-source PMI comparison: large common set of collocations with meaningful differences; ChinaNews slightly higher mean PMI in cleaned sets; scatter around y=x indicates broadly comparable collocational strength with deviations worthy of inspection.
- Document MI: distributions centered near mid-high values with subsets approaching ln(2) upper bound; top pairs reflect similar topics or stylistic overlap.

## Conclusion & Reflection
- A reproducible, interpretable pipeline transforms raw web data into actionable, code-driven analytics and visuals, aligning with course priorities.
- Limitations: adjacent-character PMI misses longer multi-character phrases; web layout changes can affect scraping; topic context is partially captured at character level.
- Future work: phrase-level PMI (n-grams), time-resolved trend analysis, topic clustering with interpretable features, cross-outlet dashboards.

## Presentation (to be added)
- Slides: `./slides/<file>.pdf` or `.html` or `.pptx`
- Video: `./video/<file>.mp4` (10–12 minutes)
- Content highlights: motivation, data, engineering pipeline, key findings; demo of core visualizations encouraged.

## References
- [jieba](https://github.com/fxsjy/jieba)
- [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/)
- [NetworkX](https://networkx.org/)
- [WordCloud for Python](https://amueller.github.io/word_cloud/)
- [Matplotlib](https://matplotlib.org/) / [Seaborn](https://seaborn.pydata.org/)

## Acknowledgements
This project adheres to the CISC7201 Data Science Programming Course Project Guidelines and uses self-collected datasets only, focusing on programming, reproducibility, and clear communication of insights.