```python
import pandas as pd
import numpy as np
import seaborn as sns
path = 'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/module_5_auto.csv'
df = pd.read_csv(path)
```


```python
df.to_csv('module_5_auto.csv')
```


```python
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
      <th>Unnamed: 0</th>
      <th>Unnamed: 0.1</th>
      <th>symboling</th>
      <th>normalized-losses</th>
      <th>make</th>
      <th>aspiration</th>
      <th>num-of-doors</th>
      <th>body-style</th>
      <th>drive-wheels</th>
      <th>engine-location</th>
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
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>122</td>
      <td>alfa-romero</td>
      <td>std</td>
      <td>two</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
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
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>122</td>
      <td>alfa-romero</td>
      <td>std</td>
      <td>two</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
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
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>122</td>
      <td>alfa-romero</td>
      <td>std</td>
      <td>two</td>
      <td>hatchback</td>
      <td>rwd</td>
      <td>front</td>
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
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>164</td>
      <td>audi</td>
      <td>std</td>
      <td>four</td>
      <td>sedan</td>
      <td>fwd</td>
      <td>front</td>
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
      <td>4</td>
      <td>4</td>
      <td>2</td>
      <td>164</td>
      <td>audi</td>
      <td>std</td>
      <td>four</td>
      <td>sedan</td>
      <td>4wd</td>
      <td>front</td>
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
<p>5 rows × 31 columns</p>
</div>




```python
df=df._get_numeric_data()
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
      <th>Unnamed: 0</th>
      <th>Unnamed: 0.1</th>
      <th>symboling</th>
      <th>normalized-losses</th>
      <th>wheel-base</th>
      <th>length</th>
      <th>width</th>
      <th>height</th>
      <th>curb-weight</th>
      <th>engine-size</th>
      <th>...</th>
      <th>stroke</th>
      <th>compression-ratio</th>
      <th>horsepower</th>
      <th>peak-rpm</th>
      <th>city-mpg</th>
      <th>highway-mpg</th>
      <th>price</th>
      <th>city-L/100km</th>
      <th>diesel</th>
      <th>gas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>122</td>
      <td>88.6</td>
      <td>0.811148</td>
      <td>0.890278</td>
      <td>48.8</td>
      <td>2548</td>
      <td>130</td>
      <td>...</td>
      <td>2.68</td>
      <td>9.0</td>
      <td>111.0</td>
      <td>5000.0</td>
      <td>21</td>
      <td>27</td>
      <td>13495.0</td>
      <td>11.190476</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>122</td>
      <td>88.6</td>
      <td>0.811148</td>
      <td>0.890278</td>
      <td>48.8</td>
      <td>2548</td>
      <td>130</td>
      <td>...</td>
      <td>2.68</td>
      <td>9.0</td>
      <td>111.0</td>
      <td>5000.0</td>
      <td>21</td>
      <td>27</td>
      <td>16500.0</td>
      <td>11.190476</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>122</td>
      <td>94.5</td>
      <td>0.822681</td>
      <td>0.909722</td>
      <td>52.4</td>
      <td>2823</td>
      <td>152</td>
      <td>...</td>
      <td>3.47</td>
      <td>9.0</td>
      <td>154.0</td>
      <td>5000.0</td>
      <td>19</td>
      <td>26</td>
      <td>16500.0</td>
      <td>12.368421</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>164</td>
      <td>99.8</td>
      <td>0.848630</td>
      <td>0.919444</td>
      <td>54.3</td>
      <td>2337</td>
      <td>109</td>
      <td>...</td>
      <td>3.40</td>
      <td>10.0</td>
      <td>102.0</td>
      <td>5500.0</td>
      <td>24</td>
      <td>30</td>
      <td>13950.0</td>
      <td>9.791667</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>4</td>
      <td>2</td>
      <td>164</td>
      <td>99.4</td>
      <td>0.848630</td>
      <td>0.922222</td>
      <td>54.3</td>
      <td>2824</td>
      <td>136</td>
      <td>...</td>
      <td>3.40</td>
      <td>8.0</td>
      <td>115.0</td>
      <td>5500.0</td>
      <td>18</td>
      <td>22</td>
      <td>17450.0</td>
      <td>13.055556</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
%%capture
! pip install ipywidgets
```


```python
from IPython.display import display
from IPython.html import widgets
from ipywidgets import interact, interactive, fixed, interact_manual
```


```python
def DistributionPlot (RedFunction, BlueFunction, RedName, BlueName, Title):
    width=12
    height=10
    plt.figure(figsize=(width, height))
    
    ax1=sns.distplot(RedFunction, hist=False, color="r", label=RedName)
    ax2=sns.distplot(BlueFunction, hist=False, color="b", label=BlueName, ax=ax1)
    
    plt.title(Title)
    plt.xlabel('Price in dollars')
    plt.ylabel('Proportion of cars')
    
    plt.show()
    plt.close()
```


```python
def PollyPlot (x_train, x_test, y_train, y_test, lr, poly_transform):
    width=12
    height=10
    plt.figure(figsize=(width, height))
    
    #training data 
    #testing data 
    # lr:  linear regression object 
    #poly_transform:  polynomial transformation object 
    
    xmax=max([x_train.values.max(), x_test.values.max()])

    xmin=min([x_train.values.min(), x_test.values.min()])

    x=np.arange(xmin, xmax, 0.1)


    plt.plot(x_train, y_train, 'ro', label='Training Data')
    plt.plot(x_test, y_test, 'go', label='Test Data')
    plt.plot(x, lr.predict(poly_transform.fit_transform(x.reshape(-1, 1))), label='Predicted Function')
    plt.ylim([-10000, 60000])
    plt.ylabel('Price')
    plt.legend()
```


```python
y_data=df["price"]
y_data.head()
y_data.shape
```




    (201,)




```python
x_data=df.drop('price', axis=1)
x_data.shape
```




    (201, 20)




```python
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=0.15, random_state=1)
print ('number of training samples:', x_train.shape[0])
print ('number of testing samples:', x_test.shape[0])
```

    number of training samples: 170
    number of testing samples: 31



```python
# Write your code below and press Shift+Enter to execute 
x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=0.4, random_state=0)
print ("number of testing samples:", x_test.shape[0])
print ("number of training samples:", x_train.shape[0])
```

    number of testing samples: 81
    number of training samples: 120



```python
from sklearn.linear_model import LinearRegression
lre=LinearRegression()
lre.fit(x_train[["horsepower"]], y_train)
lre.score(x_test[["horsepower"]], y_test)
lre.score(x_train[["horsepower"]], y_train)
```




    0.5754067463583004




```python
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=0.1, random_state=0)
from sklearn.linear_model import LinearRegression
lre.fit(x_train[["horsepower"]], y_train)
lre.score(x_test[["horsepower"]], y_test)
```




    0.7340722810055448




```python
from sklearn.model_selection import cross_val_score
Rcross = cross_val_score(lre, x_data[["horsepower"]], y_data,cv=4 )
Rcross
print ("The mean of folds:", Rcross.mean(), "The std is:", Rcross.std())
```

    The mean of folds: 0.522009915042119 The std is: 0.291183944475603



```python
from sklearn.model_selection import cross_val_score
Rcross = cross_val_score(lre, x_data[["horsepower"]], y_data, cv = 2)
print ("the mean is ", Rcross.mean(), "while the std is ", Rcross.std())
```

    the mean is  0.5166761697127429 while the std is  0.07348004195771388



```python

```


```python
from sklearn.model_selection import cross_val_predict
yhat = cross_val_predict(lre, x_data[["horsepower"]], y_data, cv=4)
yhat[0:5]
```




    array([14141.63807508, 14141.63807508, 20814.29423473, 12745.03562306,
           14762.35027598])




```python
lr = LinearRegression()
lr.fit(x_train[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']], y_train)
```




    LinearRegression(copy_X=True, fit_intercept=True, n_jobs=None,
             normalize=False)




```python
yhat_train = lr.predict(x_train[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']])
yhat_train[0:5]
yhat_test=lr.predict(x_test[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']])
yhat_test[0:5]
```




    array([ 5303.07151822, 10171.81756487, 19443.60652378, 22426.68778351,
           21294.42778767])




```python
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
```


```python
Title = "Distribution  Plot of  Predicted Value Using Training Data vs Training Data Distribution"
DistributionPlot(y_train, yhat_train, "Actual Values (Train)", "Predicted Values (Train)", Title)
```


![png](output_21_0.png)



```python
Title='Distribution  Plot of  Predicted Value Using Test Data vs Data Distribution of Test Data'
DistributionPlot(y_test, yhat_test, "Actual Values (Test)","Predicted Values (Test)",Title)
```


![png](output_22_0.png)



```python
from sklearn.preprocessing import PolynomialFeatures
```


```python
x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=0.45, random_state=0)
```


```python
pr = PolynomialFeatures(degree=5)
x_train_pr=pr.fit_transform(x_train[["horsepower"]])
x_test_pr=pr.fit_transform(x_test[["horsepower"]])
pr
```




    PolynomialFeatures(degree=5, include_bias=True, interaction_only=False)




```python
poly=LinearRegression()
poly.fit(x_train_pr, y_train)
```




    LinearRegression(copy_X=True, fit_intercept=True, n_jobs=None,
             normalize=False)




```python
yhat = poly.predict(x_test_pr)
yhat[0:5]
```




    array([ 6728.65584216,  7307.98804276, 12213.78788015, 18893.2476361 ,
           19995.95145897])




```python
print("Predicted values:", yhat[0:4])
print("True values:", y_test[0:4].values)
```

    Predicted values: [ 6728.65584216  7307.98804276 12213.78788015 18893.2476361 ]
    True values: [ 6295. 10698. 13860. 13499.]



```python
PollyPlot(x_train[['horsepower']], x_test[['horsepower']], y_train, y_test, poly,pr)
```


![png](output_29_0.png)



```python
poly.score(x_train_pr, y_train)
```




    0.5567716902126982




```python
poly.score(x_test_pr, y_test)
```




    -29.871341600352796




```python
Rsqu_test = []
order = [1,2,3,4]
for n in order:
    pr = PolynomialFeatures(degree=n)
    x_train_pr = pr.fit_transform(x_train[["horsepower"]])
    x_test_pr = pr.fit_transform(x_test[["horsepower"]])
    lr.fit(x_train_pr, y_train)
    
    Rsqu_test.append(lr.score(x_test_pr, y_test))

plt.plot(order, Rsqu_test)
plt.xlabel("order")
plt.ylabel("R^2")
plt.title("R^2 using test data")
plt.text(3, 0.75, "maximum R^2")
```




    Text(3, 0.75, 'maximum R^2')




![png](output_32_1.png)



```python
def f(order, test_data):
    x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=test_data, random_state=0)
    pr = PolynomialFeatures(degree=order)
    x_train_pr = pr.fit_transform(x_train[["horsepower"]])
    x_test_pr = pr.fit_transform(x_test[["horsepower"]])
    
    poly = LinearRegression()
    poly.fit(x_train_pr, y_train)
    PollyPlot(x_train[["horsepower"]], x_test[["horsepower"]],y_train, y_test, poly, pr )
    
```


```python
interact(f, order = (0,6,1), test_data = (0.05, 0.95, 0.5))
```


    interactive(children=(IntSlider(value=3, description='order', max=6), FloatSlider(value=0.05, description='tes…





    <function __main__.f(order, test_data)>




```python
pr1 = PolynomialFeatures(degree=2)
x_train_pr1 = pr.fit_transform (x_train[["horsepower", "curb-weight", "engine-size", "highway-mpg"]])
x_test_pr1 = pr.fit_transform (x_test[["horsepower", "curb-weight", "engine-size", "highway-mpg"]])
```


```python
x_train_pr1.shape
```




    (110, 70)




```python
poly1=LinearRegression().fit(x_train_pr1, y_train)
```


```python
yhat_test1 = poly1.predict(x_test_pr1)
Title='Distribution  Plot of  Predicted Value Using Test Data vs Data Distribution of Test Data'
DistributionPlot(y_test, yhat_test1,"Actual Values (Test)", "Predicted Values (Test)", Title )
```


![png](output_38_0.png)



```python
from sklearn.linear_model import Ridge
Ridgemodel=Ridge(alpha=10)
Ridgemodel.fit(x_train_pr, y_train)
Ridgemodel.score(x_test_pr, y_test)
```

    /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages/sklearn/linear_model/ridge.py:125: LinAlgWarning: Ill-conditioned matrix (rcond=1.17189e-18): result may not be accurate.
      overwrite_a=True).T





    0.580263384325818




```python
from sklearn.model_selection import GridSearchCV
parameters1 = [{'alpha': [0.001,0.1,1, 10, 100, 1000, 10000, 100000, 100000]}]
parameters1
```




    [{'alpha': [0.001, 0.1, 1, 10, 100, 1000, 10000, 100000, 100000]}]




```python
RR=Ridge()
RR
```




    Ridge(alpha=1.0, copy_X=True, fit_intercept=True, max_iter=None,
       normalize=False, random_state=None, solver='auto', tol=0.001)




```python
Grid1=GridSearchCV(RR, parameters1, cv=4)
Grid1
```




    GridSearchCV(cv=4, error_score='raise-deprecating',
           estimator=Ridge(alpha=1.0, copy_X=True, fit_intercept=True, max_iter=None,
       normalize=False, random_state=None, solver='auto', tol=0.001),
           fit_params=None, iid='warn', n_jobs=None,
           param_grid=[{'alpha': [0.001, 0.1, 1, 10, 100, 1000, 10000, 100000, 100000]}],
           pre_dispatch='2*n_jobs', refit=True, return_train_score='warn',
           scoring=None, verbose=0)




```python
Grid1.fit(x_train[["horsepower", "curb-weight", "engine-size", "highway-mpg"]], y_train)
BestRR=Grid1.best_estimator_
BestRR
```

    /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages/sklearn/model_selection/_search.py:841: DeprecationWarning: The default of the `iid` parameter will change from True to False in version 0.22 and will be removed in 0.24. This will change numeric results when test-set sizes are unequal.
      DeprecationWarning)





    Ridge(alpha=10000, copy_X=True, fit_intercept=True, max_iter=None,
       normalize=False, random_state=None, solver='auto', tol=0.001)




```python
BestRR.score(x_test[["horsepower", "curb-weight", "engine-size", "highway-mpg"]], y_test)
```




    0.7722630851874491


