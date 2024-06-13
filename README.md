# Bosch-production-line-performance
## Project Overview
This project leverages advanced machine learning techniques to predict internal failures in Bosch's production lines. By analyzing measurements and tests conducted on thousands of parts, the project aims to enhance the quality control processes and reduce manufacturing costs. The dataset, sourced from a Kaggle competition, presents a challenging problem due to its large number of anonymized features and highly imbalanced nature. Various classification algorithms are tested to determine the most effective method for predicting failures and insights into the production process.

## Dataset
The dataset used in this project is sourced from the Kaggle competition "[Bosch Production Line Performance](https://www.kaggle.com/competitions/bosch-production-line-performance/data)." It contains measurements of parts as they move through Bosch's production lines. Each part has a unique Id, and the goal is to predict the 'Response' (1 if the part fails quality control, 0 otherwise). The dataset includes numerical, categorical, and date features.

## Methodology
### 1. Handle Missing Values
Any missing values are addressed to ensure dataset completeness and prevent issues during subsequent steps. Numeric, categorical, and date data are processed in chunks to handle missing values without overloading memory. Columns are identified and dropped if they have more than 40% missing values, and the remaining missing values are filled with zero, which is suitable given the context of the Bosch dataset as a missing value might imply that a particular measurement wasn't taken, which can logically be represented by zero. Each chunk is processed separately, with identified columns dropped and missing values handled, then the processed chunks are progressively combined by merging them using the Id column to ensure only complete data points are included with an inner join.

### 2. Balancing the Classes 
After merging the processed dataframes, the classes are balanced by downsampling the majority class to match the minority class size, ensuring no bias towards the majority class. This process involves handling numeric data in chunks to avoid memory overload, separating the data by class, downsampling the majority class, combining, and shuffling the balanced classes. The final balanced and shuffled dataset is saved to a new CSV file, and the chunks are combined into a single DataFrame. 

### 3. Apply PCA
After balancing the classes, categorical variables causing issues with the StandardScaler in PCA are converted to dummy variables using one-hot encoding. With the dataset cleaned, missing values handled, and data balanced, PCA is applied for dimensionality reduction. The features are standardized, and PCA is used to reduce the number of features while retaining most of the variance, ensuring PCA captures the variability in the balanced dataset.

### 4. Data Splitting and Model Training
The balanced and PCA-transformed dataset is split into training and testing sets. Initial model selection involves implementing Logistic Regression, Decision Tree, SVM, Random Forest, and Gradient Boosting, and using cross-validation to evaluate their performance. Models are compared based on 5-fold cross-validation results, with SVM and Random Forest showing the best performance, especially in terms of accuracy scores. These two models undergo hyperparameter tuning using Grid Search or Randomized Search to optimize their performance. The best parameters for SVM are {'C': 1, 'gamma': 'scale', 'kernel': 'rbf'} with a cross-validation score of 0.5977. The final models are trained using the entire training dataset with the best hyperparameters, and their performance is evaluated on the hold-out set using metrics like Accuracy, Precision, Recall, F1-Score, and ROC-AUC. To ensure efficient evaluation, the test set is sampled down to 20% of the training dataset size, approximately 2,752 data points.

## Results


## Prerequisites

## Installation
1. Clone the repository:
```sh
   git clone https://github.com/Varyania/Bosch-production-line-performance.git
   cd Bosch-production-line-performance

2. Install the required packages:
```sh
pip install -r requirements.txt
