# Penalty Kick Outcomes – DSA210 Project

## Overview
This project analyzes what affects the success of a penalty kick in football using StatsBomb open event data.  
The goal is to explore which factors — such as game pressure, shot direction, and match context — influence whether a penalty is scored or missed.

The project includes:
- Data collection from StatsBomb Open Data  
- Cleaning and feature engineering  
- Exploratory data analysis (EDA)  
- Hypothesis testing  
- A machine learning model to predict penalty success  

---

## Motivation
Penalty kicks are high-pressure moments that can decide matches.  
They are also simple, well-defined events, making them a great setting to learn data analysis and machine learning without dealing with messy or overly large datasets.

The project aims to understand:
- How pressure affects performance  
- Whether players change their decisions in stressful situations  
- What features matter most for predicting success  

---

## Data Source
The dataset comes from **StatsBomb Open Data**, which provides structured JSON event files for major football competitions including the FIFA World Cup and UEFA Euro tournaments.

Repository link:  
https://github.com/statsbomb/open-data

From the event files, I extracted all **penalty shot events** (`shot.type.name == "Penalty"`), along with contextual information such as:
- player name  
- team name  
- shot outcome  
- shot technique  
- minute of the match  
- event location  
- match ID  

---

## Data Enrichment
To meet the project requirement of combining datasets and to improve the predictive model, I engineered several new features:

### **1. Reconstructed Scoreline**
For every penalty, I counted how many goals each team had scored up to that exact moment:
- `team_goals_before`  
- `opp_goals_before`  
- `score_diff`  

This captures game context more realistically.

### **2. Pressure Classification**
Using minute + score difference + late-game conditions, I created a custom pressure feature:
- **Extreme:** shootouts or minute ≥ 120, or late close games  
- **High:** second-half close games  
- **Medium:** early close games or moderate margins  
- **Low:** early or low-stress situations  

This pressure metric was validated using hypothesis testing.

### **3. Shot Direction Simplification**
Using the shot's end location (y-coordinate), I categorized penalties into:
- Left  
- Centre  
- Right  

based on equal 1/3 goal-width bins.

---

## Exploratory Data Analysis
I explored:
- penalty success distributions  
- direction frequencies  
- pressure level distributions  
- how direction and pressure interact  
- how miss types are distributed  

Visualizations were created to show patterns in the data.

---

## Hypothesis Testing
I ran three chi-square tests:

1. **Pressure → Penalty Success**  
   ✔ *Significant* — pressure affects scoring rate.

2. **Pressure → Shot Direction**  
   ✖ *Not significant* — players keep their usual direction under pressure.

3. **Pressure → Miss Type** (saved / off target / post)  
   ✖ *Not significant* — pressure changes success, not the type of mistake.

These results show that pressure affects **execution**, not **decision-making**, which fits well with football psychology.

---

## Machine Learning (Next Step)
The next part of the project is to build a **logistic regression model** to predict whether a penalty will be scored based on features like:
- pressure  
- minute  
- score difference  
- direction  
- shot technique  
- competition  

The goal is to produce a simple, interpretable model and examine which features have the strongest influence.

---

##Reproducibility Instructions

To reproduce this analysis:
	1.	Download the StatsBomb Open Data repository from: https://github.com/statsbomb/open-data
	2.	Make sure the events folder is available in your working directory, or update the file paths in the notebook based on where you store the data.
	3.	Install the required Python packages listed in requirements.txt
	4.	Open the penalty_analysis.ipynb notebook.
	5.	Run all cells in order. This will recreate the data loading, feature engineering, EDA, hypothesis tests, and machine learning steps used in this project.


---

**Tulga Berke Kayhan**
