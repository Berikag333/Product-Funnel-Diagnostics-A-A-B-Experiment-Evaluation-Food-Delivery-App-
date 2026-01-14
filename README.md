# Product-Funnel-Diagnostics-A-A-B-Experiment-Evaluation-Food-Delivery-App-
Analyse in-app event logs to diagnose funnel drop-offs and evaluate a font-change A/A/B experiment using statistical testing with multiple-comparison control.

## Overview
This project analyses user event logs for a food retail mobile app to (1) diagnose the conversion funnel and identify where users drop off, and (2) evaluate an A/A/B experiment where a new font design is tested against two control groups.

The outcome is a data-driven recommendation on whether the design change impacts user behaviour.

## Data
File:
- logs_exp_us.csv

Fields:
- EventName: event name
- DeviceIDHash: unique user id
- EventTimestamp: event timestamp
- ExpId: experiment group (246, 247 = control; 248 = variant)

## Key Questions
- Funnel: which steps users complete, conversion between steps, and main drop-off points
- Experiment: are control groups comparable (A/A), and does the font change affect user behaviour (A/A/B)?

## Workflow
1) Data prep: rename columns, convert timestamps, create datetime and date fields  
2) Data validation: events/users counts, time coverage, remove incomplete early period, confirm all groups present  
3) Funnel analysis:
   - event frequency and unique users per event
   - define funnel sequence and compute step-to-step conversion
   - identify the largest drop-off and end-to-end conversion to payment
4) A/A/B evaluation:
   - compare control groups (246 vs 247) for each event
   - compare variant (248) vs each control and vs combined controls
   - set alpha and adjust for multiple tests (e.g., Bonferroni/Šidák)

## Deliverables
- Funnel table + conversion rates
- Charts: event frequency and funnel drop-off
- Statistical test results (A/A and A/A/B) with interpretation
- Final recommendation on the font change

## Objective
Analyse event log data for a food retail app to:
1) understand the user funnel and identify where users drop off, and
2) evaluate an A/A/B experiment testing a font change to determine whether it affects user behaviour.

## 1) Data Preparation
Load the dataset, rename columns for convenience, convert timestamps to datetime, and create:
- a datetime column
- a separate date column

## 2) Data Quality & Coverage Checks
- Total events and total users
- Average events per user
- Time range (min/max timestamps) and event distribution over time
- Identify the point where data becomes stable/complete and exclude earlier data
- Confirm users exist in all experimental groups (246, 247, 248)

## 3) Funnel Analysis
### 3.1 Event landscape
- List events and their frequency
- Compute unique users per event and the share of users performing each event

### 3.2 Funnel construction
Define the funnel sequence (excluding events not part of the core purchase path if needed) and compute:
- step-to-step conversion rates
- the stage with the largest drop-off
- end-to-end conversion to payment

## 4) A/A/B Experiment Evaluation
### 4.1 A/A sanity check (246 vs 247)
Test whether control groups behave similarly across key events.

### 4.2 Variant effect (248 vs controls)
For each event:
- compare 248 vs 246
- compare 248 vs 247
- compare 248 vs combined controls

## 5) Statistical Testing Framework
- Define H0/H1 for each comparison (no difference vs difference)
- Set alpha and adjust for multiple comparisons (number of tests performed)
- Interpret p-values in product/business terms

## Conclusions
Summarise funnel bottlenecks and provide a recommendation on whether the font change should be shipped, based on experiment results and statistical evidence.

## Tech
Python, pandas, matplotlib/plotly, scipy.stats, Jupyter Notebook

## Author
**Erika González**  
MBA | Marketing & Data Analytics  
Focus areas: Product Analytics, Experimentation, Funnel Optimisation
