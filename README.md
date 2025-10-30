# NCAA Men's Basketball Game Data Visualization and Analysis  

**Authors:**  
Yixiao Wang · Beijie Ji · Yiming Cheng · Zhihao Chen · Weitong Liang

---

## Introduction

The goal of this project is to build an interactive **Shiny web application** for visualizing and analyzing NCAA men's basketball data. The app aggregates historical game results, player and team statistics, and real‑time updates, providing a foundation for future predictive modeling.

NCAA men’s basketball, with the excitement of **March Madness**, is a major cultural and athletic phenomenon in the U.S. As Duke students and basketball fans, we aimed to create a platform that allows users to explore team performance, game dynamics, and player contributions in a visually appealing and intuitive way — with special focus on Duke University.

Our app includes five modules:

- **Game Data** — View games, scores, win probabilities, and player stats  
- **Team & Player Dashboard** — Explore team histories, schedules, performance metrics  
- **Schedule** — Real‑time NCAA game info + Duke‑specific updates  
- **Prediction** — Baseline model predicting Duke vs UNC outcomes  
- **Write‑Up** — Project explanation and methodology

---

## Methods / Implementation

We primarily use `ncaahoopR` and NCAA official data sources. Since we encountered errors and inconsistencies in official data, we developed custom scraping, cleaning, and validation functions to ensure accuracy before visualization.

---

## Competition Data Module

### Motivation

While NCAA data is publicly available, we found:

- **Duplicated player records**
- **Incorrect team names**
- **Difficult-to-query official interface**

Example: The official NCAA page for Purdue vs UConn (Apr 8, 2024) showed incorrect school names and duplicated player entries. Our app **corrects these issues**, providing clean, reliable stats.

### Key Features

- Dynamic win probability chart
- Team stats comparison (rebounds, assists, shooting %, etc.)
- Player stats display w/ **flower charts** and **tables**
- Team and player logos for enhanced UI
- Interactive collapsible UI components

We initially used Plotly, but switched to **echarts4r** for smoother performance and better real‑time rendering.

### Custom Helper Functions

| Function | Purpose |
|---|---|
`wp_chart` | Build win‑probability timelines & excitement index  
`get_compe_stats` | Extract shot, score, and player behavior statistics  
`convert_game_data` | Clean box score data, split starters / bench, remove duplicates  

---

## Team & Player Data Module

### Structure

- **Team selector panel** with logos, conference filters, and search
- Detailed **team pages**:
  - Season schedules
  - Game results
  - Player stats tables
  - Assist network graphs (team‑level + player‑level)

### Methods

- Curated missing team logos
- Built interactive navigation bar
- Used `ncaahoopR::assist_network()` and customized visual layer to highlight passing dynamics
- Structured statistical summaries for both team‑ and player‑level exploration

---

## Prediction Module

We implemented a **baseline XGBoost model** to predict outcomes of **Duke vs UNC games**.

### Features Used
- Game index
- Home/away flags
- Score differences (target = home score − away score)

### Model Notes

- Train/test split: **80% / 20%**
- Objective: regression
- Key parameters: `eta=0.1`, `max_depth=3`, early stopping
- We pre‑processed data due to `ncaahoopR` parsing delays

The model outputs:

- Predicted point margin
- Predicted winner
- Rounded results for clarity

> This prediction module is a **proof‑of‑concept** — future iterations may incorporate richer features and advanced modeling.

---

##  UI / UX Design

- Unified multi‑page Shiny app
- Home page with rotating NCAA/Duke basketball images
- Navigation styled in NCAA theme colors
- Real‑time update widgets:
  - Duke countdown to next game
  - Latest Duke result
  - NCAA games today
- Responsive layout, collapsible blocks, and custom CSS

---



