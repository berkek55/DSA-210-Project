# DSA-210-Project
# Penalty Kick Outcomes – DSA210 Project

## Overview
This project looks at what affects the success of a penalty kick in football.  
Using open data from StatsBomb, I’ll analyze different factors such as the player’s foot, shot technique, and match pressure to see how they influence whether the penalty is scored or missed.

The main goals are:
- To clean and explore real football event data
- To learn and apply basic machine learning
- To create clear visualizations and insights about penalty patterns

---

## Motivation
Penalty kicks are short but high-pressure moments that often decide matches.  
They’re also simple enough to model, which makes them a great way to learn data analysis and basic ML without dealing with huge or messy datasets.  
I want to see if certain situations or techniques make scoring more likely.

---

## Data Source
I’ll use **[StatsBomb Open Data](https://github.com/statsbomb/open-data)**, which includes detailed match events for tournaments such as the FIFA World Cup and UEFA Euro.  
Each match is stored as a JSON file, listing all passes, shots, and penalties.

From these files, I’ll extract only the penalty shot events (`shot.type.name == "Penalty"`).  
Relevant fields include:
- `player.name`
- `shot.outcome.name`
- `shot.technique.name`
- `shot.body_part.name`
- `under_pressure`
- `competition_stage`
- `minute` and `match_id`

---

## Data Enrichment
To follow the project requirement of combining datasets, I’ll add extra contextual information:

1. **Psychological Pressure (Simple Version)**  
   - Create a new column based on `competition_stage`:  
     Finals and semi-finals → “High pressure”,  
     Knockouts → “Medium pressure”,  
     Group matches → “Low pressure”.

2. **Situational Pressure (Optional Enhancement)**  
   - Later in the project, if time allows, I’ll reconstruct the *scoreline at the moment of the penalty* by counting goals before the event.  
   - This will give a more realistic measure of pressure (for example, a 0–0 penalty in the 90th minute = high pressure).

3. **Player Footedness**  
   - Add a small CSV with each player’s dominant foot (Left or Right) and merge it with the main dataset.

These enrichments make the dataset more meaningful and help analyze both technical and psychological aspects of penalty success.

---


## Expected Outcome
A clear, data-driven summary of what makes a penalty more or less likely to succeed, along with visualizations and a simple predictive model.  
If time allows, I’ll also include the reconstructed in-match score to analyze how real pressure affects performance.

---
 
Tulga Berke Kayhan
