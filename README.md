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
## DATA ANALYSIS

#### DATA FILTERING

``` Python
# Filtering out only the data that is relevant to solve the problem statement

is_uSA = bikes_df["CustomerCountry"] == "United States"	

is_bike = bikes_df["ProductCategory"] == "Bikes"

bike_in_the_US = bikes_df[(is_uSA) & (is_bike)]

bike_in_the_US.head()
```

#### DATA AGGREGATION (Data Summary)

``` Python
# Aggregating the total profit by states in the united states for bikes sales or transaction.

total_profit_by_states = bike_in_the_US.pivot_table(values = "Profit" , index = "CustomerState" , aggfunc = np.sum )

total_profit_by_states

```
#### DATA SORTING ( Data Ranking)

``` Python
# Sorting the aggregated data in orser to Rank the states according to the top most profitable states.

total_profit_by_states.sort_values("Profit", ascending = False )

```
#### RESULT

``` Python
# The Top Most-Profitable 5 States for the Bike Product Category in the United State ?

top_5_most_profitable_states_in_USA = total_profit_by_states.sort_values("Profit", ascending = False ).head()

top_5_most_profitable_states_in_USA

```

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


