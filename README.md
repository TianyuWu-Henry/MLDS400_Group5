# MLDS400_Group5
This is the repo for recording Group 5's process of MLDS 400's team project.

Group Members: Xiyi Lin, Omar Shatrat, Fanqi Song, Tianyu Wu

## Weekly Updates and To-Do-Lists:
### Oct 13th 2023:
#### Updates:
* Used pgcli/psql to connect to the MLDS’s postgres DB server successfully, and imported two CSV files (deptinfo and strinfo) into databases via pgadmin4.
* Got a general feeling of the five CSV files through looking into the schema and starting to analyze them in R.
    + **deptinfo.csv and strinfo.csv Exploration**
    + **skstinfo.csv Exploration**
      
      There is an extra column that is unknown or not in the DB schema given. There are 39,230,145 observations with 5 columns (SKU, STORE, COST, RETAIL, UNKOWN)

      - SKU data reveals that there is a wide range of products represented. With SKUs ranging from 3 to 10 million, this suggests a diverse product catalog.
      - The store data provided information about where these products are sold, with store IDs ranging from 100 to 9909, which implies that the products are distributed across a large number of stores.
      - The cost data shows the cost associated with each SKU. The minimum cost is \$0, indicating that some products does not have cost, while the maximum cost if \$2700.00, which suggests an signicant cost   variation among the products.
      - The retual price data reveals the prices at which these products are sold to customers. The minimum retail price is \$0.00, indicating the possibility of free products, while the maximum retail price is \$6,017.00, showing a broad range of price points.

        **Concerns**: columns cost and retails have \$0.

        **Solutions**: There could be some correspondences between skstinfo.csv's retails column and trnsact.csv's ORGPRICE column according to the SKU and STORE number. If we encountered missing values on both sides, we could replace the NA data accordingly.


    + **trnsact.csv Exploration**


#### To-Do-Lists:
- Create tables in Postgres according to the provided database schema and grant access to everyone in the team.
- Discuss one or several ML questions that we are interested according to the data provided.
