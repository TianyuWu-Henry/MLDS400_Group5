# MLDS400_Group5
This is the repo for documenting Group 5's process of MLDS 400's team project. In this project, we are going to identify **promising location(s)** for Dillard’s next local store by leveraging sales data and consulting-backed estimation.

Group Members: Xiyi Lin, Omar Shatrat, Fanqi Song, Tianyu Wu

## Weekly Updates and To-Do-Lists:
### Oct 13th, 2023:
#### Updates:
* Used pgcli/psql to connect to the MLDS’s Postgres DB server, downloaded pgAdmin, and made a test to import two CSV files (deptinfo and strinfo) into the database via pgAdmin successfully.
* Got a general feeling of the five CSV files by looking into the schema description and starting to analyze them in R.
    + **deptinfo.csv and strinfo.csv Exploration**
      
      The deptinfo.csv file does not appear to have much meaningful information except that it notes some of the dedicated account teams that operate within Dillards. For now, it suffices to say that the department info data frame consists of 60 rows and 2 columns.

      The strinfo.csv file shows detailed information about each store, including the store number, city where the store is located, state where the store is located, and the corresponding zip code. In this dataset, we see much more interesting insights. The R Markdown tables in our main folder show us the frequency of each city, state, and zip code. Little Rock, AK has the largest number of stores with 15, and zip code 72201 has the most number of stores with 14. A bar chart also shows us that Texas is by far the most populous state in terms of store frequency.
 
    + **skuinfo.csv Exploration**
 
      This dataset describes each stock item’s details, including the department the stock item belongs to, stock item classification, universal product code, color, size, quantity of item per pack, vendor number, and brand name, but it is a little bit messy, and we need to start thinking about how to clean it in a systematic way after determining our business question. Here are several points that we are going to be attentive to:
        - The DEPT (e.g. 800,801,1100) and CLASSID (e.g. 5305,4505) columns' meanings are ambiguous, and the third column has varying lengths, making the interpretation more complicated. 
        - For the STYLE column, the input is unformatted, since there are some spaces in-between letters or the lengths of them are different. The inputs are hard to interpret without standardization and do not follow any regulated style.
        - For the COLOR column, some inputs are correct with clear color stated, while other inputs mix spaces, letters, and numbers together to confuse. 
        - For the SIZE column, there is also no standardized chart to format (e.g. XS/S/M/L) but more like ‘090M’ and ‘ALL’, which are confusing. 
          
    + **skstinfo.csv Exploration**
      
      This dataset is the second largest one, which includes 39,230,145 observations with 4 effective columns (SKU, STORE, COST, RETAIL), which clearly show the unit number of stock items for each store, corresponding cost, and retail price of the stock item.

      - SKU data reveals that there is a wide range of products represented. With SKUs ranging from 3 to 10 million, this suggests a diverse product catalog.
      - The store data provided information about where these products are sold, with store IDs ranging from 100 to 9909, which implies that the products are distributed across a large number of stores.
      - The cost data shows the cost associated with each SKU. The minimum cost is \$0, indicating that some products do not have cost, while the maximum cost is \$2700.00, which suggests a significant cost  variation among the products.
      - The actual price data reveals the prices at which these products are sold to customers. The minimum retail price is \$0.00, indicating the possibility of free products, while the maximum retail price is \$6,017.00, showing a broad range of price points.

      But there is also a concern, dealing with the null values commonly appearing in the cost and price columns, where we probably could make use of the trnsact.csv data to systematically replace the NA values (discussed in the next paragraph).


    + **trnsact.csv Exploration**
      
      Since we have not imported this largest CSV file (~11.37 GB) into the database via pgadmin4, we head to import the first 100,000 observations in R to get a general feeling of this dataset. There are 13 effective columns of information except the one specified with the "Unknown" column. We found out that the column **"AMT"** is derived from the multiplication of **"QUANTITY"** and **"SPRICE"**, and as mentioned in the previous paragraph, the null values in the **"SPRICE"** and **"ORGPRICE"** columns can be filled according to the values stored in the skstinfo.csv file, and vice versa.

      Besides that, we do have some doubts related to the actual meaning of **"TRANNUM"**, as we find that, there is more than one observation stored in the trnsact.csv data for the same **"TRANNUM"** number but with different sale dates and stores. From our understanding, this code should specify a serial number that is uniquely identified for each purchasing behavior, but different sale dates and stores for the same **"TRANNUM"** make us a bit confused. However, it is important to resolve our confusion as soon as possible, as this column could become important after determining the research question and setting out to clean data and conduct EDA.
      
#### To-Do-Lists:
- Fix the giant problems in tables skuinfo.csv using the command line and/or Python and/or R, import the other three CSV files that are not uploaded into Postgres via pgAdmin, and grant Postgres access to everyone on the team.
- Brainstorm several ML questions that we might be interested in, by looking into the data provided in-depth.

### Oct 20th, 2023:
#### Updates:
* Completed the successful import of the remaining three datasets into the PostgreSQL database via the PgAdmin4 interface, ensuring that all team members now have unrestricted access to the PostgreSQL resources.
* Commenced the data cleaning process for the 'skuinfo' table, an operation that has unearthed several noteworthy challenges:
    + Encountered unquoted string entries within columns such as 'color,' which may contain embedded commas, potentially leading to unexpected additional columns during data manipulation.
    + Observed intricacies in columns like 'style,' 'size,' 'packsize,' and others, which make their classification as categorical variables for machine learning purposes a complex task, necessitating a meticulous and time-consuming data cleansing process. This, in turn, raises questions about the feasibility of drawing substantial insights from these columns.

* Presented a set of meticulously formulated machine learning inquiries, refined through an in-depth exploration of the entire CSV dataset:
  + How does consumer price sensitivity vary across distinct geographic regions, demographics, and other relevant factors?
  + Is it possible to develop accurate sales forecasts for each product category or department over the next year or beyond?
  + Can we build a predictive model to determine the optimal discount rates for specific products to maximize profitability? Alternatively, can we develop a model that categorizes products into more desirable or less desirable segments, enabling us to optimize pricing and sales strategies accordingly?
  + Leveraging historical sales data, can we identify the most promising locations for new store openings based on a holistic evaluation, encompassing city demographics and the performance of existing stores?
  + Can we develop a predictive model that accurately forecasts the likelihood of a future return for a specific transaction, based on historical transaction attributes and patterns? 
  + Addressing the challenge of dynamic pricing, can we create optimal pricing strategies taking into account region-specific considerations (derived from 'STRINFO'), temporal trends (in response to significant economic events), and product-level or category-level attributes (informed by 'SKUINFO' and 'DEPTINFO' datasets)? The aim is to maximize sales through sophisticated price recommendations.


#### To-Do-Lists:
- Seek input and feedback from both the Teaching Assistant (TA) and the instructor regarding the proposed machine-learning questions. Additionally, conduct comprehensive research to understand how similar challenges are addressed in the industry.
- Upon validating the machine learning questions, continue with the data cleansing and Exploratory Data Analysis (EDA) processes, adhering to the determined research direction.


### Oct 27th, 2023:
#### Updates:
* Continued with the data cleansing process and Exploratory Data Analysis (EDA) processes using Python. The reason why we change our mind to use Python for data cleansing and EDA rather than R is because we learned how to connect Python with SQL servers during the MLDS422 class, and find it more convenient and intuitive to speed up our EDA process!
  
a. EDA for **deptinfo and strinfo**
    
Distribution of Stores: Texas, Florida, Arkansas, Arizona, and Ohio stand out as the top five states boasting the largest number of stores. Texas and Florida, in particular, play a significant role in this retail landscape due to their substantial store presence. This phenomenon can be attributed to the high population density and robust economic activities within these states. The most store-concentrated cities are Little Rock, Gilbert, Olathe, San Antonio, and Houston. These urban hubs likely experience this retail density owing to factors such as heightened consumer demand, thriving business opportunities, or well-thought-out strategic planning.
      
Cost and Retail Price Analysis: An analysis of summary statistics reveals that the majority of products within the dataset are characterized by relatively low costs and retail prices. Both the mean and median values for cost and retail prices fall within moderate ranges, indicating a well-balanced distribution.

The presence of high-cost and high-retail price outliers suggests the existence of certain products that deviate significantly from the average. These outliers may represent premium or luxury items. Notably, the strong positive correlation (0.896) between cost and retail prices suggests that, in general, as the cost of a product increases, the retail price also increases. This positive relationship holds valuable insights for businesses when setting their pricing strategies.

Profit Margin Insights: The profit margin, which represents the difference between retail price and cost, is a vital metric for businesses. It is calculated as (Retail Price - Cost) / Cost. We've identified the top five states with the highest profit margins: Arkansas, Oklahoma, Ohio, Texas, and Tennessee. These states not only host a significant number of stores but also maintain favorable profit margins. This observation indicates efficient cost management and effective pricing strategies in place.
    
b. EDA for **skuinfo**
    
At first glance, the columns within this CSV file may appear disorganized, lacking apparent patterns. Initially, we considered dismissing it from our analysis. However, upon conducting exploratory data analysis (EDA), we discovered the potential usefulness of certain columns, particularly COLOR and SIZE, in scenarios where machine learning questions involve the analysis of these attributes. The UPC column, though unique, serves a purpose redundant to that of SKU, the primary key of this table, and thus holds no value for our analysis. As for other columns like STYLE, VENDOR, and BRAND, while histogram plots reveal some patterns, their inclusion in the analysis warrants a more cautious approach, given the limited information available regarding the specific entries they represent.

Furthermore, the possibility of merging skuinfo and deptinfo into a single dataframe based on the common SKU primary key is feasible. However, we've chosen to defer this decision due to the uncertainty surrounding the machine learning questions that we will finalize by the end of the next week.

c. EDA for **trnsact**

The "trnsact" table is the most data-rich among the five tables in our dataset, and as such, we need to exercise caution when considering its attributes. Our initial step was to conduct a correlation analysis, revealing that the majority of its columns exhibit low correlations. An exception to this pattern is the price-related data, which includes variables such as "AMT," "salesPrice," and "originalPrice." This observation aligns with our expectations, as we would naturally anticipate a high correlation between "AMT" and the pricing variables.

Furthermore, the low correlation values across most other variables indicate that there are no significant relationships among them. This finding has a valuable implication: it minimizes the risk of multicollinearity, a phenomenon that could adversely affect any potential regression analyses we may consider in the future. In essence, our data exploration has laid a solid foundation for subsequent analytical endeavors.

* Conduct preliminary research to understand how our proposed ML questions are related to some business/academic challenges that have been dealt with so far. Below are two pieces of literature that could be useful to rethink about our ML questions:

1. [Retail Pricing and Clearance Sales](https://www.nber.org/papers/w1446)
2. [US aggregate demand for clothing and shoes: effects of non-durable expenditures, price and demographic changes](https://onlinelibrary.wiley.com/doi/full/10.1046/j.1470-6431.2003.00291.x)

#### To-Do-Lists:
- Given the demanding schedule this week, regrettably, we were unable to secure feedback from the Teaching Assistant (TA) regarding the proposed machine-learning questions. As a result, our plan is to coordinate a comprehensive meeting with the TA and our entire team next week. During this meeting, we aim to delve into the questions in detail, fostering a deeper understanding and alignment.
- Moving forward, we will speed up the EDA of the "trnsact" dataset. Subsequently, we will embark on the crucial task of feature engineering. This process will be driven by our refined machine-learning questions, which are now honed to address specific targets.


### Nov 3rd, 2023:
#### Updates:
* After two weeks of EDA, we agreed to start with deciding on an ML question to further narrow down this project scope, that is, can we develop a predictive model that accurately forecasts the likelihood of a future return for a specific transaction, based on historical transaction attributes and patterns? The reason why we chose this question is that we think from the client's shoes to help identify the pain points, as well as combine the data availability after certain levels of EDA.
* Continued with the EDA processes using Python, specifically finishing the trnsact data and trying to explore the relationship (merge if necessary) between different datasets, especially after we decided on our ML question as illustrated above.

a. Extended EDA for **trnsact**

We are keenly focused on conducting an extensive EDA for the trnsact dataset. Our primary objective is to gain a comprehensive understanding of the data, with a particular emphasis on the column that delineates purchases and returns. By delving into this column, we aim to extract valuable insights and patterns that will inform our decision-making and further our understanding of customer behavior and business performance. By the end of each analysis, we plot the Number of Different SKUs Sold Over Time, the Number of Different Products Sold Over Time, the Number of Purchases and Returns Over Time, as well as the total revenue change over time, which better demonstrates and decouples our research question. In the meanwhile, we are also curious about the amount of AMT and ORGPRICE, with two plots generated for better visualization.

b. Extended EDA for merging **trnsact and strinfo**

We've noticed an interesting trend in the sales data – there's a significant spike in sales every December, likely due to the holiday season, including Thanksgiving and holiday festivities. However, this increase is consistently followed by a decline in January. This pattern indicates that people tend to spend more during the holidays, and sales tend to drop once the holiday excitement subsides. When we looked at the top 10 states, we found that they all exhibit this same pattern of a sharp rise in December sales, followed by a dip in January. This common trend suggests that people in these states tend to splurge during the holidays, and sales slow down in the month that follows. Understanding these regional sales patterns and the influence of seasonal factors can help businesses fine-tune their strategies and inventory management to maximize sales during peak times and adapt during slower months.

#### To-Do-Lists:
- Discuss the result with the Teaching Assistant (TA) regarding our approach to solving the chosen machine-learning question (The question is still subject to change if feedback is not desirable enough).
- Conduct an extensive review of the existing literature further to elevate the sophistication and depth of our proposed machine learning question, and we will deepen it according to the literature if necessary.

### Nov 10th, 2023:
#### Updates:
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

#### To-Do-Lists:
- Develop a pipeline to build KPIs for all the cleaned data as much as possible
- Train model, tune parameters, and cross-validate
- Start to prepare presentation slides, ROI analysis, and final report


### Nov 17th, 2023:
#### Updates:
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

#### To-Do-Lists:
- Engage in a thorough discussion of the model's limitations with teammates, to ensure comprehensive improvement and re-select the features if necessary
- Initiate the creation of presentation slides, conduct ROI analysis, and compile the final report


### Nov 24th, 2023:
#### Updates:
- This week, our team delved into an in-depth discussion regarding the limitations of our model. We engaged in comprehensive brainstorming sessions to identify potential areas for improvement. Evaluating the current feature set, we're considering reselecting features to enhance the model's performance. Collaborative efforts have been fruitful in shedding light on aspects that could significantly impact the model's accuracy and robustness.
- We enhanced our dataset by incorporating latitude and longitude as new features, providing valuable spatial context to our machine learning model. To visualize success rates, we created an interactive map using the folium library, effectively illustrating the geographical distribution of successful and unsuccessful stores.
- Beyond our initial models, such as Logistic Regression, we explored K-Nearest Neighbors (KNN) and decision trees, visualizing the decision-making processes within the tree structures. Our model evaluation employed various metrics, including confusion matrices and classification reports, offering insights into the models' classification performance.
- We also visualized decision regions using Principal Component Analysis (PCA) to understand how models classified different feature space regions.  
- We initiated the creation of presentation slides intended to encapsulate our project's journey, methodology, and findings. This involved meticulous structuring to effectively communicate our approach and results.
  

#### To-Do-Lists:
- We planned to conduct a detailed ROI (Return on Investment) analysis to showcase the tangible benefits and value derived from our model's implementation. This analysis will be pivotal in illustrating the project's potential impact and justifying its relevance.
- In alignment with the presentation, we will start to compile the final report. This report will encapsulate the entire project lifecycle, encompassing methodologies, data sources, model development, and validation. Each team member is actively contributing to ensure the report reflects the depth of our work, outlining key insights, challenges faced, and recommendations for future enhancements.

### Dec 1st, 2023:
#### Updates:
- This week marked significant strides in our project's culmination. We successfully wrapped up all essential elements and began the compilation of our final report. Collaborating closely, our team has diligently contributed to the content, seamlessly integrating various facets of our work. For easy access and seamless collaboration, the document is located [here](https://docs.google.com/document/d/1sO2yizNWc-F51eoD9gPide3BTS78NSWetNMMY3FJ-qk/edit?usp=sharing).

- Moreover, we've achieved a critical milestone by finalizing the ROI Analysis, a pivotal component underscoring the project's success. Building upon these findings, we've now embarked on the slide preparation phase, streamlining our insights for an impactful presentation.

#### To-Do-Lists:
- Our primary focus will remain on meticulously finalizing all elements. Ensuring the readiness of each component is paramount as we gear up for submission. This phase demands attention to detail and precision to guarantee a comprehensive and polished project outcome.
  
### Dec 8th, 2023:
#### Updates:

As we approach the final submission deadline, our team's efforts have been dedicated to meticulous refinement and last-minute polishing. The past week has been characterized by a comprehensive review of all project components. We've diligently ensured the report's completeness, accuracy, and coherence.

The presentation underwent final adjustments, focusing on concise yet impactful delivery of our project's key highlights. Each slide was meticulously crafted to effectively communicate our achievements and insights.

With the submission deadline imminent, collaborative efforts persisted to ensure alignment and coherence between the report and presentation. Our team worked closely to address any remaining gaps and guarantee a seamless final submission.

Our collective endeavor throughout this project has been marked by dedication, collaboration, and a commitment to excellence. As we approach the conclusion, we stand proud of our accomplishments and the comprehensive nature of our project outcome.
