# As of Nov 17th, 2023:
## Updates:
* We started to create visualizations, conduct data enginnering, and evaluate models that we used to answer our proposed ML question: ***Leveraging historical sales data, can we identify the most promising locations for new store openings based on a holistic evaluation, encompassing city demographics and the performance of existing stores?***

**Visualization**

Draw visualizing and understanding the distribution of the predictor variable 'success' and exploring relationships between the selected features.

- Visualization 1: Distribution of Success - Displaying the distribution of the 'success' variable provides a clear visual representation of the count of each 'success' category (0 or 1).
- Visualization 2: Correlation Matrix - Heatmap representing the correlation matrix of features to help identify patterns and relationships between different features.
- Visualization 3: Pairplot for Selected Features - Focusing on features 'InventoryTurnover,' 'GrossProfit,' 'ReturnPercentage_y,' and 'success’ to understanding the distribution of individual features and potential patterns between 'success' categories. 

**Data Engineering**

- Create Interaction Feature: A new feature, 'Interaction1,' is created by multiplying the 'InventoryTurnover' and 'GrossProfit' columns.
- Handle Missing Data: Missing values in the 'df2' DataFrame are filled with the mean values of their respective columns.
- Standardize Numerical Features: The numerical features are standardized. Standardization transforms the features to have a mean of 0 and a standard deviation of 1, making them comparable and suitable for certain machine learning algorithms.

**Model Evaluation**

- Since the data is imbalanced,  we used the SMOTE method to reduce the impact of class imbalance on model performance. 
- Logit Regression Model with Resampled Data: 
Trained on the resampled data (balanced using SMOTE) and we generated the model’s summary with the statistical information displayed. The model is evaluated on the original test set, and accuracy, confusion matrix, and classification report are printed.
- Logistic Regression with Hyperparameter Tuning:
A logistic regression model is created using a pipeline that includes standardization of features and logistic regression. Hyperparameter tuning is performed using grid search with cross-validation and the tuned logistic regression model is evaluated on the original test set.
- Random Forest Classifier:
A random forest classifier model is created using a pipeline with standardization and a random forest model. Hyperparameter tuning is performed and the tuned random forest model is evaluated on the original test set.

## To-Do-Lists:
- Engage in a thorough discussion of the model's limitations with teammates, to ensure comprehensive improvement and re-select the features if necessary
- Initiate the creation of presentation slides, conduct ROI analysis, and compile the final report

