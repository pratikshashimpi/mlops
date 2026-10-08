# Data Pipeline Documentation

## Overview

This project implements an automated data pipeline using DVC.

The pipeline consists of four stages:

Data Collection → Preprocessing → Feature Engineering → Data Validation

## 1. Data Collection

**Purpose:** Collect the raw Iris dataset.

**Input:** Iris dataset from scikit-learn

**Output:** `data/raw/iris_raw.csv`

The collection stage loads the Iris dataset, converts the target values into species names, adds a collection timestamp, and saves the raw data.

## 2. Data Preprocessing

**Purpose:** Clean and prepare the raw dataset.

**Input:** `data/raw/iris_raw.csv`

**Output:** `data/processed/iris_preprocessed.csv`

The preprocessing stage removes duplicate records, converts numeric columns, fills missing numeric values using the median, removes rows with missing species, and removes the collection timestamp.

## 3. Feature Engineering

**Purpose:** Create additional useful features from the cleaned data.

**Input:** `data/processed/iris_preprocessed.csv`

**Output:** `data/processed/iris_features.csv`

The feature engineering stage creates:

- `sepal_area`
- `petal_area`
- `sepal_to_petal_length_ratio`
- `petal_length_bin`

## 4. Data Validation

**Purpose:** Verify that the final dataset satisfies the required conditions.

**Input:** `data/processed/iris_features.csv`

**Output:** Validation result

The validation stage checks:

- Required columns
- Missing values
- Valid species values
- Numeric value ranges

If validation fails, the pipeline stops with an error.

## DVC Pipeline

DVC manages the stages and their dependencies.

```text
collect
   |
   v
preprocess
   |
   v
features
   |
   v
validate