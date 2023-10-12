# MLDS400_Group5
This is the repo for recording Group 5's process of MLDS 400's team project.

Group Members: Xiyi Lin, Omar Shatrat, Fanqi Song, Tianyu Wu

## Weekly Updates and To-Do-Lists:
### Oct 13th 2023:
#### Updates:
* Used pgcli/psql to connect to the MLDS’s Postgres DB server, downloaded pgAdmin, and imported two CSV files (deptinfo and strinfo) into the database via pgAdmin.
* Got a general feeling of the five CSV files by looking into the schema and starting to analyze them in R.
    + **deptinfo.csv and strinfo.csv Exploration**
 
    + **skuinfo.csv Exploration**
        DATA NEEDED TO BE CLEANED:
        - There is no specific title attached to each column.
        - The DEPT(e.g 800,801,1100) and CLASSID (e.g 5305,4505) columns are ambiguous because it is hard to figure out which they belong to. Also, the third column has varying lengths, making the interpretation more complex. 
        - For the STYLE column, the input is unformatted, since there are some spaces in-between letters or the lengths of them are different. The inputs are hard to interpret without standardization and do not follow any regulated style.
        - For the COLOR column, some inputs are correct with clear color stated, while other inputs mix spaces, letters, and numbers together to confuse. 
        - For the SIZE column, there is also no standardized chart to format (e.g XS/S/M/L) but more like ‘090M’ and ‘ALL’ which are confusing. 
        - We drop the last meaningless undefined column (with entries 0 and 1) when reading the data. 
    + **skstinfo.csv Exploration**
      
      There is an extra column that is unknown or not in the DB schema given. There are 39,230,145 observations with 5 columns (SKU, STORE, COST, RETAIL, UNKNOWN)

      - SKU data reveals that there is a wide range of products represented. With SKUs ranging from 3 to 10 million, this suggests a diverse product catalog.
      - The store data provided information about where these products are sold, with store IDs ranging from 100 to 9909, which implies that the products are distributed across a large number of stores.
      - The cost data shows the cost associated with each SKU. The minimum cost is \$0, indicating that some products do not have cost, while the maximum cost is \$2700.00, which suggests a significant cost  variation among the products.
      - The actual price data reveals the prices at which these products are sold to customers. The minimum retail price is \$0.00, indicating the possibility of free products, while the maximum retail price is \$6,017.00, showing a broad range of price points.

        **Concerns**: columns cost and retails have \$0.

        **Solutions**: There could be some correspondences between skstinfo.csv's retails column and trnsact.csv's ORGPRICE column according to the SKU and STORE number. If we encountered missing values on both sides, we could replace the null data accordingly.


    + **trnsact.csv Exploration**
      
      Since we have not imported this CSV file into the database via pgadmin4, we head to import the first 100,000 observations in R to get a general feeling of this dataset due to its large volume (~11.37 GB). There are 13 effective columns of information except the one specified with the "Unknown" column. We found out that the column **"AMT"** is derived from the multiplication of **"QUANTITY"** and **"SPRICE"**, and as suggested before, the null values in the **"SPRICE"** and **"ORGPRICE"** columns can be filled according to the values stored in the skstinfo.csv file. Besides that, we do have a question about the actual meaning of **"TRANNUM"**, as we find that, there is more than one observation stored in the trnsact.csv data for the same **"TRANNUM"** number but with different sale dates and stores. From our understanding, this code should specify a serial number that is uniquely identified for each purchasing behavior, but different sale dates and stores for the same **"TRANNUM"** make us a bit confused.
      
#### To-Do-Lists:
- Fix problems in tables skuinfo.csv using command line and/or Python and/or R and import the other three CSV files that are not uploaded into Postgres.
- Create tables in Postgres according to the provided database schema and grant access to everyone in the team.
- Discuss one or several ML questions that we are interested in according to the data provided.

