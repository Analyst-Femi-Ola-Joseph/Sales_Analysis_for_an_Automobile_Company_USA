##  PROJECT TITLE: 
# Sales_Analysis_for_an_Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

## PROBLEM STATEMENT:  
What are the Top Most-Profitable 5 States for the Bike Product Category in the United State ?

## DATA PRE-PROCESSING
#### DATA LOADING
``` Python
## let us import all the necessary python packages 
# solution 
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt
print("The packages have been successfully imported")
```
``` Python
# Reading the csv files into pandas dataframe

bikes_df = pd.read_csv("C:/Users/steph/OneDrive/Desktop/_DATA SCIENCE BOOTCAMP TRAINING/DATA SET/bikes.csv")

bikes_df.head()
```
<img width="746" alt="Pandas screenshot" src="https://github.com/user-attachments/assets/b4310ad6-6da5-47a5-98bc-9948e4977fee" />

#### DATA MODIFICATION
``` Python
# (1). Adding the following 3 columns to your pansdas Dataframe:  bikes_df

# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)

bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 

# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)

bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 

# Profit : To be obtained by (SalesRevenue - TotalCostPrice)

bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]

bikes_df.head()

```

<img width="745" alt="Data Modification Screen shot" src="https://github.com/user-attachments/assets/7d002691-124e-41f5-b3d2-07837851af0a" />

## DATA ANALYSIS

#### DATA FILTERING

``` Python
# Filtering out only the data that is relevant to solve the problem statement

is_uSA = bikes_df["CustomerCountry"] == "United States"	

is_bike = bikes_df["ProductCategory"] == "Bikes"

bike_in_the_US = bikes_df[(is_uSA) & (is_bike)]

bike_in_the_US.head()
```

<img width="742" alt="Data Filtering Screen Shot" src="https://github.com/user-attachments/assets/9cbf6390-2e67-4942-b0ac-a785055cec38" />

#### DATA AGGREGATION (Data Summary)

``` Python
# Aggregating the total profit by states in the united states for bikes sales or transaction.

total_profit_by_states = bike_in_the_US.pivot_table(values = "Profit" , index = "CustomerState" , aggfunc = np.sum )

total_profit_by_states

```

<img width="194" alt="Data Aggregation Screen Shot" src="https://github.com/user-attachments/assets/5777f0eb-99cc-41f5-ad7c-4f056366db8b" />


#### DATA SORTING ( Data Ranking)

``` Python
# Sorting the aggregated data in orser to Rank the states according to the top most profitable states.

total_profit_by_states.sort_values("Profit", ascending = False )

```

<img width="178" alt="Data Ranking Screen Shot" src="https://github.com/user-attachments/assets/f3dd5ab3-1406-43c0-bfde-5e4aaaa7c265" />


#### RESULT

``` Python
# The Top Most-Profitable 5 States for the Bike Product Category in the United State ?

top_5_most_profitable_states_in_USA = total_profit_by_states.sort_values("Profit", ascending = False ).head()

top_5_most_profitable_states_in_USA

```

<img width="191" alt="Result for top 5 most profitable States" src="https://github.com/user-attachments/assets/3225eb38-530b-4f8c-8ec9-d90baf882a8a" />


## DATA VISUALIZATION

``` Python
# Visualizing the result

top_5_most_profitable_states_in_USA.plot(kind = "bar")

# Adding a title and label to the plot

plt.title("The Top 5 Most Profitable States for Bike Product in the US")

plt.xlabel("States")

plt.ylabel("Total Profit in Million Dollars")

# Showing the plot

plt.show()

```

<img width="415" alt="Project 1 Screen shot" src="https://github.com/user-attachments/assets/89b82a83-1152-4d11-8d95-c5b714e7a6a7" />
