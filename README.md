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

## Methodology

The project follows a structured workflow to ensure the analysis is reproducible and interpretable:

1. Data Collection:
   I downloaded the StatsBomb Open Data repository and extracted all event files for the competitions provided. From these JSON files, I filtered only the events where the shot type was a penalty.

2. Data Cleaning:
   I normalized the event structure and removed irrelevant or missing fields. I also reconstructed the scoreline before each penalty by counting goals up to that moment. Shot outcome, direction, and technique fields were standardized.

3. Feature Engineering:
   I created new variables including:
   • pressure level (Extreme, High, Medium, Low)
   • team_goals_before and opp_goals_before
   • score_diff
   • simplified shot direction (Left, Centre, Right)

4. Exploratory Data Analysis (EDA):
   I visualized the distributions of penalty outcomes, pressure levels, directions, and miss types, and explored relationships between pressure, direction, and success.

5. Hypothesis Testing:
   I applied chi-square tests to examine whether pressure influences penalty success, shot direction, or miss type.

6. Machine Learning :
   I trained logistic regression models to predict whether a penalty will be scored using the engineered features.
   
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

## Machine Learning

Three logistic regression models were evaluated to predict whether a penalty would be scored or missed. A baseline model was first trained to establish a reference point, but it was found to exploit class imbalance by predicting the majority outcome. A balanced model was then introduced to force the model to consider missed penalties. Finally, a custom-weighted model was trained to further tune the trade-off between overall accuracy and recall for missed penalties.

Model performance was evaluated using confusion matrices and recall for the minority class (misses). While overall predictive performance remained modest, the weighted model was able to identify approximately 38% of missed penalties, demonstrating that contextual features provide limited but meaningful information about penalty risk.

---

## Results Summary

Statistical analysis showed that pressure significantly affects penalty success, while shot direction and miss type remain largely unchanged under pressure. Logistic regression confirmed that contextual features alone cannot strongly predict outcomes, but can be used to identify higher-risk penalty situations.

---

## Limitations

Penalty kicks are inherently high-variance events influenced by factors not captured in the dataset, such as goalkeeper behavior, shot power, and individual player tendencies. As a result, there is a natural upper bound on predictive performance. While baseline accuracy appears high due to class imbalance, recall for missed penalties remains modest even after class weighting. This indicates that match-level contextual features provide limited but meaningful information for identifying risk, rather than enabling precise outcome prediction.

---

## Reproducibility Instructions

The cleaned dataset used in this analysis is provided as a CSV file.  
To reproduce the analysis:

1. Clone this repository.
2. Install the required Python packages listed in `requirements.txt`.
3. Open the notebook file.
4. Run all cells in order.

The raw StatsBomb event data is not included due to licensing restrictions, but the processed dataset ensures full reproducibility of the analysis.

---

## Data Attribution

This project uses publicly available football event data provided by **StatsBomb Open Data**.

Source:
- StatsBomb Open Data Repository: https://github.com/statsbomb/open-data

The original raw event data is owned by StatsBomb and made available for research and educational purposes. This repository includes only a cleaned and processed subset derived from the original data.

---

**Tulga Berke Kayhan**
