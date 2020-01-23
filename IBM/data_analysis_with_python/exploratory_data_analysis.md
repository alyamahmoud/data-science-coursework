```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
```


```python
path = 'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/automobileEDA.csv'
df = pd.read_csv(path)
df.head(5)
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
      <th>symboling</th>
      <th>normalized-losses</th>
      <th>make</th>
      <th>aspiration</th>
      <th>num-of-doors</th>
      <th>body-style</th>
      <th>drive-wheels</th>
      <th>engine-location</th>
      <th>wheel-base</th>
      <th>length</th>
      <th>...</th>
      <th>compression-ratio</th>
      <th>horsepower</th>
      <th>peak-rpm</th>
      <th>city-mpg</th>
      <th>highway-mpg</th>
      <th>price</th>
      <th>city-L/100km</th>
      <th>horsepower-binned</th>
      <th>diesel</th>
      <th>gas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>122</td>
      <td>alfa-romero</td>
      <td>std</td>
      <td>two</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
      <td>88.6</td>
      <td>0.811148</td>
      <td>...</td>
      <td>9.0</td>
      <td>111.0</td>
      <td>5000.0</td>
      <td>21</td>
      <td>27</td>
      <td>13495.0</td>
      <td>11.190476</td>
      <td>Medium</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>122</td>
      <td>alfa-romero</td>
      <td>std</td>
      <td>two</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
      <td>88.6</td>
      <td>0.811148</td>
      <td>...</td>
      <td>9.0</td>
      <td>111.0</td>
      <td>5000.0</td>
      <td>21</td>
      <td>27</td>
      <td>16500.0</td>
      <td>11.190476</td>
      <td>Medium</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>122</td>
      <td>alfa-romero</td>
      <td>std</td>
      <td>two</td>
      <td>hatchback</td>
      <td>rwd</td>
      <td>front</td>
      <td>94.5</td>
      <td>0.822681</td>
      <td>...</td>
      <td>9.0</td>
      <td>154.0</td>
      <td>5000.0</td>
      <td>19</td>
      <td>26</td>
      <td>16500.0</td>
      <td>12.368421</td>
      <td>Medium</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>164</td>
      <td>audi</td>
      <td>std</td>
      <td>four</td>
      <td>sedan</td>
      <td>fwd</td>
      <td>front</td>
      <td>99.8</td>
      <td>0.848630</td>
      <td>...</td>
      <td>10.0</td>
      <td>102.0</td>
      <td>5500.0</td>
      <td>24</td>
      <td>30</td>
      <td>13950.0</td>
      <td>9.791667</td>
      <td>Medium</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>164</td>
      <td>audi</td>
      <td>std</td>
      <td>four</td>
      <td>sedan</td>
      <td>4wd</td>
      <td>front</td>
      <td>99.4</td>
      <td>0.848630</td>
      <td>...</td>
      <td>8.0</td>
      <td>115.0</td>
      <td>5500.0</td>
      <td>18</td>
      <td>22</td>
      <td>17450.0</td>
      <td>13.055556</td>
      <td>Medium</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 29 columns</p>
</div>




```python
%%capture
! pip install seaborn
import seaborn as sns
%matplotlib inline
```


```python
print (df.dtypes)
```

    symboling              int64
    normalized-losses      int64
    make                  object
    aspiration            object
    num-of-doors          object
    body-style            object
    drive-wheels          object
    engine-location       object
    wheel-base           float64
    length               float64
    width                float64
    height               float64
    curb-weight            int64
    engine-type           object
    num-of-cylinders      object
    engine-size            int64
    fuel-system           object
    bore                 float64
    stroke               float64
    compression-ratio    float64
    horsepower           float64
    peak-rpm             float64
    city-mpg               int64
    highway-mpg            int64
    price                float64
    city-L/100km         float64
    horsepower-binned     object
    diesel                 int64
    gas                    int64
    dtype: object



```python
df["peak-rpm"].dtype
```




    dtype('float64')




```python
df[['horsepower', 'bore', 'stroke', 'compression-ratio']].corr()
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
      <th>horsepower</th>
      <th>bore</th>
      <th>stroke</th>
      <th>compression-ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>horsepower</th>
      <td>1.000000</td>
      <td>0.566936</td>
      <td>0.098462</td>
      <td>-0.214514</td>
    </tr>
    <tr>
      <th>bore</th>
      <td>0.566936</td>
      <td>1.000000</td>
      <td>-0.055390</td>
      <td>0.001263</td>
    </tr>
    <tr>
      <th>stroke</th>
      <td>0.098462</td>
      <td>-0.055390</td>
      <td>1.000000</td>
      <td>0.187923</td>
    </tr>
    <tr>
      <th>compression-ratio</th>
      <td>-0.214514</td>
      <td>0.001263</td>
      <td>0.187923</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.regplot(x=df['engine-size'], y=df['price'], data=df)
plt.ylim(0,)
```




    (0, 55866.25643530046)




![png](output_6_1.png)



```python
df[["engine-size", "price"]].corr()
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
      <th>engine-size</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>engine-size</th>
      <td>1.000000</td>
      <td>0.872335</td>
    </tr>
    <tr>
      <th>price</th>
      <td>0.872335</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.regplot(x=df["highway-mpg"], y=df["price"], data=df)
plt.ylim(0,)
```




    (0, 48308.51924515221)




![png](output_8_1.png)



```python
df[["highway-mpg", "price"]].corr()
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
      <th>highway-mpg</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>highway-mpg</th>
      <td>1.000000</td>
      <td>-0.704692</td>
    </tr>
    <tr>
      <th>price</th>
      <td>-0.704692</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.regplot(x=df["peak-rpm"], y=df["price"], data=df)
plt.ylim(0,)
```




    (0, 47436.148325769056)




![png](output_10_1.png)



```python
df[["price", "peak-rpm"]].corr()
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
      <th>price</th>
      <th>peak-rpm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>price</th>
      <td>1.000000</td>
      <td>-0.101616</td>
    </tr>
    <tr>
      <th>peak-rpm</th>
      <td>-0.101616</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.regplot(x=df["stroke"], y=df["price"], data=df)
plt.ylim(0,)
```




    (0, 47436.15466888818)




![png](output_12_1.png)



```python
df[["stroke", "price"]].corr()
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
      <th>stroke</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>stroke</th>
      <td>1.00000</td>
      <td>0.08231</td>
    </tr>
    <tr>
      <th>price</th>
      <td>0.08231</td>
      <td>1.00000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.boxplot(x=df["body-style"], y=df["price"], data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f2bced66780>




![png](output_14_1.png)



```python
sns.boxplot(x=df["engine-location"], y=df["price"], data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f2ba649ada0>




![png](output_15_1.png)



```python
sns.boxplot(x=df["drive-wheels"], y=df["price"], data=df)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f2ba6409e48>




![png](output_16_1.png)



```python
df['drive-wheels'].value_counts().to_frame()
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
      <th>drive-wheels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>fwd</th>
      <td>118</td>
    </tr>
    <tr>
      <th>rwd</th>
      <td>75</td>
    </tr>
    <tr>
      <th>4wd</th>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
drive_wheels_counts  = df["drive-wheels"].value_counts().to_frame()
drive_wheels_counts.rename(columns={'drive-wheels' : 'value-counts'}, inplace=True)
drive_wheels_counts
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
      <th>value-counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>fwd</th>
      <td>118</td>
    </tr>
    <tr>
      <th>rwd</th>
      <td>75</td>
    </tr>
    <tr>
      <th>4wd</th>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
drive_wheels_counts.index.name='drive-wheels'
drive_wheels_counts
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
      <th>value-counts</th>
    </tr>
    <tr>
      <th>drive-wheels</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>fwd</th>
      <td>118</td>
    </tr>
    <tr>
      <th>rwd</th>
      <td>75</td>
    </tr>
    <tr>
      <th>4wd</th>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
engine_loc_counts = df["engine-location"].value_counts().to_frame()
engine_loc_counts.rename(columns={'engine-location' : 'value_counts'}, inplace=True)
engine_loc_counts
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
      <th>value_counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>front</th>
      <td>198</td>
    </tr>
    <tr>
      <th>rear</th>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
engine_loc_counts.index.name='engine-location'
engine_loc_counts
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
      <th>value_counts</th>
    </tr>
    <tr>
      <th>engine-location</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>front</th>
      <td>198</td>
    </tr>
    <tr>
      <th>rear</th>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["drive-wheels"].unique()
```




    array(['rwd', 'fwd', '4wd'], dtype=object)




```python
df_gptest = df[['drive-wheels','body-style','price']]
grouped_test1 = df_gptest.groupby(['drive-wheels','body-style'],as_index=False).mean()
grouped_test1 = grouped_test1.pivot(index='drive-wheels', columns='body-style')
grouped_test1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="5" halign="left">price</th>
    </tr>
    <tr>
      <th>body-style</th>
      <th>convertible</th>
      <th>hardtop</th>
      <th>hatchback</th>
      <th>sedan</th>
      <th>wagon</th>
    </tr>
    <tr>
      <th>drive-wheels</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4wd</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>7603.000000</td>
      <td>12647.333333</td>
      <td>9095.750000</td>
    </tr>
    <tr>
      <th>fwd</th>
      <td>11595.0</td>
      <td>8249.000000</td>
      <td>8396.387755</td>
      <td>9811.800000</td>
      <td>9997.333333</td>
    </tr>
    <tr>
      <th>rwd</th>
      <td>23949.6</td>
      <td>24202.714286</td>
      <td>14337.777778</td>
      <td>21711.833333</td>
      <td>16994.222222</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_test1=grouped_test1.fillna(0)
grouped_test1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="5" halign="left">price</th>
    </tr>
    <tr>
      <th>body-style</th>
      <th>convertible</th>
      <th>hardtop</th>
      <th>hatchback</th>
      <th>sedan</th>
      <th>wagon</th>
    </tr>
    <tr>
      <th>drive-wheels</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4wd</th>
      <td>0.0</td>
      <td>0.000000</td>
      <td>7603.000000</td>
      <td>12647.333333</td>
      <td>9095.750000</td>
    </tr>
    <tr>
      <th>fwd</th>
      <td>11595.0</td>
      <td>8249.000000</td>
      <td>8396.387755</td>
      <td>9811.800000</td>
      <td>9997.333333</td>
    </tr>
    <tr>
      <th>rwd</th>
      <td>23949.6</td>
      <td>24202.714286</td>
      <td>14337.777778</td>
      <td>21711.833333</td>
      <td>16994.222222</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_test2=df_gptest.groupby(['body-style'], as_index=False).mean()
grouped_test2
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
      <th>body-style</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>convertible</td>
      <td>21890.500000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>hardtop</td>
      <td>22208.500000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>hatchback</td>
      <td>9957.441176</td>
    </tr>
    <tr>
      <th>3</th>
      <td>sedan</td>
      <td>14459.755319</td>
    </tr>
    <tr>
      <th>4</th>
      <td>wagon</td>
      <td>12371.960000</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_pivot = grouped_test1
plt.pcolor(grouped_pivot, cmap='RdBu')
plt.colorbar()
plt.show
```




    <function matplotlib.pyplot.show(*args, **kw)>




![png](output_26_1.png)



```python
fig, ax = plt.subplots()
im = ax.pcolor(grouped_pivot, cmap='RdBu')
row_labels = grouped_pivot.columns.levels[1]
col_labels = grouped_pivot.index
#move ticks and labels to the center
ax.set_xticks(np.arange(grouped_pivot.shape[1]) + 0.5, minor=False)
ax.set_yticks(np.arange(grouped_pivot.shape[0]) + 0.5, minor=False)

#insert labels
ax.set_xticklabels(row_labels, minor=False)
ax.set_yticklabels(col_labels, minor=False)

#rotate label if too long
plt.xticks(rotation=90)

fig.colorbar(im)
plt.show()
```


![png](output_27_0.png)



```python
from scipy import stats
```


```python
pearson_coeff, p_value =stats.pearsonr(df["wheel-base"], df["price"]) 
print ("Pearson corr coeff is: ", pearson_coeff, "and p value is: ", p_value)
```

    Pearson corr coeff is:  0.5846418222655081 and p value is:  8.076488270732955e-20



```python
pearson_coeff, p_value = stats.pearsonr(df['horsepower'], df['price'])
print ('pearson corr coeff is:', pearson_coeff, 'and p value is:', p_value)
```

    pearson corr coeff is: 0.8095745670036559 and p value is: 6.36905742825998e-48



```python
grouped_test2=df_gptest[['drive-wheels', 'price']].groupby(['drive-wheels'])
grouped_test2.head(5)
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
      <th>drive-wheels</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>rwd</td>
      <td>13495.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>rwd</td>
      <td>16500.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>rwd</td>
      <td>16500.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>fwd</td>
      <td>13950.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4wd</td>
      <td>17450.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>fwd</td>
      <td>15250.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>fwd</td>
      <td>17710.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>fwd</td>
      <td>18920.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>fwd</td>
      <td>23875.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>rwd</td>
      <td>16430.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>rwd</td>
      <td>16925.0</td>
    </tr>
    <tr>
      <th>136</th>
      <td>4wd</td>
      <td>7603.0</td>
    </tr>
    <tr>
      <th>140</th>
      <td>4wd</td>
      <td>9233.0</td>
    </tr>
    <tr>
      <th>141</th>
      <td>4wd</td>
      <td>11259.0</td>
    </tr>
    <tr>
      <th>144</th>
      <td>4wd</td>
      <td>8013.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_test2.get_group('4wd')['price']
```




    4      17450.0
    136     7603.0
    140     9233.0
    141    11259.0
    144     8013.0
    145    11694.0
    150     7898.0
    151     8778.0
    Name: price, dtype: float64




```python
f_val, p_val = stats.f_oneway(grouped_test2.get_group('4wd')['price'], grouped_test2.get_group('fwd')['price'], grouped_test2.get_group('rwd')['price'])
print ('f test score is:', f_val, 'and p value is:', p_val)
```

    f test score is: 67.95406500780399 and p value is: 3.3945443577151245e-23



```python

```
