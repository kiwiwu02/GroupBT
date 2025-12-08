## 团队成员
团队有五个成员中有同学 A BC 均匀人工智能专业方向背景，对 NLP 感兴趣，DE是Marketing Analytics专业方向，对财经内容感兴趣

## 主要工作内容
同时我告诉你我这个项目大致的工作内容：专注于中文新闻文本的挖掘与分析。我们通过混合爬虫技术从新浪财经网与中国新闻网批量获取新闻文本，构建了一个高质量的对比语料库，并系统性地实现了汉字邻近同现概率、点式互信息（PMI）及文档间互信息的计算与可视化分析。

- 全流程覆盖：从数据采集、清洗、统计分析到结果可视化的完整NLP项目流程。
- 双源对比：基于新浪新闻与网易新闻的对比语料库，进行深入的对比分析。
- 多维度分析：涵盖字符级（邻近同现）、词汇级（PMI）和文档级（互信息）的文本分析。
- 完整可视化：提供词云、热力图、分布图等多种可视化结果。

## 数据
数据获取时间为 12 月8 日下午 3 点，这两个完整最新发布的及 950-1000 条新闻标题及其对应的新闻内容，

URL 分别为：https://news.sina.com.cn/roll/#pageid=153&lid=2509&k=&num=50&page={i} 和 https://www.chinanews.com.cn/scroll-news/news1.html



## 运行顺序
requirements.txt                   # 项目依赖

项目使用Selenium进行动态页面爬取，需要安装Chrome浏览器和对应的ChromeDriver：
- 确保已安装 Google Chrome
- 下载对应版本的 ChromeDriver
- 将ChromeDriver所在目录添加到系统PATH环境变量中

建议按以下顺序执行代码文件，以确保数据流的完整性：
- 首先执行数据采集
    - 01_数据采集/Data_Analysis_XinlangNews.ipynb # 新浪新闻网爬取
    - 01_数据采集/Data_Collection_ChinaNews.ipynb # 中国新闻网爬取
- 然后进行数据清洗和分析
    - 02_数据分析/Data_Analysis_XinlangNews.ipynb # 新浪数据分析
    - 02_数据分析/Data_Analysis_ChinaNews.ipynb # 中国新闻网数据分析
- 进行核心算法计算
    - 03_核心计算/Data_Processing_corpus_prob_analysis_XinlangNews.ipynb# 对新浪财经新闻邻近同现概率
    - 03_核心计算/Data_Processing_corpus_prob_analysis_ChinaNews.ipynb # 对中国新闻网邻近同现概率
    - 03_核心计算/visual_pmi_analysis.ipynb # Data_Processing_pmi_analysis.ipynb
- 最后生成可视化结果
    - 04_可视化/Data_Visualization_articles_avg_pmi_analysis.ipynb# 对两个网站的新闻进行文档互信息可视化
    - 04_可视化/Data_Visualization_word_frequency_analysis.ipynb # 对两个网站的新闻进行词频可视化
