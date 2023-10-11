# MLDS400_Group5
This is the repo for Group 5's submission of MLDS 400's team project.

## Weekly Updates:
### Until Oct 13th 2023



#### skstinfo.csv Analysis

There is an extra column that is unknown or not in the DB schema given. There are 39230145 oberservations/rows and there are 5 columns (SKU, STORE, COST, RETAIL, UNKOWN)

- SKU data reveals that there is a wide range of products represented. With SKUs ranging from 3 to 10 million, this suggests a diverse product catalog.
- The store data provided information about where these products are sold, with store IDs ranging from 100 to 9909, which implies that the products are distributed across a large number of stores.
- The cost data shows the cost associated with each SKU. The minimum cost is \$0, indicating that some products does not have cost, while the maximum cost if \$2700.00, which suggests an signicant cost variation among the products.
- The retual price data reveals the prices at which these products are sold to customers. The minimum retail price is \$0.00, indicating the possibility of free products, while the maximum retail price is \$6,017.00, showing a broad range of price points.

**Concerns**: columns cost and retails have \$0.
There could be some correspondences between skstinfo.csv's retails column and trnsact.csv's ORGPRICE column according to the SKU and STORE number. If we encountered missing values on both sides, we could replace the NA data accordingly.
