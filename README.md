# Bosch-production-line-performance
## Project Overview
This project leverages advanced machine learning techniques to predict internal failures in Bosch's production lines. By analyzing measurements and tests conducted on thousands of parts, the project aims to enhance the quality control processes and reduce manufacturing costs. The dataset, sourced from a Kaggle competition, presents a challenging problem due to its large number of anonymized features and highly imbalanced nature. Various classification algorithms are tested to determine the most effective method for predicting failures and insights into the production process.

## Dataset
The dataset used in this project is sourced from the Kaggle competition "[Bosch Production Line Performance](https://www.kaggle.com/competitions/bosch-production-line-performance/data)." It contains measurements of parts as they move through Bosch's production lines. Each part has a unique Id, and the goal is to predict the 'Response' (1 if the part fails quality control, 0 otherwise). The dataset includes numerical, categorical, and date features.

## Methodology
### 1. Handle Missing Values
Any missing values are addressed to ensure dataset completeness and prevent issues during subsequent steps. Numeric, categorical, and date data are processed in chunks to handle missing values without overloading memory. Columns are identified and dropped if they have more than 40% missing values, and the remaining missing values are filled with zero, which is suitable given the context of the Bosch dataset as a missing value might imply that a particular measurement wasn't taken, which can logically be represented by zero. Each chunk is processed separately, with identified columns dropped and missing values handled, then the processed chunks are progressively combined by merging them using the Id column to ensure only complete data points are included with an inner join.
