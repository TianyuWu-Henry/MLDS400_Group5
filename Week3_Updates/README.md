
# As of Oct 27th, 2023:
## Updates:
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

## To-Do-Lists:
- Given the demanding schedule this week, regrettably, we were unable to secure feedback from the Teaching Assistant (TA) regarding the proposed machine-learning questions. As a result, our plan is to coordinate a comprehensive meeting with the TA and our entire team next week. During this meeting, we aim to delve into the questions in detail, fostering a deeper understanding and alignment.
- Moving forward, we will speed up the EDA of the "trnsact" dataset. Subsequently, we will embark on the crucial task of feature engineering. This process will be driven by our refined machine-learning questions, which are now honed to address specific targets. 
