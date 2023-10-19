# MLDS400_Group5
This is the repo for documenting Group 5's process of MLDS 400's team project.

Group Members: Xiyi Lin, Omar Shatrat, Fanqi Song, Tianyu Wu

## Weekly Updates and To-Do-Lists:
### Oct 13th 2023:
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

      Besides that, we do have some doubts related to the actual meaning of **"TRANNUM"**, as we find that, there is more than one observation stored in the trnsact.csv data for the same **"TRANNUM"** number but with different sale dates and stores. From our understanding, this code should specify a serial number that is uniquely identified for each purchasing behavior, but different sale dates and stores for the same **"TRANNUM"** make us a bit confused. However, it is important to resolve our confusion as soon as possible, as this column could become important after determining the research question and setting out to clean data and conduct EDA.What 

  +**Potential Questions**
  - How does price sensitivity differ across regions, gender, and other demographics?
  - Can we forecast sales for each product category and/or each department for the coming year(s)? 
      
#### To-Do-Lists:
- Fix the giant problems in tables skuinfo.csv using the command line and/or Python and/or R, import the other three CSV files that are not uploaded into Postgres via pgAdmin, and grant Postgres access to everyone on the team.
- Brainstorm several ML questions that we might be interested in, by looking into the data provided in-depth.
- Get feedback regarding out questions. 
- Start cleaning the data (e.g. filling the null values and replacing misleading or incorrect values) and conducting EDA in a systematic way, after narrowing the discussion down to one or two specific business questions.
