# Retail Strategy and Analytics: Optimization of Control Stores for Sales Enhancement

## Goal of the project
**Introduction:**

In this project, we aim to optimize the performance of retail chain stores by establishing control stores based on their performance compared to selected trial stores. By leveraging data analytics and strategic insights, we seek to enhance sales revenue and drive growth within the retail chain.

**Problem Statement:**

The retail industry faces challenges in understanding customer behavior and optimizing store performance to maximize sales revenue. Without proper insights and strategic planning, retail chains may struggle to identify target customer segments and make informed decisions for category review and expansion.


## Analysis Approach
### 1. Data Quality Assessment and Data Cleaning
The first step towards generating useful insights from the data was the data prepartion, quality assessment and data cleaning step. After the cleaning process exploratory data analysis on the transaction dataset and identify customer purchasing behaviours to generate insights and provide commercial recommendations.

In the data cleaning step the data quality of the datasets were first assesed. After a data quality assessment the following data quality issues was observed and the necessary process to mitigate the issue was followed :
- The Date column in the  dataset was in integer format ie. number of days from Dec 30, 1985. Hence this column was converted to datetime format taking Dec 30, 1985 as a referennce date.
- Removed outlier records based on the PROD_QTY (quantity purchased of a particular product) column.
- The analysis concentrated on Chips products. Hence the "PROD_NAME" (Product Name) column was split and frequency of each word was counted then all rows containing "salsa" in "PROD_NAME" was removed. 
- A new feature namely Brand was created by extracting the brand name from the product name "PROD_NAME"
- Checked whether there are duplicate records present in the dataset. 

### 2. Exploratory Data Analysis on Customer Segments
After the data cleaning process, we defined mertics of interest that will drive metrics of interest that will drive our analysis :
- <b>Customer Segments who spend the most on chips, described based on their lifestage and the premium tier they belong</b><br> 
Sales are coming mainly from Budget - older families ($ 168,363), Mainstream - young singles/couples ($ 157,622) and Mainstream- retirees ($ 155,677) which contributes to 25% of the total sales of $ 1,933 K.
![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/d321db55-9355-4f59-8f18-68e19c119b59)


- <b>Number of Customers in each Customer Segment</b><br>
Young Singles/Couples (Mainstream) has the highest population, followed by Retirees (Mainstream) which explains their high total sales. There are more Mainstream - young singles/couples and Mainstream - retirees who buy chips. This contributes to there being more sales to these customer segments but this is not a major driver for the Budget - Older families segment. However amount of chips bought per customer can be a determining factor for higher sales.
![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/b582d7bc-b93a-4b15-a66b-e6ccc49705e2)


- <b>Amount of chips bought per Customer Segment</b><br>
Affluence appears consistent across each individual life stage profile; Older and Young Family shoppers purchase the highest average units of chips pack per transaction.
![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/cff4cb7a-90e4-4acc-b01c-1336c6024f42)


- <b>Average price of pack bought per unit purchase of chips across Customer Segments</b><br>
Mainstream midage and young singles and couples are more willing to pay more per packet of chips compared to their budget and premium counterparts. This may be due to premium shoppers being more likely to buy healthy snacks and when they buy chips, this is mainly for entertainment purposes rather than their own consumption. This is also supported by there being fewer premium midage and young singles and couples buying chips compared to their mainstream counterparts.
![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/11824d65-47b8-4cab-b9f6-151502f6af1e)

The difference in average price of chips pack isn't quite large across the customer segments. Hence performed <b>Two Sample t-test</b> to find out whether this difference in average price is statistically different. <br>
The t-test results in a p-value came to be < 2.2e-16. Hence it means that the average price for mainstream young and midage singles and couples are significantly higher than that of budget or premium young and midage singles and couples.<br>
<br>
- <b>Brand and Pack Size preferred across Customer Segments</b><br>
Chips brand Kettle is dominating every segment as the most purchased brand.Most frequent chip size purchased is 175gr followed by the 150gr chip size for all segments.
![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/a4745763-179f-4f91-b1f9-e028d5e3ef22)



### 3. Experimentation and Uplift testing
In this stage of analysis benchmark stores or control stores are established and their impact in trial store layouts on customer sales and number of customers visting the stores are tested and compared. Stores with store number 77, 86 and 88 are seleteced as trial stores and the goal is to establish control stores for each of these trial stores.The stores which were operational for the entire observation period (i.e. for the entire year, 12 months of data) are eligible to be a control store.

Thereafter a comparison of control stores and trial stores are done prior to the trial period of Feb 2019 in terms of the following performance metrics :
- Monthly overall sales revenue
- Monthly number of customers

The ranking of how similar a potential store is similar to a trial store is based on a composite score of the following :
- correlation between the trial store’s performance and each control store’s performance
- standardised metric based on the absolute difference between the trial store’s performance and each control store’s performance

The final composite score is simple average of the correlation and magnitude scores for each driver. The store with the highest composite score is then selected as the control store since it is most similar to the trial store.

The trial store and control store pairs are geiven below :
- For trail store 77, the control store is 233
- For trail store 86, the control store is 155
- For trail store 88, the control store is 237

Visualizations depicting how similar trial stores and control strores are is given below :<br>
![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/32736289-83cc-4575-baad-c090ccf7da3d)

![Untitled](https://github.com/vbhatsaccnt/Retail-Strategy-and-Analytics-Optimization-of-Control-Stores-for-Sales-Enhancement/assets/67544433/bf45b1ff-d551-42b7-9c41-05a18599715e)


## Datasets Used
The datasets used include:
- __Purchase_Behaviour.csv__: This dataset contains the customer related data like their Liability Number, Lifestage and to which Premium Tier they belong.
- __Transaction_data.xlsx__: This dataset includes the transaction details for customer.


## Data Dictionary

### Purchase_Behaviour

| Table Column | Data Type | Description |
| -------- | ------------- | --------- |
| LYLTY_CARD_NBR (PRIMARY_KEY) | integer  | Liability Number of a customer, primary key to identify a customer |
|  LIFESTAGE | varchar(32) | Lifestage of the customer like young / midage / old singles or couples |
| PREMIUM_CUSTOMER | varchar(32) | Premium Level of the Customer like Mainstream / Budget / Premium |

### Transaction_data

| Table Column | Data Type | Description |
| ------------ | ---------- | --------- |
| TXN_ID (PRIMARY_KEY) | integer  | primary key for Transaction ID |
|  DATE | integer | Occurance date of Transaction  |
| STORE_NBR | integer | Store Number at which the purchase transaction happened |
| LYLTY_CARD_NBR (FOREIGN KEY) | integer | Customer's Liability Number |
| PROD_NBR | integer | Product Number of the product  |
| PROD_NAME | varchar(32) |  Product Name |
| PROD_QTY | integer |  Product Quantity purchased |
| TOT_SALES | integer | Total Sales Amount |


## Tools and Technologies used
The tools used in this project include:
- __Python__ - This was needed to conduct <b>Data Quality Assessment</b> and also for <b>Data Cleaning processes</b>. With Python libraries <b>pandas, matplotlib, seaborn</b> exploratory data analysis of the datasets and to gain useful insights from the data was possible.



## Built With
- Python 3.12.0

## Authors
- Vikas Bhat - [Github Profile]([https://github.com/AbhishekGit-hash](https://github.com/vbhatsaccnt)https://github.com/vbhatsaccnt)



