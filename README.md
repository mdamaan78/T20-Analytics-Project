# 🏏 ICC Men's T20 Cricket World Cup 2022 — Data Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-PowerBI-F2C811?logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Web Scraping](https://img.shields.io/badge/Web%20Scraping-Bright%20Data-success)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Project Overview

This project is a comprehensive **Player Performance Analytics Dashboard** built on **ICC Men's T20 Cricket World Cup 2022** data. Using **Python** for web scraping and data preprocessing, and **Power BI** for visualization, the dashboard allows users to:

- 📊 Analyse & compare individual player performances across all World Cup matches
- 🧠 Pick the best Final 11 from the entire tournament pool based on data-driven selection criteria
- 🔍 Explore players by role — Power Hitters, Anchors, Finishers, All-Rounders, and Specialist Fast Bowlers

> 💡 To interact with the dashboard, download the **T20 Analytics Dashboard.pbix** file from this repository and open it in Power BI Desktop.

---

## 📋 Table of Contents

- Problem Statement
- Dataset Information
- Project Workflow
- Data Collection
- Data Transformation
- Data Modelling
- DAX Measures
- Player Selection Criteria
- Dashboard Screenshots
- Tools & Technologies

---

## ❓ Problem Statement

Cricket coaches, analysts, and fans often struggle to objectively compare player performances across different teams and conditions.

This project solves that by building an interactive Power BI dashboard that:

- Reviews and compares all player performances from the T20 World Cup 2022
- Enables users to build their dream Final 11 from the tournament pool
- Evaluates players based on role-specific criteria such as batting average, strike rate, economy and bowling average

---

## 📂 Dataset Information

| Detail | Info |
|------------|-----------------------------|
| Source | ESPN Cricinfo |
| Scraping Tool | Bright Data + BeautifulSoup |
| Tournament | ICC Men's T20 Cricket World Cup 2022 |
| Coverage | Qualifier Stage + Super 12 |
| Data Types | Match results, batting summaries, bowling summaries, player info |

### Key Files

- t20_batting_summary
- t20_bowling_summary
- t20_players_info
- t20_match_results

---

## 🔄 Project Workflow

```text
Requirement Scoping
      ↓
Web Scraping
      ↓
Data Cleaning & Preprocessing
      ↓
Data Transformation
      ↓
Data Modelling & DAX
      ↓
Dashboard Building
```

---

## 🌐 Data Collection

- ESPN Cricinfo
- Bright Data
- BeautifulSoup
- JSON → Pandas → CSV → Power BI

---

## 🧹 Data Transformation

### Stage 1 — Python (Pandas)

- Corrected player name inconsistencies
- Handled missing values
- Linked match IDs

### Stage 2 — Power Query

- Data shaping
- Column renaming
- Dataset merging
- Conditional columns

---

## 🗃️ Data Modelling

- matchID → batting, bowling & match results
- team → player information

Additional calculated columns and parameters enable dynamic player selection.

---

## ⚙️ DAX Measures

```DAX
Total Runs = SUM(t20_batting_summary[runs])

Batting Avg =
DIVIDE([Total Runs],[Total Innings Dismissed],0)

Strike Rate =
DIVIDE([Total Runs],[Total Balls Faced],0)*100

Economy =
DIVIDE([Runs Conceded],([Balls Bowled]/6),0)

Bowling Average =
DIVIDE([Runs Conceded],[Wickets],0)
```

---

## 🎯 Player Selection Criteria

### 💥 Openers / Power Hitters

| Parameter | Criteria |
|------------|------------|
| Batting Average | >30 |
| Strike Rate | >140 |
| Innings Batted | >3 |
| Boundary % | >50 |
| Batting Position | <4 |

### ⚓ Anchors

| Parameter | Criteria |
|------------|------------|
| Batting Average | >40 |
| Strike Rate | >125 |
| Avg Balls Faced | >20 |

### 🏁 Finishers

| Parameter | Criteria |
|------------|------------|
| Batting Average | >25 |
| Strike Rate | >130 |
| Innings Bowled | >1 |

### 🔄 All-Rounders

| Parameter | Criteria |
|------------|------------|
| Strike Rate | >140 |
| Bowling Economy | <7 |
| Bowling Strike Rate | <20 |

### 🎳 Specialist Fast Bowlers

| Parameter | Criteria |
|------------|------------|
| Bowling Economy | <7 |
| Bowling Strike Rate | <16 |
| Dot Ball % | >40 |

---

# 📊 Dashboard Screenshots

## 🔢 Final 11

![](final-11.jpg)

## 💥 Power Hitters

![](power-hitters.jpg)

![](openers_criteria.png)

## ⚓ Anchors

![](anchors.jpg)

![](anchors_criteria.png)

## 🏁 Finishers

![](finishers.jpg)

![](finishers_criteria.png)

![](lower-order-anchors_criteria.png)

## 🔄 All-Rounders

![](all-rounders.jpg)

![](all-rounders_criteria.png)

## 🎳 Specialist Fast Bowlers

![](specialist-fast-bowlers.jpg)

![](specialist-fast-bowlers_criteria.png)

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------------|----------------|
| Python | Scripting |
| BeautifulSoup | Web Scraping |
| Bright Data | Scraping Infrastructure |
| Pandas | Data Processing |
| Jupyter Notebook | EDA |
| Power BI | Dashboard |
| Power Query | Transformation |
| DAX | Measures |
| ESPN Cricinfo | Data Source |

---

## 📎 References

- ESPN Cricinfo
- Bright Data
- Microsoft Power BI Documentation

---

## 🙌 Acknowledgements

Special thanks to the open cricket data community and ESPN Cricinfo for making match and player data accessible for analytical projects.

⭐ If you found this project useful, please give it a star on GitHub!
