# DATS 6103 - INDIVIDUAL PROJECT - 1 

## ARUSHI KAPOOR 

### The purpose of this project is to explore the military spending of 10 nations, as assigned, for atleast five years of data no older than 2010. 
### The given project explores the military spending of United States of America, China, Russia, Germany, United Kingdom, France, Italy, Saudi Arabia, South Korea and Israel for the time period 2013 - 2019. 

### 1. SOURCE OF THE DATA 

The required datasets were procured from the Stockholm International Peace Research Institute's (SIPRI) Military Expenditure Database. The SIPRI Military Expenditure Database contains consistent time series on the military spending of countries for the period 1949–2019 and is based on open sources. 

For this project, the following datasets have been accessed from the source for analyses - 

1. Military expenditure by country, in millions of US$ at current prices and exchange rates, 1949-2019
2. Military expenditure by country as percentage of gross domestic product, 1949-2019 
3. Military expenditure per capita  by country, 1988-2019

https://www.sipri.org/databases/milex 

### 2. READING, CLEANING & PRE - PROCESSING THE DATASETS 
The given datasets were read using pandas software library. For ease in data reading and indexing, the given excel files were converted into a csv format and then read into respective dataframes.


```python
# Converting the given datasets into a csv format.
import pandas as pd
pd.set_option("display.float.format", lambda x: "%.4f" % x)
milUSD=pd.read_excel("current_usd.xlsx")
milUSD.to_csv ("currentusd.csv")
milGDP=pd.read_excel("share_gdp.xlsx")
milGDP.to_csv ("sharegdp.csv")
milCapita=pd.read_excel("per_capita.xlsx")
milCapita.to_csv ("percapita.csv")
```

### The csv formatted datasets were loaded into dataframes as shown below. It is important to note the following: 

1. The milUSD dataframe represents Military expenditure by country in US$ 
2. The milGDP dataframe represents Military expenditure by country as a percentage of gross domestic product 
3. The milCapita dataframe represents Military expenditure per capita by country 

### Since our analyses focus just on 10 nations for the years 2013 - 2019, the same is assigned into variables 'countries' and 'years' respectively. Then, a function titled, 'display_relevant' is created to filter the three datasets as per the requirements. 



```python
# Selecting the relevant columns and rows by assigning them to the given variables. 
countries = ["USA", "China", "Russia", "Germany", "UK", "France", "Italy", "Saudi Arabia", "Korea, South", "Israel"]
years = ["2013", "2014", "2015", "2016", "2017", "2018", "2019"]
```


```python
# Filtering the data using the given function as per analyses requirements. 
def display_relevant(dataset, countries, years):
    data = pd.read_csv(dataset).set_index('Country')
    filtered_data=data.loc[countries,years]
    filtered_data=filtered_data.applymap(lambda x: float(x))
    return filtered_data

milUSD=display_relevant('currentusd.csv',countries,years)
milGDP=display_relevant('sharegdp.csv',countries, years)
milCapita=display_relevant('percapita.csv',countries,years)
```

### The values of milGDP dataset are multiplied by 100 to obtain the relevant percentage values. 


```python
# Multiplying the values by 100 to obtain percentage values.
milGDP = milGDP*100 
milGDP 
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
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
      <th>2018</th>
      <th>2019</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
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
      <th>USA</th>
      <td>4.0467</td>
      <td>3.6959</td>
      <td>3.4778</td>
      <td>3.4189</td>
      <td>3.3134</td>
      <td>3.3162</td>
      <td>3.4131</td>
    </tr>
    <tr>
      <th>China</th>
      <td>1.8669</td>
      <td>1.9058</td>
      <td>1.9105</td>
      <td>1.9300</td>
      <td>1.8960</td>
      <td>1.8963</td>
      <td>1.8886</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>3.8462</td>
      <td>4.1042</td>
      <td>4.8628</td>
      <td>5.4524</td>
      <td>4.2334</td>
      <td>3.7242</td>
      <td>3.8786</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>1.2019</td>
      <td>1.1384</td>
      <td>1.1017</td>
      <td>1.1461</td>
      <td>1.1636</td>
      <td>1.1783</td>
      <td>1.2795</td>
    </tr>
    <tr>
      <th>UK</th>
      <td>2.0650</td>
      <td>1.9488</td>
      <td>1.8596</td>
      <td>1.8108</td>
      <td>1.7666</td>
      <td>1.7660</td>
      <td>1.7435</td>
    </tr>
    <tr>
      <th>France</th>
      <td>1.8499</td>
      <td>1.8630</td>
      <td>1.8723</td>
      <td>1.9173</td>
      <td>1.9105</td>
      <td>1.8510</td>
      <td>1.8572</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>1.4061</td>
      <td>1.2874</td>
      <td>1.2106</td>
      <td>1.3395</td>
      <td>1.3646</td>
      <td>1.3409</td>
      <td>1.3514</td>
    </tr>
    <tr>
      <th>Saudi Arabia</th>
      <td>8.9761</td>
      <td>10.6779</td>
      <td>13.3257</td>
      <td>9.8727</td>
      <td>10.2238</td>
      <td>9.5082</td>
      <td>7.9798</td>
    </tr>
    <tr>
      <th>Korea, South</th>
      <td>2.5030</td>
      <td>2.5299</td>
      <td>2.4950</td>
      <td>2.4596</td>
      <td>2.4215</td>
      <td>2.5030</td>
      <td>2.6736</td>
    </tr>
    <tr>
      <th>Israel</th>
      <td>5.5732</td>
      <td>5.7450</td>
      <td>5.4970</td>
      <td>5.4778</td>
      <td>5.5285</td>
      <td>5.3448</td>
      <td>5.2577</td>
    </tr>
  </tbody>
</table>
</div>



### Now that we have filtered each of the datasets, we stack them and form one dataset titled 'Complete'. We assign the variables 'Country' and 'Year' as indices of the given dataset.  This is a MultiIndex dataset. 


```python
# Stacking the milUSD, milGDP and milCapita datasets to form one dataframe titled 'Complete'. The variables 'Country' and 'Year'
# have been assigned as the indices of the dataframe. 
Complete=pd.DataFrame()
Complete['milUSD']=milUSD.stack()
Complete['milGDP']=milGDP.stack()
Complete['milCapita']=milCapita.stack()
Complete = Complete.rename_axis(index = ['Country','Year'])
```


```python
Complete.head()
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
      <th>milUSD</th>
      <th>milGDP</th>
      <th>milCapita</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">USA</th>
      <th>2013</th>
      <td>679229.0000</td>
      <td>4.0467</td>
      <td>2146.7378</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>647789.0000</td>
      <td>3.6959</td>
      <td>2032.7676</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>633829.6390</td>
      <td>3.4778</td>
      <td>1975.2960</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>639856.4430</td>
      <td>3.4189</td>
      <td>1980.8816</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>646752.9270</td>
      <td>3.3134</td>
      <td>1989.4902</td>
    </tr>
  </tbody>
</table>
</div>



### Now that the dataset is cleaned, new variables are created for analyses. The new variables are as follows -

1. Total GDP, denoted by **totGDP**, by = $ \frac{Total \ Military \ Expenditure}{\frac{Military \ Expenditure \ as \ a \ Share \ of \ GDP}{100}}$

<br />

2. Total Population, denoted by **totPOP**, by = $\frac{Total \ Military \ Expenditure}{Per \ Capita \ Military \ Spending}$

<br />

3. GDP per Capita denoted by **gdpCapita**, by = $\frac{Total \ GDP}{Total \ Population}$

<br />

4. Ratio of Per Capita Military Spending to Per Capita GDP as an absolute value, denoted by **CapitaRatio_Absolute**, by = $\frac {Per \ Capita \ Military \ Spending}{Per \ Capita \ GDP}$ 

<br />

5. Ratio of Per Capita Military Spending to Per Capita GDP as a percent value, denoted by **CapitaRatio_%**, by = $\frac {Per \ Capita \ Military \ Spending}{Per \ Capita \ GDP} * 100$ 

<br />

6. Overall Growth from 2013 to 2019 in absolute values, denoted by **Overall Growth_Absolute**, by = $\frac{Total \ Military \ Expenditure \ of \ 2019 - Total \ Military \ Expenditure \ of \ 2013}{Total \ Military \ Expenditure \ of \ 2013}$

<br />

7. Overall Growth from 2013 to 2019 in percent values, denoted by **Overall Growth_%**, by = $\frac{Total \ Military \ Expenditure \ of \ 2019 - Total \ Military \ Expenditure \ of \ 2013}{Total \ Military \ Expenditure \ of \ 2013} * 100$


```python
# Creating new variables required for analyses.
Complete['totPOP']=Complete['milUSD']/Complete['milCapita']
Complete['totGDP'] = Complete['milUSD']/(Complete['milGDP']/100)
Complete['gdpCapita']=Complete['totGDP']/Complete['totPOP']
Complete['CapitaRatio_Absolute'] = Complete['milCapita']/Complete['gdpCapita']
Complete['CapitaRatio_%'] = Complete['milCapita']/Complete['gdpCapita']*100
Complete['Overall Growth_Absolute'] = Complete.groupby('Country')['milUSD'].pct_change(periods=6)
Complete['Overall Growth_%'] = Complete.groupby('Country')['milUSD'].pct_change(periods=6)*100
```


```python
# Printing a slice of the Complete dataframe.
Complete.loc['Russia']
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
      <th>milUSD</th>
      <th>milGDP</th>
      <th>milCapita</th>
      <th>totPOP</th>
      <th>totGDP</th>
      <th>gdpCapita</th>
      <th>CapitaRatio_Absolute</th>
      <th>CapitaRatio_%</th>
      <th>Overall Growth_Absolute</th>
      <th>Overall Growth_%</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>2013</th>
      <td>88352.8965</td>
      <td>3.8462</td>
      <td>612.1782</td>
      <td>144.3255</td>
      <td>2297128.1932</td>
      <td>15916.3065</td>
      <td>0.0385</td>
      <td>3.8462</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>84696.5047</td>
      <td>4.1042</td>
      <td>585.4671</td>
      <td>144.6648</td>
      <td>2063663.3624</td>
      <td>14265.1345</td>
      <td>0.0410</td>
      <td>4.1042</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>66418.3268</td>
      <td>4.8628</td>
      <td>458.1046</td>
      <td>144.9851</td>
      <td>1365857.1007</td>
      <td>9420.6749</td>
      <td>0.0486</td>
      <td>4.8628</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>69245.3095</td>
      <td>5.4524</td>
      <td>476.6486</td>
      <td>145.2754</td>
      <td>1269995.3558</td>
      <td>8741.9865</td>
      <td>0.0545</td>
      <td>5.4524</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>66527.3040</td>
      <td>4.2334</td>
      <td>457.1378</td>
      <td>145.5301</td>
      <td>1571483.6344</td>
      <td>10798.3416</td>
      <td>0.0423</td>
      <td>4.2334</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>61387.5470</td>
      <td>3.7242</td>
      <td>421.2300</td>
      <td>145.7340</td>
      <td>1648348.5642</td>
      <td>11310.6631</td>
      <td>0.0372</td>
      <td>3.7242</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>65102.5697</td>
      <td>3.8786</td>
      <td>446.2985</td>
      <td>145.8723</td>
      <td>1678511.9886</td>
      <td>11506.7251</td>
      <td>0.0388</td>
      <td>3.8786</td>
      <td>-0.2632</td>
      <td>-26.3153</td>
    </tr>
  </tbody>
</table>
</div>



### 3. VISUALIZING THE DATA

### For visualization purposes, Seaborn and Matplotlib software packages are applied. Visualization will allow us to derive meaningful conclusions in regards to a nation's military expenditure. 


```python
# Loading the required software libraries for graphing purposes.
import warnings
warnings.filterwarnings('ignore')
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
```

#### 3.1 Comparing the military data to that country’s GDP


```python
# Creating a lineplot graph to compare military spending as a share of GDP for each country for 2013 - 2019. 
# Assigning dimensions to the graph 
fig, ax = plt.subplots(figsize=(10, 7))
# Assigning variables to be denoted on the x-axis and y-axis
sns.lineplot(x ='Year' , y = 'milGDP', data=Complete.reset_index(), hue='Country', ax=ax)
# Displaying the required legend outside the graph
plt.legend(bbox_to_anchor=(1, 1))
# Assigning the required label to the graph
plt.ylabel("Military Spending as a % Share of GDP")
# Assigning title to the graph
plt.title('Military Spending of each Country as a Share of GDP, 2013 - 2019')
# Displaying the graph
plt.show()
```


![png](output_files/output_21_0.png)


#### Key Findings 

1. We observe that as compared to other nations, Saudi Arabia's military expenditure as a percentage share of GDP, is the highest. Germany's military expenditure as a percentage share of GDP is the lowest.  


2. Saudi Arabia's military expenditure increased sharply for the period of 2014 to 2015. This observation can be owed to a military campaign led by the nation against rebels in the neighboring country of Yemen during that time. 


3. Israel's military expenditure as a share of its GDP seems to be consistent throughout the given duration. A similar trend is observed in South Korea, UK and European Union nations. 


4. Russia's military expenditure as a share of its GDP increased in 2014, This could be due to the conflict between Russia and Ukraine that began in February 2014. A drop in the same is observed from 2016 onwards, which was due to President Putin's decision to re-allocate funds to improve living standards and social care for the nation's people. 


```python
# Creating a for loop to display graphs for each country to compare military expenditure and GDP. 
for i in countries:
    # Slicing the columns required for graphing
    data = Complete.loc[i][['milUSD', 'totGDP']].reset_index()
    # Assigning graph dimensions
    fig, ax1 = plt.subplots(figsize=(7, 7))
    # Assigning military expenditure in USD on y-axis 1 and denoting the same by color blue
    ax1.plot(data['Year'],data['milUSD'], color="blue")
    # Assigning the label to y-axis 1
    ax1.set_ylabel("Military Expenditure in millions USD", color="blue")
    # Assigning the label to x-axis
    ax1.set_xlabel("Year")
    # Assigning twin y-axis 2
    ax2 = ax1.twinx()
    # Assigning total GDP in USD on y-axis 2 and denoting the same by color red
    ax2.plot(data['Year'],data['totGDP'], color="red")
    # Assigning the label to y-axis 1
    ax2.set_ylabel("Total GDP in millions USD", color="red")
    # Removing the scientific notation on y-axes
    plt.ticklabel_format(style='plain',axis='y')
    # Assigning title to the graph
    plt.title("Comparing military data to the country's GDP: {}".format(i))
# Displaying the graph for each country 
plt.show()
```


![png](output_files/output_24_0.png)



![png](output_files/output_24_1.png)



![png](output_files/output_24_2.png)



![png](output_files/output_24_3.png)



![png](output_files/output_24_4.png)



![png](output_files/output_24_5.png)



![png](output_files/output_24_6.png)



![png](output_files/output_24_7.png)



![png](output_files/output_24_8.png)



![png](output_files/output_24_9.png)


#### Key Findings 

We observe the following - 

1. A strong positive correlation exists between China's GDP and military expenditure throughout the given period. 
   
   
2. While Saudi Arabia's GDP observed a sharp decrease from 2014 to 2015, its military expenditure observed a significant increase and was the highest among 2013 - 2019. 


3. USA's military expenditure observed a notable decrease from 2014 to 2017 but increased significantly since 2017. 


4. France, UK and Italy have observed a significant decrease in both GDP and military expenditure since 2018. 


5. A positive correlation exists between the GDP and military expenditure of both Israel and South Korea from 2015 till 2018. However, in 2018,  South Korea's GDP dipped while its military expenditure continued to remain mostly consistent. A similar trend can be observed in Germany too. 


6. Russia's GDP has increased since 2016. However, its military expenditure took a dip in the same year but rose again in 2018. 


#### 3.2 Comparing the overall military spending of the all 10 countries in absolute and percentages

#### 3.2.a. Absolute Values in Barplot 


```python
# Creating a barplot graph to compare overall military spending in absolute values of all the 10 countries for 2013 - 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.barplot(x ='Year' , y = 'milUSD', data=Complete.reset_index(), hue='Country', ax=ax)
plt.legend(bbox_to_anchor=(1, 1))
plt.ylabel("Military Spending in millions of USD")
plt.title('Military Spending of each Country in Absolute Values, 2013 - 2019')
plt.show()
```


![png](output_files/output_29_0.png)


#### 3.2.b. Percentage Values in Barplot


```python
# Creating a barplot graph to compare overall military spending as a share of GDP of all the 10 countries for 2013 - 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.barplot(x = 'Year', y = 'milGDP', data=Complete.reset_index(), hue='Country', ax=ax)
plt.legend(bbox_to_anchor=(1, 1))
plt.ylabel("Military Spending as a % Share of GDP")
plt.title('Military Spending of each Country as a Share of GDP, 2013 - 2019')
plt.show()
```


![png](output_files/output_31_0.png)


#### Key Findings

We can observe the following - 

1. In absolute values, United States of America has incurred the highest military expenditure in USD for the given duration, 2013 - 2019. China ranks second. Israel ranks the lowest. 


2. Military expenditure as a percentage share of GDP, is observed to be highest for Saudi Arabia for the given duration, 2013 - 2019, followed by Israel. Germany ranks the lowest. 


#### 3.3 Comparing the per person military spending to the per person GDP in absolute and percentages

#### 3.3.a. Absolute Values in Lineplot


```python
# Creating a lineplot graph to compare per capita military spending in absolute values of each country for 2013 - 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.lineplot(data=Complete.reset_index(), hue='Country', x='Year', y='milCapita', ax=ax)
plt.legend(bbox_to_anchor=(1, 1))
plt.ylabel("Per Capita Military Spending in USD")
plt.title('Per Capita Military Spending for each Country, 2013 - 2019')
plt.show()
```


![png](output_files/output_36_0.png)


#### Key Findings

We can observe the following - 

1. As compared to other nations, per capita military spending has been the highest in Saudi Arabia from 2013 to 2015. However, Israel overtook Saudi Arabia by the end of 2015 until 2019. 


2. It is interesting to note that though China's military expenditure in USD is second highest, its per capita military spending is the lowest as compared to other nations. 


3. Since 2018, USA ranks the second in per capita military spending. This could be attributed to the 2018 Defense Budget which was assigned by the President authorizing a 2.4% increase in military pay and a 0.7% increase in Basic Allowance for Housing.


4. Italy, Russia and Germany have a similar per capita military spending throughout the years. The same can be observed for South Korea, France and UK. However, South Korea, France and UK have a higher per capita military spending than Italy, Russia and Germany. 


```python
# Creating a lineplot graph to compare per capita GDP in absolute values of each country for 2013 - 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.lineplot(data=Complete.reset_index(), hue='Country', x='Year', y='gdpCapita', ax=ax)
plt.legend(bbox_to_anchor=(1, 1))
plt.ylabel("Per Capita GDP in USD")
plt.title('Per Capita GDP for each Country, 2013 - 2019')
plt.show()
```


![png](output_files/output_39_0.png)


#### Key Findings 

We can observe the following - 

1. Since 2013, USA's per capita GDP has been the highest among the given nations, followed by Germany. 


2. Since 2013, China's per capita GDP has been the lowest among the given nations. Russia's per capita GDP is second lowest. 


```python
# Creating a lineplot graph to compare the ratio of per capita military spending to per capita GDP in absolute values of each country for 2013 - 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.lineplot(data=Complete.reset_index(), hue='Country', x='Year', y='CapitaRatio_Absolute', ax=ax)
plt.legend(bbox_to_anchor=(1, 1))
plt.ylabel("Ratio in Absolute Values")
plt.title('Ratio of Per Capita Military Spending to Per Capita GDP for each Country, 2013 - 2019')
plt.show()
```


![png](output_files/output_42_0.png)


#### 3.3.b. Percentage Values in Barplot


```python
# Creating a barplot graph to compare the ratio of per capita military spending to per capita GDP in % values of each country 
# for 2013 - 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.barplot(data=Complete.reset_index(), hue='Country', x='Year', y='CapitaRatio_%', ax=ax)
plt.legend(bbox_to_anchor=(1, 1))
plt.ylabel("Ratio in % Values")
plt.title('Ratio of Per Capita Military Spending to Per Capita GDP of each Country (%), 2013 - 2019')
plt.show()
```


![png](output_files/output_44_0.png)


#### Key Findings 

We observe the following - 

1. The striking observation is that the above graph is same as the graphs for military spending as a share of GDP over the years. 


2.  Saudi Arabia leads the nations with the highest ratio of per capita military spending to per capita GDP. Saudi Arabia's ratio of per capita military spending to per capita GDP sharply rose from 2013 till 2015. This can be due to the military campaign led by the nation against rebels in the neighboring country of Yemen during that time.


3. Israel ranks the second highest. This can be attributed to the military assistance provided by the United States to Israel. Israel's ratio of per capita military spending to per capita seems to be consistent throughout the given duration. 


4. Russia's ratio of per capita military spending to per capita GDP sharply rose in 2014. This could be due to the conflict between Russia and Ukraine that began in February 2014. A drop in the same is observed from 2016 onwards, which was due to President Putin's decision to re-allocate funds to improve living standards and social care for the nation's people. Russia's ratio of per capita military spending to per capita GDP has been high until 2016. However, a drop in the same is observed from 2016 onwards, which can be attributed to President Putin's decision to re-allocate funds to improve living standards and social care for the nation's people. 


5. The ratio of per capita military spending to per capita GDP for South Korea has been consistent throughout. It is higher than those of UK and the European nations.  


4. The ratio of per capita military spending to the ratio of GDP is consistent over the years in UK and the European Union nations. 

#### 3.4 Growth

#### 3.4.a. Overall Growth in Absolute Values in Barplot


```python
# Comparing each country's overall growth in military expenditure in absolute values from 2013 to 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.barplot(x ='Country' , y = 'Overall Growth_Absolute', data=Complete.reset_index(), ax=ax)
plt.ylabel("Overall Growth in Absolute Values")
plt.title('Overall Growth in Military Expenditure for each Country, 2013 - 2019')
plt.show()
```


![png](output_files/output_49_0.png)


#### 3.4.b. Overall Growth in Percent Values in Barplot 


```python
# Comparing each country's overall growth in military expenditure in % values from 2013 to 2019. 
fig, ax = plt.subplots(figsize=(10, 7))
sns.barplot(x = 'Country' , y = 'Overall Growth_%', data=Complete.reset_index(), ax=ax)
plt.ylabel("Overall Growth in Absolute Values")
plt.title('Overall Growth in Military Expenditure for each Country, 2013 - 2019')
plt.show()
```


![png](output_files/output_51_0.png)


#### Key Findings

We observe the following - 

1. China exhibits the maximum growth in military spending overall. South Korea ranks the second. 


2. Russia's military expenditure has shrunk the most overall. 


5. USA, Germany and Israel's military expenditure have shown a positive change overall. 


6. UK, France and Italy's military expenditure show a negative change overall. 

#### The fastest growing country in terms of both absolute and percentage values is China. South Korea ranks second. 

#### 3.5 Predictions & Correlations

#### 3.5.a. Correlation between Military Expenditure and Total GDP 


```python
# Creating a pairplot to explore relationships between total GDP, military expenditure in USD and per capita military spending 
# for each country from 2013 to 2019. 
sns.pairplot(data = Complete.reset_index() ,hue= 'Country', vars=['totGDP', 'milGDP', 'milCapita'])
plt.show()
```


![png](output_files/output_57_0.png)


#### Key Findings 

We can classify Israel and Saudi Arabia into one group. European Nations (France, Italy and Germany), UK, South Korea and Russia together into another group. China and USA are perceived to be as outliers. 

1. We observe that Saudi Arabia's military expenditure as a share of GDP has been increasing while the total GDP remains constant. Similarly, we observe that the nation's per capita military spending has been increasing while total GDP remains constant. We observe a similar trend in Israel too. 


2. We observe that while China's total GDP increases, it's military expenditure as a share of GDP has been constant. However, there exists a positive correlation between its per capita military spending and total GDP over the years. 


3. We don't observe a positive correlation between military expenditure as a share of GDP and total GDP in the USA. Both USA's total GDP and per capita military spending has increased over the last couple years.


4. We don't observe a significant relationship between per capita military spending and military spending as a share of GDP in Italy, UK, Germany, France and South Korea. Russia's military expenditure as a share of GDP has increased while its total GDP remains consistent over the years. It's per capita military spending has remained consistent while its military spending as a share of GDP has increased slightly over the last few years. 

#### 3.5.b. Forecasting China's Growth 

#### For this part of the project, the following packages were installed -

!conda install -c conda-forge fbprophet -y


conda install libpython m2w64-toolchain -c msys2


pip install pystan


pip install fbprophet

The following source was used to learn more about Prophet and its installation process - 

https://facebook.github.io/prophet/docs/installation.html#python


https://facebook.github.io/prophet/docs/quick_start.html



```python
# Installing the required packages

!conda install -c conda-forge fbprophet -y
```

    Collecting package metadata (current_repodata.json): ...working... done
    Solving environment: ...working... done
    
    # All requested packages already installed.
    
    


```python
conda install libpython m2w64-toolchain -c msys2
```

    Collecting package metadata (current_repodata.json): ...working... done
    Solving environment: ...working... done
    
    # All requested packages already installed.
    
    
    Note: you may need to restart the kernel to use updated packages.
    


```python
pip install pystan
```

    Requirement already satisfied: pystan in c:\users\annak\anaconda3\lib\site-packages (2.19.1.1)
    Requirement already satisfied: Cython!=0.25.1,>=0.22 in c:\users\annak\anaconda3\lib\site-packages (from pystan) (0.29.17)
    Requirement already satisfied: numpy>=1.7 in c:\users\annak\anaconda3\lib\site-packages (from pystan) (1.18.5)
    Note: you may need to restart the kernel to use updated packages.
    


```python
pip install fbprophet
```

    Requirement already satisfied: fbprophet in c:\users\annak\anaconda3\lib\site-packages (0.7.1)
    Requirement already satisfied: holidays>=0.10.2 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (0.10.3)
    Requirement already satisfied: convertdate>=2.1.2 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (2.2.2)
    Requirement already satisfied: python-dateutil>=2.8.0 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (2.8.1)
    Requirement already satisfied: cmdstanpy==0.9.5 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (0.9.5)
    Requirement already satisfied: pandas>=1.0.4 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (1.0.5)
    Requirement already satisfied: LunarCalendar>=0.0.9 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (0.0.9)
    Requirement already satisfied: matplotlib>=2.0.0 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (3.2.2)
    Requirement already satisfied: numpy>=1.15.4 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (1.18.5)
    Requirement already satisfied: Cython>=0.22 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (0.29.17)
    Requirement already satisfied: setuptools-git>=1.2 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (1.2)
    Requirement already satisfied: pystan>=2.14 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (2.19.1.1)
    Requirement already satisfied: tqdm>=4.36.1 in c:\users\annak\anaconda3\lib\site-packages (from fbprophet) (4.47.0)
    Requirement already satisfied: six in c:\users\annak\anaconda3\lib\site-packages (from holidays>=0.10.2->fbprophet) (1.15.0)
    Requirement already satisfied: korean-lunar-calendar in c:\users\annak\anaconda3\lib\site-packages (from holidays>=0.10.2->fbprophet) (0.2.1)
    Requirement already satisfied: pymeeus<=1,>=0.3.6 in c:\users\annak\anaconda3\lib\site-packages (from convertdate>=2.1.2->fbprophet) (0.3.7)
    Requirement already satisfied: pytz>=2014.10 in c:\users\annak\anaconda3\lib\site-packages (from convertdate>=2.1.2->fbprophet) (2020.1)
    Requirement already satisfied: ephem>=3.7.5.3 in c:\users\annak\anaconda3\lib\site-packages (from LunarCalendar>=0.0.9->fbprophet) (3.7.7.1)
    Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in c:\users\annak\anaconda3\lib\site-packages (from matplotlib>=2.0.0->fbprophet) (2.4.7)
    Requirement already satisfied: kiwisolver>=1.0.1 in c:\users\annak\anaconda3\lib\site-packages (from matplotlib>=2.0.0->fbprophet) (1.2.0)
    Requirement already satisfied: cycler>=0.10 in c:\users\annak\anaconda3\lib\site-packages (from matplotlib>=2.0.0->fbprophet) (0.10.0)
    Note: you may need to restart the kernel to use updated packages.
    

In this section, Prophet has been used to predict future values of China's military expenditure in USD.

First, Prophet is imported from the library fbprophet. It is required that the years of the dataset are converted to a datetime format so that the same can be read by Prophet easily for prediction purposes.


```python
# Importing Prophet and datetime packages. 
from fbprophet import Prophet
import datetime
```

Total military expenditure in USD along with the corresponding years is sliced for China. 


```python
# Slicing China's military expenditure for the given years from the Complete dataframe. 
China=Complete.loc['China']['milUSD'].reset_index()
```

The Year variable column is transformed into the datetime and year end format.  


```python
# Setting the year to a datetime format; for analysis purposes, it has been assumed that the given military expenditure values 
# for each year were obtained on the last day of the year 
China['Year'] = pd.DatetimeIndex(China['Year'])
China['Year'] = China['Year'] + pd.offsets.YearEnd(0) 
```


```python
China
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
      <th>Year</th>
      <th>milUSD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013-12-31</td>
      <td>179880.4514</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-12-31</td>
      <td>200772.2038</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-12-31</td>
      <td>214471.4957</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-12-31</td>
      <td>216404.2830</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-31</td>
      <td>228466.2700</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018-12-31</td>
      <td>253491.5361</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-12-31</td>
      <td>261081.9404</td>
    </tr>
  </tbody>
</table>
</div>



Prophet requires that the input columns be named ds and y. 


```python
# Renaming the columns 
China = China.rename(columns={'Year': 'ds','milUSD': 'y'})
```


```python
China
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
      <th>ds</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013-12-31</td>
      <td>179880.4514</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-12-31</td>
      <td>200772.2038</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-12-31</td>
      <td>214471.4957</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-12-31</td>
      <td>216404.2830</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-31</td>
      <td>228466.2700</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018-12-31</td>
      <td>253491.5361</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-12-31</td>
      <td>261081.9404</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Fitting the model 
model = Prophet()
model.fit(China)
```

    INFO:fbprophet:Disabling weekly seasonality. Run prophet with weekly_seasonality=True to override this.
    INFO:fbprophet:Disabling daily seasonality. Run prophet with daily_seasonality=True to override this.
    INFO:fbprophet:n_changepoints greater than number of observations. Using 4.
    




    <fbprophet.forecaster.Prophet at 0x24bb44be7c0>



Predictions are then made on the dataframe with renamed columns. Prophet.make_future_dataframe creates a dataframe that extends into the future a specified number of periods. In the following code, the periods refers to the number of years and frequency refers to the type of duration into the future for which the predictions have to be made. By default, the dates from the history are included too. This further allows us to see the fit of the model. 


```python
# Creating a future dataframe 
future_predictions = model.make_future_dataframe(periods=3, freq='Y')
```

Prophet returns a dataframe with the following columns - 

1. ds: the date of the forecasted value


2. yhat: the forecasted value of the total military expenditure in USD (milUSD)


3. yhat_lower: the lower value of the forecasts


4. yhat_upper: the upper value of the forecasts


```python
# Creating a dataframe with the forecasted values 
forecast = model.predict(future_predictions)
forecast[['ds', 'yhat', 'yhat_lower', 'yhat_upper']]
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
      <th>ds</th>
      <th>yhat</th>
      <th>yhat_lower</th>
      <th>yhat_upper</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013-12-31</td>
      <td>182295.3292</td>
      <td>178561.2288</td>
      <td>185926.7536</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-12-31</td>
      <td>198838.6671</td>
      <td>195272.8590</td>
      <td>202468.9290</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-12-31</td>
      <td>213986.7927</td>
      <td>210249.0389</td>
      <td>217721.9163</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-12-31</td>
      <td>214448.5212</td>
      <td>210563.1794</td>
      <td>217925.8857</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-31</td>
      <td>232302.3063</td>
      <td>228516.8826</td>
      <td>236263.2188</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018-12-31</td>
      <td>248793.1398</td>
      <td>245175.9429</td>
      <td>252429.0775</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-12-31</td>
      <td>263912.6680</td>
      <td>259948.5495</td>
      <td>267498.2240</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2020-12-31</td>
      <td>264373.0728</td>
      <td>260595.5817</td>
      <td>267828.3595</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2021-12-31</td>
      <td>282226.8579</td>
      <td>278444.8000</td>
      <td>285955.2475</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2022-12-31</td>
      <td>298717.6914</td>
      <td>295072.0939</td>
      <td>302522.7159</td>
    </tr>
  </tbody>
</table>
</div>



Prophet plots the following - 

1. The actual / observed values represented by the black dots

2. The forecasted values represented by the blue line

3. The uncertainty intervals of the forecasts represented by the blue shaded regions.


```python
# Plotting the forecasts
forecast_figure = model.plot(forecast)
```


![png](output_files/output_83_0.png)


Based on the above graph, it can be concluded that the model is a good fit to predict China's military expenditure in USD. As seen above, the actual or observed values, repesented by black dots, are close to the forecasted values for the years 2013 to 2019. We expect China's military expenditure to remain stagnant until the end of 2021. However, we can expect a sharp growth in years 2021 and 2022. 

### 4. OVERALL CONCLUSION 

To conclude, it can be stated that we can expect China's total military expenditure to grow in the future. On the other hand, UK, Germany, France and Italy are expected to remain consistent in their military expenditure. South Korea and Israel's total military expenditure can be expected to remain consistent too. In USA, external factors can influence the nation's military spending in the future. For instance, if a change occurs in the current administration due to the 2020 Presidential Elections, a change can be expected in the nation's plans for its military spending. Like USA, Saudi Arabia's and Russia's military expenditure is dependent mostly on the country's administration's decisions rather than variables such as GDP. 

### 5. LEARNING PROCESS

The learning process has been both interesting and challenging. The most important lesson that I have learned is one can always dive deeper to generate meaningful insights. Through this project, I have become well-versed with the concepts of merging and stacking datasets, visualizing using seaborn and forecasting data values. 

### Thank you
