

```python
import pandas as pd
```


```python
filename = "purchase_data.json"
purchase_df = pd.read_json(filename, orient=None, typ='frame', dtype=True,
              convert_axes=True, convert_dates=True, keep_default_dates=True,
              numpy=False, precise_float=False, date_unit=None, encoding=None,
              lines=False, chunksize=None, compression='infer')
```


```python
# Total Players
unique_players = purchase_df["SN"].unique()
total_players = len(unique_players)

# Create Dataframe for answer
total_players_data = {"Total Players" : [total_players]}
total_players_df = pd.DataFrame(total_players_data)
total_players_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Number of Unique Items
unique_items = purchase_df["Item Name"].unique()
num_unique_items = len(unique_items)
```


```python
# Average Purchase Price
avg_purchase_price = purchase_df["Price"].mean()
formatted_avg_purchase_price = "$" + str(round(avg_purchase_price, 2))
```


```python
# Total Number of Purchases
total_purchases = purchase_df["Item ID"].count()
```


```python
# Total Revenue
total_revenue = purchase_df["Price"].sum()
formatted_total_revenue = "$" + str(round(total_revenue, 2))
```


```python
# Purchasing Analysis (Total)
purchasing_analysis_rawdic = {"Number of Unique Items" : [num_unique_items],
                         "Average Purchase Price": [formatted_avg_purchase_price],
                         "Total Number of Purchases" : [total_purchases],
                         "Total Revenue" : [formatted_total_revenue]}

purchasing_analysis_df = pd.DataFrame(purchasing_analysis_rawdic)
purchasing_analysis_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.93</td>
      <td>179</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Percentage and Count of Male Players
male_players = purchase_df.loc[purchase_df["Gender"] == "Male", :]
group_male_players = male_players.groupby("SN")

# Count of Male Players
count_male_players = len(group_male_players)

# Percentage of Male Players
percentage_male_players = count_male_players / total_players
formatted_percentage_male_players = round(100 * percentage_male_players, 2)
```


```python
# Percentage and Count of Female Players
female_players = purchase_df.loc[purchase_df["Gender"] == "Female", :]
group_female_players = female_players.groupby("SN")

# Count of Female Players
count_female_players = len(group_female_players)

# Percentage of Female Players
percentage_female_players = count_female_players / total_players
formatted_percentage_female_players = round(100 * percentage_female_players, 2)
```


```python
# Percentage and Count of Other / Non-Disclosed Players
other_gender_players = purchase_df.loc[purchase_df["Gender"] == "Other / Non-Disclosed", :]
group_other_gender_players = other_gender_players.groupby("SN")

# Count of Other / Non-Disclosed Players
count_other_gender_players = len(group_other_gender_players)

# Percentage of Other / Non-Disclosed Players
percentage_other_gender_players = count_other_gender_players / total_players
formatted_percentage_other_gender_players = round(100 * percentage_other_gender_players, 2)
```


```python
# Gender Demographics
gender_demographics_rawdic = {"Percentage of Total Players" : [formatted_percentage_male_players, formatted_percentage_female_players, formatted_percentage_other_gender_players],
                         "Total Count": [count_male_players, count_female_players, count_other_gender_players]}

gender_demographics_df = pd.DataFrame(gender_demographics_rawdic)

formatted_gender_demographics = gender_demographics_df.rename(index={0 : "Male", 1 : "Female", 2 : "Other / Non-Disclosed"})
formatted_gender_demographics
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Total Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Male Purchasing Analysis

# Count of Male Purchases
male_players_purchases = purchase_df.loc[purchase_df["Gender"] == "Male", :]
group_male_players_purchases = male_players_purchases.groupby("SN")
count_male_players_purchases = len(group_male_players_purchases)

# Average Purchase Price (Males)
avg_male_players_purchases = male_players_purchases["Price"].mean()
formatted_avg_male_players_purchases = "$" + str(round(avg_male_players_purchases, 2))

# Total Purchase Value (Males)
total_male_players_purchases = male_players_purchases["Price"].sum()
formatted_total_male_players_purchases = "$" + str(round(total_male_players_purchases, 2))

# Normalized Avg Total (Males)
normalized_male_players_purchases = total_male_players_purchases / count_male_players_purchases
formatted_normalized_male_players_purchases = "$" + str(round(normalized_male_players_purchases, 2))
```


```python
# Female Purchasing Analysis

# Count of female Purchases
female_players_purchases = purchase_df.loc[purchase_df["Gender"] == "Female", :]
group_female_players_purchases = female_players_purchases.groupby("SN")
count_female_players_purchases = len(group_female_players_purchases)

# Average Purchase Price (Females)
avg_female_players_purchases = female_players_purchases["Price"].mean()
formatted_avg_female_players_purchases = "$" + str(round(avg_female_players_purchases, 2))

# Total Purchase Value (Females)
total_female_players_purchases = female_players_purchases["Price"].sum()
formatted_total_female_players_purchases = "$" + str(round(total_female_players_purchases, 2))

# Normalized Avg Total (Females)
normalized_female_players_purchases = total_female_players_purchases / count_female_players_purchases
formatted_normalized_female_players_purchases = "$" + str(round(normalized_female_players_purchases, 2))
```


```python
# Other / Non-Disclosed Purchasing Analysis

# Count of Other / Non-Disclosed Purchases
other_gender_players_purchases = purchase_df.loc[purchase_df["Gender"] == "Other / Non-Disclosed", :]
group_other_gender_players_purchases = other_gender_players_purchases.groupby("SN")
count_other_gender_players_purchases = len(group_other_gender_players_purchases)

# Average Purchase Price (Other / Non-Disclosed)
avg_other_gender_players_purchases = other_gender_players_purchases["Price"].mean()
formatted_avg_other_gender_players_purchases = "$" + str(round(avg_other_gender_players_purchases, 2))

# Total Purchase Value (Other / Non-Disclosed)
total_other_gender_players_purchases = other_gender_players_purchases["Price"].sum()
formatted_total_other_gender_players_purchases = "$" + str(round(total_other_gender_players_purchases, 2))

# Normalized Avg Total (Other / Non-Disclosed)
normalized_other_gender_players_purchases = total_other_gender_players_purchases / count_other_gender_players_purchases
formatted_normalized_other_gender_players_purchases = "$" + str(round(normalized_other_gender_players_purchases, 2))
```


```python
# Purchasing Analysis by Gender Chart
purchasing_analysis_gender_rawdic = {"Purchase Count" : [count_male_players_purchases, count_female_players_purchases, count_other_gender_players_purchases],
                         "Average Purchase Price": [formatted_avg_male_players_purchases, formatted_avg_female_players_purchases, formatted_avg_other_gender_players_purchases],
                         "Total Purchase Value" : [formatted_total_male_players_purchases, formatted_total_female_players_purchases, formatted_total_other_gender_players_purchases],
                         "Normalized Totals" : [formatted_normalized_male_players_purchases, formatted_normalized_female_players_purchases, formatted_normalized_other_gender_players_purchases]}

purchasing_analysis_gender_df = pd.DataFrame(purchasing_analysis_gender_rawdic)
formatted_purchasing_analysis_gender_df = purchasing_analysis_gender_df.rename(index={0 : "Male", 1 : "Female", 2 : "Other / Non-Disclosed"})
formatted_purchasing_analysis_gender_df.index.name = "Gender"
formatted_purchasing_analysis_gender_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>$2.95</td>
      <td>$4.02</td>
      <td>465</td>
      <td>$1867.68</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>$2.82</td>
      <td>$3.83</td>
      <td>100</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>$3.25</td>
      <td>$4.47</td>
      <td>8</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Age Demographics into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
bins = [0, 10,  14,  19, 24, 29, 34, 39, 100]

group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40=<"]
```


```python
# Place into bins
purchase_df["Age Range"] = pd.cut(purchase_df["Age"], bins, labels=group_names)

#regiment_df["Test Score Summary"] = pd.cut(regiment_df["Test Score"], bins, labels=group_names)
age_demographics = purchase_df.groupby("Age Range")
unique_age = age_demographics["SN"].nunique()
unique_age_df = pd.DataFrame(unique_age)
count_age_demographics = unique_age_df.rename(columns={"SN" : "Total Count of Players"})
```


```python
df = count_age_demographics["Total Count of Players"]
percentage_age_demographics = [round((person / total_players) * 100, 2) for person in df]
```


```python
# Convert Percentage Age Demographics into DataFrame
percentage_age_demographics_df = pd.DataFrame(percentage_age_demographics)
renamed_percentage_age_demographics_df = percentage_age_demographics_df.rename(index={0 : "<10", 1 : "10-14", 2 : "15-19", 3: "20-24",
                                                                                      4 : "25-29", 5 : "30-34", 6 : "35-39", 7 : "40=<"})

```


```python
# Age Demographics
age_demographics_table = count_age_demographics.join(renamed_percentage_age_demographics_df)
final_age_demographics_table = age_demographics_table.rename(columns={0 : "Percentage of Players"})
final_age_demographics_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count of Players</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>22</td>
      <td>3.84</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>20</td>
      <td>3.49</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>45.20</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>15.18</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>8.20</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>4.71</td>
    </tr>
    <tr>
      <th>40=&lt;</th>
      <td>11</td>
      <td>1.92</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchase Count
purchase_count = age_demographics["Age"].count()

# Convert to DataFrame
purchase_count_df = pd.DataFrame(purchase_count)
renamed_purchase_count_df = purchase_count_df.rename(columns={"Age" : "Purchase Count"})
```


```python
# Average Purchase Price by Age
avg_price_age = age_demographics["Price"].mean()

# Convert to DataFrame
avg_price_age_df = pd.DataFrame(avg_price_age)
renamed_avg_price_age_df = avg_price_age_df.rename(columns={"Price" : "Average Purchase Price"})
```


```python
# Total Purchase Value by Age
total_value_age = age_demographics["Price"].sum()

# Convert to DataFrame
total_value_age_df = pd.DataFrame(total_value_age)
renamed_total_value_age_df = total_value_age_df.rename(columns={"Price" : "Total Purchase Value"})
```


```python
# Normalized Values
normalized_values_age = total_value_age / final_age_demographics_table["Total Count of Players"]

# Format and Convert
formatted_normalized_values_age_df = pd.DataFrame(normalized_values_age)
renamed_normalized_values_age_df = formatted_normalized_values_age_df.rename(columns={0 : "Normalized Value Totals"})
```


```python
# Purchasing Analysis (Age) Chart
first_merged_table = renamed_avg_price_age_df.join(renamed_total_value_age_df)
second_merged_table = first_merged_table.join(renamed_normalized_values_age_df)
purchasing_analysis_age_table = second_merged_table.join(renamed_purchase_count_df)
purchasing_analysis_age_table[["Average Purchase Price", "Total Purchase Value", "Normalized Value Totals"]] = purchasing_analysis_age_table[["Average Purchase Price", "Total Purchase Value", "Normalized Value Totals"]].applymap("${:,.2f}".format)
purchasing_analysis_age_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Value Totals</th>
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$3.02</td>
      <td>$96.62</td>
      <td>$4.39</td>
      <td>32</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$2.70</td>
      <td>$83.79</td>
      <td>$4.19</td>
      <td>31</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>$3.86</td>
      <td>133</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$2.91</td>
      <td>$978.77</td>
      <td>$3.78</td>
      <td>336</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$2.96</td>
      <td>$370.33</td>
      <td>$4.26</td>
      <td>125</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$3.08</td>
      <td>$197.25</td>
      <td>$4.20</td>
      <td>64</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$2.84</td>
      <td>$119.40</td>
      <td>$4.42</td>
      <td>42</td>
    </tr>
    <tr>
      <th>40=&lt;</th>
      <td>$3.16</td>
      <td>$53.75</td>
      <td>$4.89</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Top Spenders (SN) - Purchase Count
group_SN = purchase_df.groupby("SN")
SN_count = group_SN.count()
SN_count_sort = SN_count.sort_values("Item ID", ascending=False)
top_spender_num_purchases = SN_count_sort["Item ID"]
top_spender_purchases_df = pd.DataFrame(top_spender_num_purchases)
top_spender_num_purchases_df = top_spender_purchases_df.rename(columns={"Item ID" : "Purchase Count"})
```


```python
# Top Spenders (SN) - Average Purchase Price
group_SN = purchase_df.groupby("SN")
SN_avg_price = group_SN.mean()
SN_avg_price_sort = SN_avg_price.sort_values("Price", ascending=False)
top_spender_avg_price = SN_avg_price_sort["Price"]
top_spender_avg_price_df = pd.DataFrame(top_spender_avg_price)
renamed_top_spender_avg_price_df = top_spender_avg_price_df.rename(columns={"Price" : "Average Purchase Price"})
```


```python
# Top Spenders (SN) - Total Purchase Value
group_SN = purchase_df.groupby("SN")
SN_total_value = group_SN.sum()
SN_total_value_sort = SN_total_value.sort_values("Price", ascending=False)
top_spender_total_value = SN_total_value_sort["Price"]
top_spender_total_value_df = pd.DataFrame(top_spender_total_value)
renamed_top_spender_total_value_df = top_spender_total_value_df.rename(columns={"Price" : "Total Purchase Value"})
```


```python
# Joining DataFrames to Create Final Product
numpurchase_avgprice_joined_table = top_spender_num_purchases_df.join(renamed_top_spender_avg_price_df)
top_spenders_table_df = numpurchase_avgprice_joined_table.join(renamed_top_spender_total_value_df)

# Format Final DataFrame
top_spenders_table_df[["Average Purchase Price", "Total Purchase Value"]] = top_spenders_table_df[["Average Purchase Price", "Total Purchase Value"]].applymap("${:,.2f}".format)
top_spenders_table_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Qarwen67</th>
      <td>4</td>
      <td>$2.49</td>
      <td>$9.97</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Sondastan54</th>
      <td>4</td>
      <td>$2.56</td>
      <td>$10.24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Most Popular Items - Purchase Count
item_group = purchase_df.groupby(["Item ID", "Item Name"])
count_item_group = item_group.count()
purchase_count_item = count_item_group["SN"]
purchase_count_item_df = pd.DataFrame(purchase_count_item)
renamed_purchase_count_item_df = purchase_count_item_df.rename(columns={"SN" : "Purchase Count"})
```


```python
# Most Popular Items - Total Purchase Value
item_group = purchase_df.groupby(["Item ID", "Item Name"])
total_item_group = item_group.sum()
total_item_group
total_purchase_item = total_item_group["Price"]
total_purchase_item_df = pd.DataFrame(total_purchase_item)
renamed_total_purchase_item_df = total_purchase_item_df.rename(columns={"Price" : "Total Purchase Value"})
```


```python
# Most Popular Items - Item Price
item_group = purchase_df.groupby(["Item ID", "Item Name"])
item_price_group = item_group.max()
item_price = item_price_group["Price"]
item_price_df = pd.DataFrame(item_price)
renamed_item_price_df = item_price_df.rename(columns={"Price" : "Item Price"})
```


```python
# Joining DataFrames to Create Most Popular Items DataFrame
count_price_join = renamed_purchase_count_item_df.join(renamed_item_price_df)
popular_items = count_price_join.join(renamed_total_purchase_item_df)
most_popular_items = popular_items.sort_values("Purchase Count", ascending=False)
most_popular_items[["Item Price", "Total Purchase Value"]] = most_popular_items[["Item Price", "Total Purchase Value"]].applymap("${:,.2f}".format)
```


```python
# Most Profitable Items - Most Times Purchased
most_popular_items.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Formatting for Most Profitable Items - Highest Revenue Total
most_profitable_items = popular_items.sort_values("Total Purchase Value", ascending=False)
most_profitable_items[["Item Price", "Total Purchase Value"]] = most_profitable_items[["Item Price", "Total Purchase Value"]].applymap("${:,.2f}".format)
```


```python
# Most Profitable Items - Highest Revenue Total
most_profitable_items.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
# -------------------------------------------------------------------------------------
```


```python
# -------------------------------------------------------------------------------------
```


```python
# Summary of Charts
```


```python
total_players_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchasing_analysis_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.93</td>
      <td>179</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
formatted_gender_demographics
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Total Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
formatted_purchasing_analysis_gender_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>$2.95</td>
      <td>$4.02</td>
      <td>465</td>
      <td>$1867.68</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>$2.82</td>
      <td>$3.83</td>
      <td>100</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>$3.25</td>
      <td>$4.47</td>
      <td>8</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
final_age_demographics_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count of Players</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>22</td>
      <td>3.84</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>20</td>
      <td>3.49</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>45.20</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>15.18</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>8.20</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>4.71</td>
    </tr>
    <tr>
      <th>40=&lt;</th>
      <td>11</td>
      <td>1.92</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchasing_analysis_age_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Value Totals</th>
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$3.02</td>
      <td>$96.62</td>
      <td>$4.39</td>
      <td>32</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$2.70</td>
      <td>$83.79</td>
      <td>$4.19</td>
      <td>31</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>$3.86</td>
      <td>133</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$2.91</td>
      <td>$978.77</td>
      <td>$3.78</td>
      <td>336</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$2.96</td>
      <td>$370.33</td>
      <td>$4.26</td>
      <td>125</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$3.08</td>
      <td>$197.25</td>
      <td>$4.20</td>
      <td>64</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$2.84</td>
      <td>$119.40</td>
      <td>$4.42</td>
      <td>42</td>
    </tr>
    <tr>
      <th>40=&lt;</th>
      <td>$3.16</td>
      <td>$53.75</td>
      <td>$4.89</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_spenders_table_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Qarwen67</th>
      <td>4</td>
      <td>$2.49</td>
      <td>$9.97</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Sondastan54</th>
      <td>4</td>
      <td>$2.56</td>
      <td>$10.24</td>
    </tr>
  </tbody>
</table>
</div>




```python
most_popular_items.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
most_profitable_items.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


