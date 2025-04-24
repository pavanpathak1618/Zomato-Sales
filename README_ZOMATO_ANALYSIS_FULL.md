# ZOMATA DATA ANALYSIS PROJECT.

## IMPORTING LIBRARIES. 


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## IMPORTING AND VIEWING THE DATAFRAME.


```python
df= pd.read_csv('Desktop/ZOMATO_SALES.csv')
df.head()
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
      <th>name</th>
      <th>online_order</th>
      <th>book_table</th>
      <th>rate</th>
      <th>votes</th>
      <th>approx_cost(for two people)</th>
      <th>listed_in(type)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jalsa</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>4.1/5</td>
      <td>775</td>
      <td>800</td>
      <td>Buffet</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spice Elephant</td>
      <td>Yes</td>
      <td>No</td>
      <td>4.1/5</td>
      <td>787</td>
      <td>800</td>
      <td>Buffet</td>
    </tr>
    <tr>
      <th>2</th>
      <td>San Churro Cafe</td>
      <td>Yes</td>
      <td>No</td>
      <td>3.8/5</td>
      <td>918</td>
      <td>800</td>
      <td>Buffet</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Addhuri Udupi Bhojana</td>
      <td>No</td>
      <td>No</td>
      <td>3.7/5</td>
      <td>88</td>
      <td>300</td>
      <td>Buffet</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Grand Village</td>
      <td>No</td>
      <td>No</td>
      <td>3.8/5</td>
      <td>166</td>
      <td>600</td>
      <td>Buffet</td>
    </tr>
  </tbody>
</table>
</div>



## DETERMINING THE DIMENSION OF THE DATAFRAME.


```python
df.shape
```




    (148, 7)



## SUMMARY OF DATAFRAME.


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 148 entries, 0 to 147
    Data columns (total 7 columns):
     #   Column                       Non-Null Count  Dtype 
    ---  ------                       --------------  ----- 
     0   name                         148 non-null    object
     1   online_order                 148 non-null    object
     2   book_table                   148 non-null    object
     3   rate                         148 non-null    object
     4   votes                        148 non-null    int64 
     5   approx_cost(for two people)  148 non-null    int64 
     6   listed_in(type)              148 non-null    object
    dtypes: int64(2), object(5)
    memory usage: 8.2+ KB


## DESCRIPTION OF DATAFRAME.


```python
df.describe()
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
      <th>votes</th>
      <th>approx_cost(for two people)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>148.000000</td>
      <td>148.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>264.810811</td>
      <td>418.243243</td>
    </tr>
    <tr>
      <th>std</th>
      <td>653.676951</td>
      <td>223.085098</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.750000</td>
      <td>200.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>43.500000</td>
      <td>400.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>221.750000</td>
      <td>600.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>4884.000000</td>
      <td>950.000000</td>
    </tr>
  </tbody>
</table>
</div>



## CONVERTING THE DATA-TYPE OF COLUMN - RATE.


```python
def handleRate(value):
    value=str(value).split('/')
    value=value[0]
    return float(value)

df['rate']=df['rate'].apply(handleRate)
print(df.head())
```

                        name online_order book_table  rate  votes  \
    0                  Jalsa          Yes        Yes   4.1    775   
    1         Spice Elephant          Yes         No   4.1    787   
    2        San Churro Cafe          Yes         No   3.8    918   
    3  Addhuri Udupi Bhojana           No         No   3.7     88   
    4          Grand Village           No         No   3.8    166   
    
       approx_cost(for two people) listed_in(type)  
    0                          800          Buffet  
    1                          800          Buffet  
    2                          800          Buffet  
    3                          300          Buffet  
    4                          600          Buffet  


## TYPE OF RESTAURANT.


```python
sns.countplot(x=df['listed_in(type)'])
plt.xlabel("Type of restaurant")
```




    Text(0.5, 0, 'Type of restaurant')




    
![png](output_14_1.png)
    


### CONCLUSION.
DINING IS PREFFERED BY GREATER NUMBER OF INDIVIDUALS.
## VOTES.


```python
grouped_data=df.groupby('listed_in(type)')['votes'].sum()
result=pd.DataFrame({'votes': grouped_data})
plt.plot(result, c="green", marker="o")
plt.xlabel("Type of Restaurant", c="red", size=20)
plt.ylabel("votes", c="red", size=20)
```




    Text(0, 0.5, 'votes')




    
![png](output_18_1.png)
    


### CONCLUSION.
MAJORITY OF VOTES ARE GIVEN TO DINING WHICH CONCLUDES IT IS THE MOST PREFFERED TYPE.
## RATINGS RECIEVED BY MAJORITY OF RESTAURANT.


```python
plt.hist(df['rate'], bins=5)
plt.title("Ratings Distribution")
plt.show()
```


    
![png](output_22_0.png)
    


### CONCLUSION.
MOJARITY OF RESTAURANTS HAVE RATING BETWEEN 3.75 TO 4.
## MOST PREFERRED RESTAURANTS BY COUPLE (DEPENDING ON AVERAGE COST).


```python
couple_data=df['approx_cost(for two people)']
sns.countplot(x=couple_data)
```




    <Axes: xlabel='approx_cost(for two people)', ylabel='count'>




    
![png](output_26_1.png)
    


### CONCLUSION.
COUPLES MOSTLY PREFER RESTAURANTS HAVING AN AVAERAGE COST OF 300.
## WHICH MODE RECIEVES HIGHER RATING ( ONLINE OR OFFLINE ).


```python
plt.figure(figsize=(6,6))
sns.boxplot(x='online_order', y='rate', data=df)
```




    <Axes: xlabel='online_order', ylabel='rate'>




    
![png](output_30_1.png)
    


### CONCLUSION.
OFFLINE ORDERS RECIEVE LOWER RATING AS COMPARED TO ONLINE ORDERS.
## 🟢 Insights & Conclusions:
ONLINE ORDERING:
A MAJORITY OF RESTAURANTS OFFER ONLINE ORDERING.
THIS COULD INDICATE A CUSTOMER PREFERENCE FOR DIGITAL CONVENIENCE.TABLE BOOKING:
FEWER RESTAURANTS OFFER TABLE BOOKING COMPARED TO ONLINE ORDERING.
SUGGESTS TABLE BOOKING MIGHT BE LIMITED TO MORE PREMIUM OR DINE-IN FOCUSED ESTABLISHMENTS.VOTES DISTRIBUTION:
MOST RESTAURANTS HAVE FEWER THAN 1000 VOTES.
A FEW POPULAR ONES HAVE VERY HIGH VOTE COUNTS, INDICATING A SKEWED DISTRIBUTION (SOME HIGHLY FAVORED PLACES).COST VS RATING:
NO STRICT CORRELATION BETWEEN COST AND RATING.
BOTH HIGH- AND LOW-COST RESTAURANTS CAN HAVE HIGH RATINGS, SUGGESTING QUALITY AND EXPERIENCE MATTER MORE THAN JUST PRICE.