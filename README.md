````markdown
# 🏏 ICC Men's T20 Cricket World Cup 2022 — Data Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-Data%20Processing-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Web Scraping](https://img.shields.io/badge/Web%20Scraping-Bright%20Data-success)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

# 📌 Project Overview

This project is a comprehensive **Player Performance Analytics Dashboard** built using **ICC Men's T20 Cricket World Cup 2022** data. The project combines **Python for web scraping & data preprocessing** with **Power BI for data visualization** to provide an interactive platform for player analysis and team selection.

### ✨ Key Features

- 📊 Analyse and compare individual player performances across all World Cup matches
- 🧠 Build the best Final Playing 11 using data-driven selection criteria
- 🔍 Explore players by role: Power Hitters, Anchors, Finishers, All-Rounders, and Specialist Fast Bowlers
- 📈 Interactive Power BI dashboard with dynamic filters and KPIs

> **💡 To interact with the dashboard, download the `.pbix` file from this repository and open it in Power BI Desktop.**

---

# 📋 Table of Contents

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
- References
- Acknowledgements

---

# ❓ Problem Statement

Cricket coaches, analysts, and fans often struggle to objectively compare player performances across different teams and match conditions.

This project addresses that challenge by building an interactive Power BI dashboard that:

- 🏏 Reviews and compares player performances from the T20 World Cup 2022
- 📊 Enables users to build their own Final Playing 11 from the complete tournament pool
- 🎯 Evaluates players using role-specific performance metrics such as Batting Average, Strike Rate, Bowling Economy, and Dot Ball Percentage

---

# 📂 Dataset Information

| Detail | Information |
|----------------------|--------------------------------|
| **Source** | ESPN Cricinfo |
| **Scraping Tool** | Bright Data + BeautifulSoup |
| **Tournament** | ICC Men's T20 Cricket World Cup 2022 (Australia) |
| **Coverage** | Qualifier Stage + Super 12 |
| **Data Types** | Match Results, Batting Summary, Bowling Summary, Player Information |

### 📁 Key Files

- **t20_batting_summary** — Innings-level batting statistics
- **t20_bowling_summary** — Innings-level bowling statistics
- **t20_players_info** — Player metadata and playing roles
- **t20_match_results** — Match details and match IDs

---

# 🔄 Project Workflow

```
Requirement Scoping
        ↓
Web Scraping
(ESPN Cricinfo via Bright Data + BeautifulSoup)
        ↓
Data Cleaning & Preprocessing
(Python + Pandas)
        ↓
Data Transformation
(Power Query)
        ↓
Data Modelling & DAX
(Power BI)
        ↓
Interactive Dashboard Development
```

---

# 🌐 Data Collection

All match and player information was collected from **ESPN Cricinfo** using **Bright Data** as the scraping infrastructure and **BeautifulSoup** as the HTML parser.

The scraped JSON data was converted into **Pandas DataFrames** using Jupyter Notebook and exported as CSV files for Power BI analysis.

---

# 🧹 Data Transformation

## Stage 1 — Python (Pandas)

- ✅ Corrected player name inconsistencies
- ✅ Handled missing values
- ✅ Linked Match IDs across batting and bowling tables

## Stage 2 — Power Query (Power BI)

- ✅ Final data shaping
- ✅ Column renaming
- ✅ Merging datasets
- ✅ Creating conditional columns for role-based filtering

---

# 🗃️ Data Modelling

The data model was designed using relational tables connected through primary keys.

### Relationships

- **matchID** → Links batting summary, bowling summary, and match results
- **team** → Links player information with match data

Additional calculated columns and parameters were created to enable dynamic player selection and role-based filtering.

---

# ⚙️ DAX Measures

## 🏏 Batting Measures

```DAX
Total Runs =
SUM(t20_batting_summary[runs])

Total Innings Batted =
COUNT(t20_batting_summary[matchID])

Total Innings Dismissed =
SUM(t20_batting_summary[Out])

Batting Avg =
DIVIDE([Total Runs], [Total Innings Dismissed], 0)

Total Balls Faced =
SUM(t20_batting_summary[balls])

Strike Rate =
DIVIDE([Total Runs], [Total Balls Faced], 0) * 100

Batting Position =
ROUNDUP(AVERAGE(t20_batting_summary[battingPos]), 0)

Boundary % =
DIVIDE(SUM(t20_batting_summary[Boundary runs]), [Total Runs], 0) * 100

Avg. Balls Faced =
AVERAGE(t20_batting_summary[balls])

Boundary Runs Batting =
t20_batting_summary[fours] * 4 +
t20_batting_summary[sixes] * 6
```

## 🎯 Bowling Measures

```DAX
Wickets =
SUM(t20_bowling_summary[wickets])

Balls Bowled =
SUM(t20_bowling_summary[balls])

Runs Conceded =
SUM(t20_bowling_summary[runs])

Economy =
DIVIDE([Runs Conceded], ([Balls Bowled]/6), 0)

Bowling Strike Rate =
DIVIDE([Balls Bowled], [Wickets], 0)

Bowling Average =
DIVIDE([Runs Conceded], [Wickets], 0)

Total Innings Bowled =
DISTINCTCOUNT(t20_bowling_summary[matchID])

Dot Ball % =
DIVIDE(
SUM(t20_bowling_summary[zeros]),
SUM(t20_bowling_summary[balls]),
0
)

Boundary Runs Bowling =
t20_bowling_summary[fours] * 4 +
t20_bowling_summary[sixes] * 6
```

## 🧩 Dynamic Selection Measures

```DAX
Player Selection =
IF(ISFILTERED(t20_players_info[name]),"1","0")

Display Text =
IF(
[Player Selection]="1",
" ",
"Select Player(s) by clicking the player's name to see their individual or combined strength"
)

Color Callout Value =
IF([Player Selection]="0","#E8D166","#1D1D2E")
```

---

# 🎯 Player Selection Criteria

The dashboard enables users to build their own **Final Playing 11** using role-based performance criteria.

## 💥 Power Hitters / Openers

| Parameter | Criteria |
|----------------|------------|
| Batting Average | > 30 |
| Strike Rate | > 140 |
| Innings Batted | > 3 |
| Boundary % | > 50 |
| Batting Position | < 4 |

---

## ⚓ Anchors / Middle Order

| Parameter | Criteria |
|----------------|------------|
| Batting Average | > 40 |
| Strike Rate | > 125 |
| Innings Batted | > 3 |
| Avg. Balls Faced | > 20 |
| Batting Position | > 2 |

---

## 🏁 Finishers / Lower Order

| Parameter | Criteria |
|----------------|------------|
| Batting Average | > 25 |
| Strike Rate | > 130 |
| Innings Batted | > 3 |
| Avg. Balls Faced | > 12 |
| Batting Position | > 4 |
| Innings Bowled | > 1 |

---

## 🔄 All-Rounders

| Parameter | Criteria |
|----------------|------------|
| Batting Average | > 15 |
| Strike Rate | > 140 |
| Innings Batted | > 2 |
| Batting Position | > 4 |
| Innings Bowled | > 2 |
| Bowling Economy | < 7 |
| Bowling Strike Rate | < 20 |

---

## 🎳 Specialist Fast Bowlers

| Parameter | Criteria |
|----------------|------------|
| Innings Bowled | > 4 |
| Bowling Economy | < 7 |
| Bowling Strike Rate | < 16 |
| Bowling Style | Fast |
| Bowling Average | < 20 |
| Dot Ball % | > 40 |

---

# 📊 Dashboard Screenshots

## 🔢 Final Playing 11

> *Add Screenshot Here*

---

## 💥 Power Hitters

> *Add Screenshot Here*

---

## ⚓ Anchors

> *Add Screenshot Here*

---

## 🏁 Finishers

> *Add Screenshot Here*

---

## 🔄 All-Rounders

> *Add Screenshot Here*

---

## 🎳 Specialist Fast Bowlers

> *Add Screenshot Here*

---

# 🛠️ Tools & Technologies

| Tool | Purpose |
|-----------------------------|--------------------------------|
| Python | Core scripting language |
| BeautifulSoup | HTML parsing & web scraping |
| Bright Data | Web scraping infrastructure |
| Pandas | Data cleaning & preprocessing |
| Jupyter Notebook | Data transformation & EDA |
| Microsoft Power BI Desktop | Dashboard development |
| Power Query | Data transformation |
| DAX | Measures & calculated columns |
| ESPN Cricinfo | Primary data source |

---

# 📎 References

- 📌 ESPN Cricinfo — T20 World Cup 2022
- 📌 Bright Data — Web Scraping Platform
- 📌 Microsoft Power BI Documentation

---

# 🙌 Acknowledgements

Special thanks to the open cricket data community and ESPN Cricinfo for making cricket statistics accessible for analytical and educational projects.

---

# ⭐ Support

If you found this project useful, consider giving it a **⭐ Star** on GitHub!
````
