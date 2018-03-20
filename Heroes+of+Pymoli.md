

```python
import pandas as pd 
import numpy as np
import math
```


```python
df = pd.read_json('purchase_data.json')
#df.sort_values('Item ID').iloc[380:450]
df.head()
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total number of players

df['SN'].nunique()
```




    573




```python
#number of unique items                 
print(df['Item Name'].nunique())
#print(hi)
#print(df['Item ID'].count())

#average purchase price
print(df['Price'].mean())  

#total number of purchases
print(len(df))

#total revenue
print(df['Price'].sum())

```

    179
    2.931192307692303
    780
    2286.3299999999963



```python

```


```python

```


```python
#count of players
gen['Player Count'] = df.groupby('Gender').SN.nunique().to_frame()

#Percentage of players
gen['Percentage of Players'] = (df['Gender'].value_counts() / len(df)).to_frame()

gen
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
      <th>Price</th>
      <th>Count of Players</th>
      <th>Percentage of Players</th>
      <th>Average Purchase</th>
      <th>Total Purchase Value</th>
      <th>Player Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>136</td>
      <td>0.174359</td>
      <td>2.815515</td>
      <td>382.91</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>633</td>
      <td>0.811538</td>
      <td>2.950521</td>
      <td>1867.68</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>11</td>
      <td>0.014103</td>
      <td>3.249091</td>
      <td>35.74</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
#The below each broken by gender 


#Purchase Count
gen = df.groupby('Gender').Price.count().to_frame()
gen = gen.rename(columns={"Price": "Purchase Count"})

#count of players
gen['Player Count'] = df.groupby('Gender').SN.nunique().to_frame()

#Percentage of players
gen['Percentage of Players'] = (df['Gender'].value_counts() / len(df)).to_frame()

#Average Purchase 
gen['Average Purchase'] = df.groupby('Gender').Price.mean().to_frame()

#Total Purchase Value 
gen['Total Purchase Value'] = df.groupby('Gender').Price.sum()

gen

########################################################################
#seriously
#Normalized Totals # no idea wtf this means
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
      <th>Purchase Count</th>
      <th>Player Count</th>
      <th>Percentage of Players</th>
      <th>Average Purchase</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>100</td>
      <td>0.174359</td>
      <td>2.815515</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>465</td>
      <td>0.811538</td>
      <td>2.950521</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>8</td>
      <td>0.014103</td>
      <td>3.249091</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#chopchop = df
#chopchop.head()
```


```python
chopchop['Age Range'] = pd.cut(chopchop['Age'],np.arange(6, 4.0+48, 4),right=False)
#chop.drop('oldies')
chopchop.head()
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
      <th>Age Range</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>[38.0, 42.0)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>[18.0, 22.0)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>[34.0, 38.0)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>[18.0, 22.0)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>[22.0, 26.0)</td>
    </tr>
  </tbody>
</table>
</div>




```python
#purchase count
chop1 = chopchop.groupby('Age Range').Price.count().to_frame()
chop1 = chop1.rename(columns={"Price": "Purchase Count"})

# average purchase price
chop1['Mean'] = chopchop.groupby('Age Range').Price.mean().to_frame()

#Total Purchase Value
chop1['Total Purchase Value'] = chopchop.groupby('Age Range').Price.sum().to_frame()


chop1
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
      <th>Purchase Count</th>
      <th>Mean</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>[6.0, 10.0)</th>
      <td>28</td>
      <td>2.980714</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>[10.0, 14.0)</th>
      <td>29</td>
      <td>2.850000</td>
      <td>82.65</td>
    </tr>
    <tr>
      <th>[14.0, 18.0)</th>
      <td>93</td>
      <td>2.865376</td>
      <td>266.48</td>
    </tr>
    <tr>
      <th>[18.0, 22.0)</th>
      <td>187</td>
      <td>2.873209</td>
      <td>537.29</td>
    </tr>
    <tr>
      <th>[22.0, 26.0)</th>
      <td>262</td>
      <td>2.985649</td>
      <td>782.24</td>
    </tr>
    <tr>
      <th>[26.0, 30.0)</th>
      <td>58</td>
      <td>2.824310</td>
      <td>163.81</td>
    </tr>
    <tr>
      <th>[30.0, 34.0)</th>
      <td>56</td>
      <td>3.088036</td>
      <td>172.93</td>
    </tr>
    <tr>
      <th>[34.0, 38.0)</th>
      <td>36</td>
      <td>2.849722</td>
      <td>102.59</td>
    </tr>
    <tr>
      <th>[38.0, 42.0)</th>
      <td>28</td>
      <td>3.080000</td>
      <td>86.24</td>
    </tr>
    <tr>
      <th>[42.0, 46.0)</th>
      <td>3</td>
      <td>2.880000</td>
      <td>8.64</td>
    </tr>
    <tr>
      <th>[46.0, 50.0)</th>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```


```python
#WTF are normalized totals
```


```python
#Top $penders

#Purchase Count 
#Average Purchase 
#Purchase Value


toptop = chopchop
ts = toptop.groupby('SN').Price.sum().sort_values(ascending=False).to_frame()
ts = ts.rename(columns={"Price": "Total Purchase Value"})
ts['Average Purchase Price'] = toptop.groupby('SN').Price.mean().sort_values(ascending=False).to_frame()
ts['Purchase Count'] = toptop.groupby('SN').Price.count().sort_values(ascending=False).to_frame()
ts.head()
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
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
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
      <td>17.06</td>
      <td>3.412000</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>13.56</td>
      <td>3.390000</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>12.74</td>
      <td>3.185000</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>12.73</td>
      <td>4.243333</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>11.58</td>
      <td>3.860000</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
#most popular items
toptop = chopchop
toptop['Item Name'].value_counts()
popi = toptop.groupby('Item Name').size().sort_values(ascending=False).to_frame()
popi = popi.reset_index()
popi = popi.rename(columns={0: "Total Purchase Count"})
pop2 = toptop['Item ID'].drop_duplicates().to_frame()
pop2['Item Name'] = toptop['Item Name']
pop2['Price'] = toptop['Price']
pop2.reindex()

popcomb = popi.merge(pop2, on=['Item Name'])
popcomb['Total'] = popcomb['Total Purchase Count'] * popcomb['Price']
popcomb.head(7)

#Final critic has two different Item IDs 92 and 101 same with storm caller

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
      <th>Item Name</th>
      <th>Total Purchase Count</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>92</td>
      <td>1.36</td>
      <td>19.04</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>101</td>
      <td>4.62</td>
      <td>64.68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>39</td>
      <td>2.35</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>84</td>
      <td>2.23</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Stormcaller</td>
      <td>10</td>
      <td>30</td>
      <td>4.15</td>
      <td>41.50</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Stormcaller</td>
      <td>10</td>
      <td>180</td>
      <td>2.78</td>
      <td>27.80</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>175</td>
      <td>1.24</td>
      <td>11.16</td>
    </tr>
  </tbody>
</table>
</div>




```python
#most profitable items
popcomb.sort_values('Total',ascending=False).head()
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
      <th>Item Name</th>
      <th>Total Purchase Count</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>101</td>
      <td>4.62</td>
      <td>64.68</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Stormcaller</td>
      <td>10</td>
      <td>30</td>
      <td>4.15</td>
      <td>41.50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>34</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>115</td>
      <td>4.25</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Orenmir</td>
      <td>6</td>
      <td>32</td>
      <td>4.95</td>
      <td>29.70</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
