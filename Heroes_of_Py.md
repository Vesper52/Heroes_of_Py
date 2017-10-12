

```python
import pandas as pd
```


```python
Purchase_data="purchase_data.json"
```


```python
Heroes_df=pd.read_json(Purchase_data)

```


```python
Heroes_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Player Count

Total_players_df=pd.DataFrame({"Total Players":[Heroes_df["Age"].count()]})
Total_players_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>78</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis
x=Heroes_df["Price"].sum()/Heroes_df["Price"].count()
x=round(x,2)
Purchasing_Analysis_df=pd.DataFrame({"Number of Unique Items":[Heroes_df['Item Name'].nunique()],"Average Price":"$"+str(x),"Total Number of Purchases":[Heroes_df['Price'].count()],"Total Revenue":[Heroes_df["Price"].sum()]})
#Purchasing_Analysis_df["Total Revenue"]=Purchasing_Analysis_df["Total Revenue"].map("${:.2f}").format
Purchasing_Analysis_df["Total Revenue"]=Purchasing_Analysis_df["Total Revenue"].map("${:.2f}".format)
Purchasing_Analysis_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.92</td>
      <td>63</td>
      <td>78</td>
      <td>$228.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Gender Demographics

total_genders=Heroes_df["Gender"].count()
total_count=Heroes_df["Gender"].value_counts()
total_count.head()


Gender_df=pd.DataFrame({"Percentage of Players":(total_count/total_genders)*100,"Total Count":total_count})
Gender_df["Percentage of Players"]=Gender_df["Percentage of Players"].map("%{:.2f}".format)
Gender_df.head()




#Trend Analysis #1
#To no suprise as with most online video games the vast majority of the player base is made up of males,
#what would be really interesting to see is if this game had a class sytem the breakdown of genders on roles,
#in most mmos females tend to vastly play support/healers roles compared to tank/dps roles. I would imagine it
#would be the same in this game too.
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>%82.05</td>
      <td>64</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>%16.67</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>%1.28</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis(Gender)
Grouped_gender=Heroes_df.groupby(['Gender'])
Average_Price=Grouped_gender["Price"].sum()/Grouped_gender["Price"].count()
Total_Price=Grouped_gender["Price"].sum()



Gender_Purchase_df=pd.DataFrame({"Purchase Count":(total_count),"Average Purchase Price":Average_Price,"Total Purchase Value":Total_Price})
Gender_Purchase_df["Average Purchase Price"]=Gender_Purchase_df["Average Purchase Price"].map("${:.2f}".format)
Gender_Purchase_df["Total Purchase Value"]=Gender_Purchase_df["Total Purchase Value"].map("${:.2f}".format)
Gender_Purchase_df.head()



```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>$3.18</td>
      <td>13</td>
      <td>$41.38</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>$2.88</td>
      <td>64</td>
      <td>$184.60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>$2.12</td>
      <td>1</td>
      <td>$2.12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age demographics
Age_bins=[0,10,14,20,24,28,32,36,40,100]
Group_names=['0-10','11-14','15-20','21-24','25-28','29-32','33-36','37-40','40<']

Heroes_df["Age Range"]=pd.cut(Heroes_df["Age"],Age_bins,labels=Group_names)
Age_Count=Heroes_df["Age Range"].value_counts()
Age_Count.head()
total_ages=Heroes_df["Age"].count()
Age_Demo_df=pd.DataFrame({"Percentage of Players":(Age_Count/total_ages)*100,"Total Count":Age_Count})
Age_Demo_df["Percentage of Players"]=Age_Demo_df["Percentage of Players"].map("%{:.2f}".format)
Age_Demo_df.head(9)


#Trend Analysis #2
#As with most mmo's it seems that the majority of the player base tends to be youn with the 21 to 24 age demographic having the
#highest population. This is due to video games in general being very popular with young people in general as they tend to not have
#as many responsibilites/jobs as say the older population.

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>21-24</th>
      <td>%33.33</td>
      <td>26</td>
    </tr>
    <tr>
      <th>15-20</th>
      <td>%26.92</td>
      <td>21</td>
    </tr>
    <tr>
      <th>25-28</th>
      <td>%11.54</td>
      <td>9</td>
    </tr>
    <tr>
      <th>33-36</th>
      <td>%8.97</td>
      <td>7</td>
    </tr>
    <tr>
      <th>0-10</th>
      <td>%6.41</td>
      <td>5</td>
    </tr>
    <tr>
      <th>29-32</th>
      <td>%5.13</td>
      <td>4</td>
    </tr>
    <tr>
      <th>37-40</th>
      <td>%3.85</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11-14</th>
      <td>%3.85</td>
      <td>3</td>
    </tr>
    <tr>
      <th>40&lt;</th>
      <td>%0.00</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis by Age

Age_bins=[0,10,14,20,24,28,32,36,40,100]
Group_names=['0-10','11-14','15-20','21-24','25-28','29-32','33-36','37-40','40<']
Heroes_df["Age Range"]=pd.cut(Heroes_df["Age"],Age_bins,labels=Group_names)
Age_Count=Heroes_df["Age Range"].value_counts()
Grouped_Age=Heroes_df.groupby(['Age Range'])
Average_Price=Grouped_Age["Price"].sum()/Grouped_Age["Price"].count()
Total_Price=Grouped_Age["Price"].sum()



Age_Purchase_df=pd.DataFrame({"Purchase Count":(Age_Count),"Average Purchase Price":Average_Price,"Total Purchase Value":Total_Price})
Age_Purchase_df["Average Purchase Price"]=Age_Purchase_df["Average Purchase Price"].map("${:.2f}".format)
Age_Purchase_df["Total Purchase Value"]=Age_Purchase_df["Total Purchase Value"].map("${:.2f}".format)
Age_Purchase_df.head(8)


#Trend Analysis #3
#Following a similar trend to the previous analysis it seems that the 15-20 and 21-24 age demographics are also the highest 
#spenders. Whats interesting is that the 21-24 demograhic is purchasing items on average at a higher price than the 15-20
#bracket this could be due to people who are 21-24 tend to have jobs or a part time job that would pay more while people 15-20
#tend to be in school and would only have jobs during the summer thus having less money to spend on this mmo.
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0-10</th>
      <td>$2.76</td>
      <td>5</td>
      <td>$13.82</td>
    </tr>
    <tr>
      <th>11-14</th>
      <td>$2.99</td>
      <td>3</td>
      <td>$8.96</td>
    </tr>
    <tr>
      <th>15-20</th>
      <td>$2.76</td>
      <td>21</td>
      <td>$57.94</td>
    </tr>
    <tr>
      <th>21-24</th>
      <td>$3.13</td>
      <td>26</td>
      <td>$81.36</td>
    </tr>
    <tr>
      <th>25-28</th>
      <td>$2.90</td>
      <td>9</td>
      <td>$26.11</td>
    </tr>
    <tr>
      <th>29-32</th>
      <td>$1.99</td>
      <td>4</td>
      <td>$7.97</td>
    </tr>
    <tr>
      <th>33-36</th>
      <td>$2.93</td>
      <td>7</td>
      <td>$20.48</td>
    </tr>
    <tr>
      <th>37-40</th>
      <td>$3.82</td>
      <td>3</td>
      <td>$11.46</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders
Top_Spenders=Heroes_df.groupby(['SN'])
Average_Price=Top_Spenders["Price"].sum()/Top_Spenders["Price"].count()
Total_Price=Top_Spenders["Price"].sum()
total_count=Heroes_df["SN"].value_counts()


Top_Spenders_df=pd.DataFrame({"Purchase Count": total_count,"Total Purchase Value":Total_Price,"Average Purchase Price":Average_Price})
Top_Spenders_df.sort_values(["Total Purchase Value"],ascending=False,inplace=True)
Top_Spenders_df["Average Purchase Price"]=Top_Spenders_df["Average Purchase Price"].map("${:.2f}".format)
Top_Spenders_df["Total Purchase Value"]=Top_Spenders_df["Total Purchase Value"].map("${:.2f}".format)
Top_Spenders_df.head(5)
                
#Grouped_SN=Heroes_df.groupby(['SN'])
#sorted_SN=Grouped_SN.sort_values([""])
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sundaky74</th>
      <td>$3.71</td>
      <td>2</td>
      <td>$7.41</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>$2.56</td>
      <td>2</td>
      <td>$5.13</td>
    </tr>
    <tr>
      <th>Eusty71</th>
      <td>$4.81</td>
      <td>1</td>
      <td>$4.81</td>
    </tr>
    <tr>
      <th>Chanirra64</th>
      <td>$4.78</td>
      <td>1</td>
      <td>$4.78</td>
    </tr>
    <tr>
      <th>Alarap40</th>
      <td>$4.71</td>
      <td>1</td>
      <td>$4.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items
Top_Items=Heroes_df.groupby(["Item Name"])
total_count=Heroes_df["Item Name"].value_counts()
Individual_Price=Top_Items["Price"].sum()/total_count
Total_Price=Top_Items["Price"].sum()


Top_Items_df=pd.DataFrame({"Purchase count":total_count,"Total Purchase Value": Total_Price,"Item Price":Individual_Price})
Top_Items_df.sort_values(["Total Purchase Value"],ascending=False,inplace=True)
Top_Items_df["Item Price"]=Top_Items_df["Item Price"].map("${:.2f}".format)
Top_Items_df["Total Purchase Value"]=Top_Items_df["Total Purchase Value"].map("${:.2f}".format)
Top_Items_df.head(5)



```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Price</th>
      <th>Purchase count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mourning Blade</th>
      <td>$3.64</td>
      <td>3</td>
      <td>$10.92</td>
    </tr>
    <tr>
      <th>Heartstriker, Legacy of the Light</th>
      <td>$4.71</td>
      <td>2</td>
      <td>$9.42</td>
    </tr>
    <tr>
      <th>Apocalyptic Battlescythe</th>
      <td>$4.49</td>
      <td>2</td>
      <td>$8.98</td>
    </tr>
    <tr>
      <th>Betrayer</th>
      <td>$4.12</td>
      <td>2</td>
      <td>$8.24</td>
    </tr>
    <tr>
      <th>Feral Katana</th>
      <td>$4.11</td>
      <td>2</td>
      <td>$8.22</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Popular Item
Top_Items=Heroes_df.groupby(["Item Name"])
total_count=Heroes_df["Item Name"].value_counts()
Individual_Price=Top_Items["Price"].sum()/total_count
Total_Price=Top_Items["Price"].sum()


Top_Items_df=pd.DataFrame({"Purchase count":total_count,"Total Purchase Value": Total_Price,"Item Price":Individual_Price})
Top_Items_df.sort_values(["Purchase count"],ascending=False,inplace=True)

Top_Items_df["Item Price"]=Top_Items_df["Item Price"].map("${:.2f}".format)
Top_Items_df["Total Purchase Value"]=Top_Items_df["Total Purchase Value"].map("${:.2f}".format)
Top_Items_df.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Price</th>
      <th>Purchase count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mourning Blade</th>
      <td>$3.64</td>
      <td>3</td>
      <td>$10.92</td>
    </tr>
    <tr>
      <th>Deadline, Voice Of Subtlety</th>
      <td>$1.29</td>
      <td>2</td>
      <td>$2.58</td>
    </tr>
    <tr>
      <th>Stormcaller</th>
      <td>$2.77</td>
      <td>2</td>
      <td>$5.54</td>
    </tr>
    <tr>
      <th>Relentless Iron Skewer</th>
      <td>$2.12</td>
      <td>2</td>
      <td>$4.24</td>
    </tr>
    <tr>
      <th>Apocalyptic Battlescythe</th>
      <td>$4.49</td>
      <td>2</td>
      <td>$8.98</td>
    </tr>
  </tbody>
</table>
</div>


