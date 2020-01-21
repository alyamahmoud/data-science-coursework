```python
%load_ext sql
%sql ibm_db_sa://smg47194:v0b8j%5Eq48gk021x5@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
```




    'Connected: smg47194@BLUDB'




```python
import pandas
chicago_socioeconomic_dat = pandas.read_csv ('https://data.cityofchicago.org/resource/jcxq-k9xf.csv')
%sql PERSIST chicago_socioeconomic_dat
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB





    'Persisted chicago_socioeconomic_dat'




```python
%sql SELECT * from chicago_socioeconomic_dat limit 5; 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>index</th>
        <th>ca</th>
        <th>community_area_name</th>
        <th>percent_of_housing_crowded</th>
        <th>percent_households_below_poverty</th>
        <th>percent_aged_16_unemployed</th>
        <th>percent_aged_25_without_high_school_diploma</th>
        <th>percent_aged_under_18_or_over_64</th>
        <th>per_capita_income_</th>
        <th>hardship_index</th>
    </tr>
    <tr>
        <td>0</td>
        <td>1.0</td>
        <td>Rogers Park</td>
        <td>7.7</td>
        <td>23.6</td>
        <td>8.7</td>
        <td>18.2</td>
        <td>27.5</td>
        <td>23939</td>
        <td>39.0</td>
    </tr>
    <tr>
        <td>1</td>
        <td>2.0</td>
        <td>West Ridge</td>
        <td>7.8</td>
        <td>17.2</td>
        <td>8.8</td>
        <td>20.8</td>
        <td>38.5</td>
        <td>23040</td>
        <td>46.0</td>
    </tr>
    <tr>
        <td>2</td>
        <td>3.0</td>
        <td>Uptown</td>
        <td>3.8</td>
        <td>24.0</td>
        <td>8.9</td>
        <td>11.8</td>
        <td>22.2</td>
        <td>35787</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>3</td>
        <td>4.0</td>
        <td>Lincoln Square</td>
        <td>3.4</td>
        <td>10.9</td>
        <td>8.2</td>
        <td>13.4</td>
        <td>25.5</td>
        <td>37524</td>
        <td>17.0</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5.0</td>
        <td>North Center</td>
        <td>0.3</td>
        <td>7.5</td>
        <td>5.2</td>
        <td>4.5</td>
        <td>26.2</td>
        <td>57123</td>
        <td>6.0</td>
    </tr>
</table>




```python
%sql SELECT count(*) from chicago_socioeconomic_dat; 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>78</td>
    </tr>
</table>




```python
%sql SELECT count (*) community_area_name from chicago_socioeconomic_dat where hardship_index > 50; 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    (ibm_db_dbi.ProgrammingError) ibm_db_dbi::ProgrammingError: SQLNumResultCols failed: [IBM][CLI Driver][DB2/LINUXX8664] SQL0104N  An unexpected token "(" was found following "T count (*) distinct".  Expected tokens may include:  ",".  SQLSTATE=42601 SQLCODE=-104
    [SQL: SELECT count (*) distinct (community_area_name) from chicago_socioeconomic_dat where hardship_index > 50;]
    (Background on this error at: http://sqlalche.me/e/f405)



```python
%sql SELECT MAX(hardship_index) from chicago_socioeconomic_dat; 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>98.0</td>
    </tr>
</table>




```python
%sql SELECT community_area_name from chicago_socioeconomic_dat where hardship_index = 98; 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>community_area_name</th>
    </tr>
    <tr>
        <td>Riverdale</td>
    </tr>
</table>




```python
%sql SELECT community_area_name from chicago_socioeconomic_dat where per_capita_income_ > 60000; 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>community_area_name</th>
    </tr>
    <tr>
        <td>Lake View</td>
    </tr>
    <tr>
        <td>Lincoln Park</td>
    </tr>
    <tr>
        <td>Near North Side</td>
    </tr>
    <tr>
        <td>Loop</td>
    </tr>
</table>




```python
import matplotlib.pyplot as plt
import seaborn as sns
income_vs_hardship = %sql SELECT per_capita_income_, hardship_index from chicago_socioeconomic_dat; 
plot = sns.jointplot (x='per_capita_income_', y='hardship_index', data=income_vs_hardship.DataFrame())
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.



![png](output_8_1.png)



```python
import matplotlib.pyplot as plt
import seaborn as sns
income_vs_poverty = %sql SELECT percent_households_below_poverty, per_capita_income_ from chicago_socioeconomic_dat; 
plot = sns.jointplot(x='per_capita_income_', y='percent_households_below_poverty', data=income_vs_poverty.DataFrame())
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.



![png](output_9_1.png)



```python
income_vs_unemployment = %sql SELECT per_capita_income_, percent_aged_16_unemployed from chicago_socioeconomic_dat; 
plot = sns.jointplot(x='per_capita_income_', y='percent_aged_16_unemployed', data=income_vs_unemployment.DataFrame())
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.



![png](output_10_1.png)



```python

```


```python

```
