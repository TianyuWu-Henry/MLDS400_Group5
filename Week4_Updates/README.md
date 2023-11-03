# As of Nov 3rd, 2023:
## Updates:
* After two weeks of EDA, we agreed to start with deciding on an ML question to further narrow down this project scope, that is, can we develop a predictive model that accurately forecasts the likelihood of a future return for a specific transaction, based on historical transaction attributes and patterns? The reason why we chose this question is that we think from the client's shoes to help identify the pain points, as well as combine the data availability after certain levels of EDA.
* Continued with the EDA processes using Python, specifically finishing the trnsact data and trying to explore the relationship (merge if necessary) between different datasets, especially after we decided on our ML question as illustrated above.

a. Extended EDA for **trnsact**

We are keenly focused on conducting an extensive EDA for the trnsact dataset. Our primary objective is to gain a comprehensive understanding of the data, with a particular emphasis on the column that delineates purchases and returns. By delving into this column, we aim to extract valuable insights and patterns that will inform our decision-making and further our understanding of customer behavior and business performance. By the end of each analysis, we plot the Number of Different SKUs Sold Over Time, the Number of Different Products Sold Over Time, the Number of Purchases and Returns Over Time, as well as the total revenue change over time, which better demonstrates and decouples our research question. In the meanwhile, we are also curious about the amount of AMT and ORGPRICE, with two plots generated for better visualization.

b. Extended EDA for merging **trnsact and strinfo**

We've noticed an interesting trend in the sales data – there's a significant spike in sales every December, likely due to the holiday season, including Thanksgiving and holiday festivities. However, this increase is consistently followed by a decline in January. This pattern indicates that people tend to spend more during the holidays, and sales tend to drop once the holiday excitement subsides. When we looked at the top 10 states, we found that they all exhibit this same pattern of a sharp rise in December sales, followed by a dip in January. This common trend suggests that people in these states tend to splurge during the holidays, and sales slow down in the month that follows. Understanding these regional sales patterns and the influence of seasonal factors can help businesses fine-tune their strategies and inventory management to maximize sales during peak times and adapt during slower months.

## To-Do-Lists:
- Discuss the result with the Teaching Assistant (TA) regarding our approach to solving the chosen machine-learning question (The question is still subject to change if feedback is not desirable enough).
- Conduct an extensive review of the existing literature further to elevate the sophistication and depth of our proposed machine learning question, and we will deepen it according to the literature if necessary.
