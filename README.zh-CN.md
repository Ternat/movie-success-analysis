# 电影成功因素分析

**一个关于"什么让电影成功"的端到端数据挖掘与可视化项目。**

本项目分析一份电影元数据数据集（约 4,800 部电影），探究哪些因素--预算、类型、关键词、时长、热度--真正区分了高评分、高票房的电影与其他电影。

![评分分布](images/rating-distribution.png)

## 项目展示的能力

- 数据清洗与特征工程（缺失值、伪缺失值、日期解析、特征提取）
- 包含 25+ 张图表的探索性数据分析（EDA）
- 无监督学习（KMeans 聚类）与监督学习（决策树分类）
- 将模型输出转化为可解释的业务洞察

## 主要发现

- **高预算买不来好口碑。** 预算与评分的相关性很弱--花更多钱并不一定能拍出更好的电影。
- **受众热度与评分同向变化。** KMeans（k=2，轮廓系数约 0.50）把电影分成"大片"聚类（评分约 7.06、约 2,950 票、热度约 68.7）和"小众"聚类（评分约 6.04、344 票、热度约 14.4）。
- **题材比规模更重要。** 高评分电影偏向情感共鸣类关键词（"friendship"、"biography"），而低评分电影更常出现泛化或暴力类关键词。
- **不同类型成功率不同。** 某些类型的电影在评分和商业成功上持续表现更好。
- **上映前的因素几乎预测不了评分。** 决策树分类器交叉验证 ROC-AUC 仅约 0.70，其判别力几乎完全来自上映后的 popularity（特征重要性 0.463），而非预算或时长；这说明票房与评分在很大程度上是事后结果，难以提前预测。

## 分析流程

1. **数据清洗与特征工程** - 去重、缺失值与伪缺失值（budget/revenue 中的 0 值）处理、时间解析、从类 JSON 字段中提取类型/关键词/国家/语言、构造衍生特征（年代、高评分标签、成功标志）。
2. **探索性数据分析（EDA）** - 分布、年份/年代趋势、预算-评分与时长-评分关系、类型/国家/语言分析，以及关键词词云。
3. **建模**
   - 无监督：KMeans 聚类，用轮廓系数选 k（k=2），并用 PCA 降维可视化。
   - 监督：决策树分类器（max_depth=4）预测高评分电影。
4. **洞察** - 区分高评分与低评分电影的关键词与类型模式。

## 技术栈

Python、pandas、NumPy、Matplotlib、Seaborn、scikit-learn、WordCloud

## 数据

电影元数据数据集（约 4,800 部电影），由课程提供，原始来源未注明。字段（budget、revenue、genres、keywords、popularity、vote_average、vote_count）与 The Movie Database（TMDB）的电影元数据一致，这是一类常见的教学数据集。如需复用原始数据，请注明原始来源。

## 运行方式

**在线查看 notebook（无需本地环境）：** [nbviewer](https://nbviewer.org/github/Ternat/movie-success-analysis/blob/main/movie-success-analysis.ipynb)

```bash
pip install -r requirements.txt
jupyter notebook movie-success-analysis.ipynb
```

## 项目结构

- `movie-success-analysis.ipynb` - 完整分析 notebook（可直接运行，含全部输出）
- `movies.csv` - 原始数据集
- `images/` - 从 notebook 导出的图表

## 语言

- [English version](README.md)
