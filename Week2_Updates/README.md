# As of Oct 20th 2023:
## Updates:
* Completed the successful import of the remaining three datasets into the PostgreSQL database via the PgAdmin4 interface, ensuring that all team members now have unrestricted access to the PostgreSQL resources.
* Commenced the data cleaning process for the 'skuinfo' table, an operation that has unearthed several noteworthy challenges:
    + Encountered unquoted string entries within columns such as 'color,' which may contain embedded commas, potentially leading to unexpected additional columns during data manipulation.
    + Observed intricacies in columns like 'style,' 'size,' 'packsize,' and others, which make their classification as categorical variables for machine learning purposes a complex task, necessitating a meticulous and time-consuming data cleansing process. This, in turn, raises questions about the feasibility of drawing substantial insights from these columns.

* Presented a set of meticulously formulated machine learning inquiries, refined through an in-depth exploration of the entire CSV dataset:
  + How does consumer price sensitivity vary across distinct geographic regions, demographics, and other relevant factors?
  + Is it possible to develop accurate sales forecasts for each product category or department over the next year or beyond?
  + Can we build a predictive model to determine the optimal discount rates for specific products to maximize profitability? Alternatively, can we develop a model that categorizes products into more desirable or less desirable segments, enabling us to optimize pricing and sales strategies accordingly?
  + Leveraging historical sales data, can we identify the most promising locations for new store openings based on a holistic evaluation, encompassing city demographics and the performance of existing stores?
  + Addressing the challenge of dynamic pricing, can we create optimal pricing strategies taking into account region-specific considerations (derived from 'STRINFO'), temporal trends (in response to significant economic events), and product-level or category-level attributes (informed by 'SKUINFO' and 'DEPTINFO' datasets)? The aim is to maximize sales through sophisticated price recommendations.

      
## To-Do-Lists:
- Seek input and feedback from both the Teaching Assistant (TA) and the instructor regarding the proposed machine-learning questions. Additionally, conduct comprehensive research to understand how similar challenges are addressed in the industry.
- Upon validating the machine learning questions, continue with the data cleansing and Exploratory Data Analysis (EDA) processes, adhering to the determined research direction.

