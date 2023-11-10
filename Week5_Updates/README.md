# As of Nov 10th, 2023:
## Updates:
* After careful consideration and in response to evolving project insights, we have strategically opted to refine our focus for this project, that is, to change our ML question to:

  ***Leveraging historical sales data, can we identify the most promising locations for new store openings based on a holistic evaluation, encompassing city demographics and the performance of existing stores?***

  The reasons are as follows:
  1. **Business Relevance**: Compared to the traditional directly-specified ML question, this question could directly address a practical and common business problem faced by DILLARDS, which could significantly impact the overall success and profitability of the business.
  2. **Data Availability**: We will mainly rely on skstinfo, strinfo, and trnsact datasets to conduct analyses and therefore build predictive models by selecting relevant rows and trying to do some merges.
  3. **Applications of Class Knowledge**: This task involves predictive modeling, a key aspect of what we have learned over this quarter. By developing models (logistic regression) to predict the potential success of new store locations, we could showcase our ability to apply machine learning techniques to real-world business challenges.
  4. **Measurable Success**: The success of the project can be measured in a tangible and business-oriented manner. Data in the project ranges from 2004 to 2005, and we aim to use those data to predict future openings. But since now we have been in the year 2023, we could observe the new openings for sure by some public open data, for feasible and measurable validation. 

* EDA for **merged data**

We merged trnsact, deptinfo, and strinfo into one data frame, and then we did data cleaning, including handling null values and duplicates. The 'SALEDATE' column was transformed into a DateTime format, and additional date-related features were created. To prepare categorical variables for the machine learning model, label encoding was applied to 'CITY' and 'STATE,' as these columns contain location information. We employed one-hot encoding to the 'STYPE' column ensuring that the model can appropriately interpret and learn from this information.

After the preprocessing steps, visualizations were generated to gain insights into the dataset. Histograms and scatter plots were utilized to understand the distribution of retail prices and explore the relationship between cost and retail prices. The bar charts visualized average retail prices and total sales amounts by city and store, providing a clear representation of these key metrics. Additionally, a correlation plot was created to identify potential relationships between different variables.

We also developed codes to calculate important KPIs given the data we have, namely:
- Inventory Turnover
- Gross Profit
- Return %

For each store, we define a successful company as one that is above the 50th percentile in Inventory Turnover and Gross Profit while having a return percentage below 5% Using a threshold approach. Using these benchmarks, we can classify each store as successful or not and develop a logistic regression model to assist with our classification problem. 

![image](https://github.com/TianyuWu-Henry/MLDS400_Group5/assets/49295640/90054de9-d33b-4b19-938b-5a36fff314c2)

This approach is now only applied to a subset of the sample data, our final dataframe ought to contain more samples (rows) in order to better train our predictive model.

## To-Do-Lists:
- Develop a pipeline to build KPIs for all the cleaned data as much as possible
- Train model, tune parameters, and cross-validate
- Start to prepare presentation slides, ROI analysis, and final report
