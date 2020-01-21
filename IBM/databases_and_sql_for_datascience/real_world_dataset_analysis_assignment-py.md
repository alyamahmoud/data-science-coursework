<a href="https://cognitiveclass.ai"><img src = "https://ibm.box.com/shared/static/ugcqz6ohbvff804xp84y4kqnvvk3bq1g.png" width = 300, align = "center"></a>

<h1 align=center><font size = 5>Assignment: Notebook for Peer Assignment</font></h1>

# Introduction

Using this Python notebook you will:
1. Understand 3 Chicago datasets  
1. Load the 3 datasets into 3 tables in a Db2 database
1. Execute SQL queries to answer assignment questions 

## Understand the datasets 
To complete the assignment problems in this notebook you will be using three datasets that are available on the city of Chicago's Data Portal:
1. <a href="https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2">Socioeconomic Indicators in Chicago</a>
1. <a href="https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t">Chicago Public Schools</a>
1. <a href="https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2">Chicago Crime Data</a>

### 1. Socioeconomic Indicators in Chicago
This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” for each Chicago community area, for the years 2008 – 2012.

For this assignment you will use a snapshot of this dataset which can be downloaded from:
https://ibm.box.com/shared/static/05c3415cbfbtfnr2fx4atenb2sd361ze.csv

A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:
https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2



### 2. Chicago Public Schools

This dataset shows all school level performance data used to create CPS School Report Cards for the 2011-2012 school year. This dataset is provided by the city of Chicago's Data Portal.

For this assignment you will use a snapshot of this dataset which can be downloaded from:
https://ibm.box.com/shared/static/f9gjvj1gjmxxzycdhplzt01qtz0s7ew7.csv

A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:
https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t




### 3. Chicago Crime Data 

This dataset reflects reported incidents of crime (with the exception of murders where data exists for each victim) that occurred in the City of Chicago from 2001 to present, minus the most recent seven days. 

This dataset is quite large - over 1.5GB in size with over 6.5 million rows. For the purposes of this assignment we will use a much smaller sample of this dataset which can be downloaded from:
https://ibm.box.com/shared/static/svflyugsr9zbqy5bmowgswqemfpm1x7f.csv

A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:
https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2


### Download the datasets
In many cases the dataset to be analyzed is available as a .CSV (comma separated values) file, perhaps on the internet. Click on the links below to download and save the datasets (.CSV files):
1. __CENSUS_DATA:__ https://ibm.box.com/shared/static/05c3415cbfbtfnr2fx4atenb2sd361ze.csv
1. __CHICAGO_PUBLIC_SCHOOLS__  https://ibm.box.com/shared/static/f9gjvj1gjmxxzycdhplzt01qtz0s7ew7.csv
1. __CHICAGO_CRIME_DATA:__ https://ibm.box.com/shared/static/svflyugsr9zbqy5bmowgswqemfpm1x7f.csv

__NOTE:__ Ensure you have downloaded the datasets using the links above instead of directly from the Chicago Data Portal. The versions linked here are subsets of the original datasets and have some of the column names modified to be more database friendly which will make it easier to complete this assignment.

### Store the datasets in database tables
To analyze the data using SQL, it first needs to be stored in the database.

While it is easier to read the dataset into a Pandas dataframe and then PERSIST it into the database as we saw in Week 3 Lab 3, it results in mapping to default datatypes which may not be optimal for SQL querying. For example a long textual field may map to a CLOB instead of a VARCHAR. 

Therefore, __it is highly recommended to manually load the table using the database console LOAD tool, as indicated in Week 2 Lab 1 Part II__. The only difference with that lab is that in Step 5 of the instructions you will need to click on create "(+) New Table" and specify the name of the table you want to create and then click "Next". 

<img src = "https://ibm.box.com/shared/static/uc4xjh1uxcc78ks1i18v668simioz4es.jpg">

##### Now open the Db2 console, open the LOAD tool, Select / Drag the .CSV file for the first dataset, Next create a New Table, and then follow the steps on-screen instructions to load the data. Name the new tables as folows:
1. __CENSUS_DATA__
1. __CHICAGO_PUBLIC_SCHOOLS__
1. __CHICAGO_CRIME_DATA__

### Connect to the database 
Let us first load the SQL extension and establish a connection with the database


```python
%load_ext sql
```

In the next cell enter your db2 connection string. Recall you created Service Credentials for your Db2 instance in first lab in Week 3. From the __uri__ field of your Db2 service credentials copy everything after db2:// (except the double quote at the end) and paste it in the cell below after ibm_db_sa://

<img src ="https://ibm.box.com/shared/static/hzhkvdyinpupm2wfx49lkr71q9swbpec.jpg">


```python
# Remember the connection string is of the format:
# %sql ibm_db_sa://my-username:my-password@my-hostname:my-port/my-db-name
# Enter the connection string for your Db2 on Cloud database instance below
%sql ibm_db_sa://smg47194:v0b8j%5Eq48gk021x5@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
```




    'Connected: smg47194@BLUDB'



## Problems
Now write and execute SQL queries to solve assignment problems

### Problem 1

##### Find the total number of crimes recorded in the CRIME table


```python
# Rows in Crime table
import pandas
CHICAGO_CRIME_DATA = pandas.read_csv ('https://ibm.box.com/shared/static/svflyugsr9zbqy5bmowgswqemfpm1x7f.csv')
%sql drop table CHICAGO_CRIME_DATA
%sql PERSIST CHICAGO_CRIME_DATA
%sql SELECT * FROM SYSCAT.TABLES where TABNAME='CHICAGO_CRIME_DATA'
%sql SELECT COUNT(*) FROM CHICAGO_CRIME_DATA
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.
     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.
     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>533</td>
    </tr>
</table>



### Problem 2

##### Retrieve first 10 rows from the CRIME table



```python
%sql SELECT * FROM CHICAGO_CRIME_DATA LIMIT 10;
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>index</th>
        <th>id</th>
        <th>case_number</th>
        <th>DATE</th>
        <th>block</th>
        <th>iucr</th>
        <th>primary_type</th>
        <th>description</th>
        <th>location_description</th>
        <th>arrest</th>
        <th>domestic</th>
        <th>beat</th>
        <th>district</th>
        <th>ward</th>
        <th>community_area_number</th>
        <th>fbicode</th>
        <th>x_coordinate</th>
        <th>y_coordinate</th>
        <th>YEAR</th>
        <th>updatedon</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>location</th>
    </tr>
    <tr>
        <td>0</td>
        <td>3512276</td>
        <td>HK587712</td>
        <td>08/28/2004 05:50:56 PM</td>
        <td>047XX S KEDZIE AVE</td>
        <td>890</td>
        <td>THEFT</td>
        <td>FROM BUILDING</td>
        <td>SMALL RETAIL STORE</td>
        <td>0</td>
        <td>0</td>
        <td>911</td>
        <td>9</td>
        <td>14.0</td>
        <td>58.0</td>
        <td>6</td>
        <td>1155838.0</td>
        <td>1873050.0</td>
        <td>2004</td>
        <td>02/10/2018 03:50:01 PM</td>
        <td>41.807440500000006</td>
        <td>-87.70395585</td>
        <td>(41.8074405, -87.703955849)</td>
    </tr>
    <tr>
        <td>1</td>
        <td>3406613</td>
        <td>HK456306</td>
        <td>06/26/2004 12:40:00 PM</td>
        <td>009XX N CENTRAL PARK AVE</td>
        <td>820</td>
        <td>THEFT</td>
        <td>$500 AND UNDER</td>
        <td>OTHER</td>
        <td>0</td>
        <td>0</td>
        <td>1112</td>
        <td>11</td>
        <td>27.0</td>
        <td>23.0</td>
        <td>6</td>
        <td>1152206.0</td>
        <td>1906127.0</td>
        <td>2004</td>
        <td>02/28/2018 03:56:25 PM</td>
        <td>41.89827996</td>
        <td>-87.71640551</td>
        <td>(41.898279962, -87.716405505)</td>
    </tr>
    <tr>
        <td>2</td>
        <td>8002131</td>
        <td>HT233595</td>
        <td>04/04/2011 05:45:00 AM</td>
        <td>043XX S WABASH AVE</td>
        <td>820</td>
        <td>THEFT</td>
        <td>$500 AND UNDER</td>
        <td>NURSING HOME/RETIREMENT HOME</td>
        <td>0</td>
        <td>0</td>
        <td>221</td>
        <td>2</td>
        <td>3.0</td>
        <td>38.0</td>
        <td>6</td>
        <td>1177436.0</td>
        <td>1876313.0</td>
        <td>2011</td>
        <td>02/10/2018 03:50:01 PM</td>
        <td>41.81593313</td>
        <td>-87.62464213</td>
        <td>(41.815933131, -87.624642127)</td>
    </tr>
    <tr>
        <td>3</td>
        <td>7903289</td>
        <td>HT133522</td>
        <td>12/30/2010 04:30:00 PM</td>
        <td>083XX S KINGSTON AVE</td>
        <td>840</td>
        <td>THEFT</td>
        <td>FINANCIAL ID THEFT: OVER $300</td>
        <td>RESIDENCE</td>
        <td>0</td>
        <td>0</td>
        <td>423</td>
        <td>4</td>
        <td>7.0</td>
        <td>46.0</td>
        <td>6</td>
        <td>1194622.0</td>
        <td>1850125.0</td>
        <td>2010</td>
        <td>02/10/2018 03:50:01 PM</td>
        <td>41.74366532</td>
        <td>-87.56246276</td>
        <td>(41.743665322, -87.562462756)</td>
    </tr>
    <tr>
        <td>4</td>
        <td>10402076</td>
        <td>HZ138551</td>
        <td>02/02/2016 07:30:00 PM</td>
        <td>033XX W 66TH ST</td>
        <td>820</td>
        <td>THEFT</td>
        <td>$500 AND UNDER</td>
        <td>ALLEY</td>
        <td>0</td>
        <td>0</td>
        <td>831</td>
        <td>8</td>
        <td>15.0</td>
        <td>66.0</td>
        <td>6</td>
        <td>1155240.0</td>
        <td>1860661.0</td>
        <td>2016</td>
        <td>02/10/2018 03:50:01 PM</td>
        <td>41.773455299999995</td>
        <td>-87.70648047</td>
        <td>(41.773455295, -87.706480471)</td>
    </tr>
    <tr>
        <td>5</td>
        <td>7732712</td>
        <td>HS540106</td>
        <td>09/29/2010 07:59:00 AM</td>
        <td>006XX W CHICAGO AVE</td>
        <td>810</td>
        <td>THEFT</td>
        <td>OVER $500</td>
        <td>PARKING LOT/GARAGE(NON.RESID.)</td>
        <td>0</td>
        <td>0</td>
        <td>1323</td>
        <td>12</td>
        <td>27.0</td>
        <td>24.0</td>
        <td>6</td>
        <td>1171668.0</td>
        <td>1905607.0</td>
        <td>2010</td>
        <td>02/10/2018 03:50:01 PM</td>
        <td>41.89644677</td>
        <td>-87.64493868</td>
        <td>(41.896446772, -87.644938678)</td>
    </tr>
    <tr>
        <td>6</td>
        <td>10769475</td>
        <td>HZ534771</td>
        <td>11/30/2016 01:15:00 AM</td>
        <td>050XX N KEDZIE AVE</td>
        <td>810</td>
        <td>THEFT</td>
        <td>OVER $500</td>
        <td>STREET</td>
        <td>0</td>
        <td>0</td>
        <td>1713</td>
        <td>17</td>
        <td>33.0</td>
        <td>14.0</td>
        <td>6</td>
        <td>1154133.0</td>
        <td>1933314.0</td>
        <td>2016</td>
        <td>02/10/2018 03:50:01 PM</td>
        <td>41.97284491</td>
        <td>-87.70860008</td>
        <td>(41.972844913, -87.708600079)</td>
    </tr>
    <tr>
        <td>7</td>
        <td>4494340</td>
        <td>HL793243</td>
        <td>12/16/2005 04:45:00 PM</td>
        <td>005XX E PERSHING RD</td>
        <td>860</td>
        <td>THEFT</td>
        <td>RETAIL THEFT</td>
        <td>GROCERY FOOD STORE</td>
        <td>1</td>
        <td>0</td>
        <td>213</td>
        <td>2</td>
        <td>3.0</td>
        <td>38.0</td>
        <td>6</td>
        <td>1180448.0</td>
        <td>1879234.0</td>
        <td>2005</td>
        <td>02/28/2018 03:56:25 PM</td>
        <td>41.82387989</td>
        <td>-87.61350386</td>
        <td>(41.823879885, -87.613503857)</td>
    </tr>
    <tr>
        <td>8</td>
        <td>3778925</td>
        <td>HL149610</td>
        <td>01/28/2005 05:00:00 PM</td>
        <td>100XX S WASHTENAW AVE</td>
        <td>810</td>
        <td>THEFT</td>
        <td>OVER $500</td>
        <td>STREET</td>
        <td>0</td>
        <td>0</td>
        <td>2211</td>
        <td>22</td>
        <td>19.0</td>
        <td>72.0</td>
        <td>6</td>
        <td>1160129.0</td>
        <td>1838040.0</td>
        <td>2005</td>
        <td>02/28/2018 03:56:25 PM</td>
        <td>41.71128051</td>
        <td>-87.68917909999999</td>
        <td>(41.711280513, -87.689179097)</td>
    </tr>
    <tr>
        <td>9</td>
        <td>3324217</td>
        <td>HK361551</td>
        <td>05/13/2004 02:15:00 PM</td>
        <td>033XX W BELMONT AVE</td>
        <td>820</td>
        <td>THEFT</td>
        <td>$500 AND UNDER</td>
        <td>SMALL RETAIL STORE</td>
        <td>0</td>
        <td>0</td>
        <td>1733</td>
        <td>17</td>
        <td>35.0</td>
        <td>21.0</td>
        <td>6</td>
        <td>1153590.0</td>
        <td>1921084.0</td>
        <td>2004</td>
        <td>02/28/2018 03:56:25 PM</td>
        <td>41.93929582</td>
        <td>-87.71092344</td>
        <td>(41.939295821, -87.710923442)</td>
    </tr>
</table>



### Problem 3

##### How many crimes involve an arrest?


```python
%sql SELECT COUNT(*) FROM CHICAGO_CRIME_DATA WHERE arrest=1;
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>163</td>
    </tr>
</table>



### Problem 4

##### Which unique types of crimes have been recorded at GAS STATION locations?



```python
%sql SELECT primary_type FROM CHICAGO_CRIME_DATA WHERE location_description = 'GAS STATION' 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>primary_type</th>
    </tr>
    <tr>
        <td>THEFT</td>
    </tr>
    <tr>
        <td>THEFT</td>
    </tr>
    <tr>
        <td>NARCOTICS</td>
    </tr>
    <tr>
        <td>ROBBERY</td>
    </tr>
    <tr>
        <td>ROBBERY</td>
    </tr>
    <tr>
        <td>CRIMINAL TRESPASS</td>
    </tr>
</table>



Hint: Which column lists types of crimes e.g. THEFT?

### Problem 5

##### In the CENUS_DATA table list all Community Areas whose names start with the letter ‘B’.


```python
%sql SELECT * FROM CENSUS_DATA limit 10; 
#%sql SELECT community_area_name FROM CENSUS_DATA where community_area_name LIKE 'B%'
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>community_area_number</th>
        <th>community_area_name</th>
        <th>percent_of_housing_crowded</th>
        <th>percent_households_below_poverty</th>
        <th>percent_aged_16__unemployed</th>
        <th>percent_aged_25__without_high_school_diploma</th>
        <th>percent_aged_under_18_or_over_64</th>
        <th>per_capita_income</th>
        <th>hardship_index</th>
    </tr>
    <tr>
        <td>1</td>
        <td>Rogers Park</td>
        <td>7.7</td>
        <td>23.6</td>
        <td>8.7</td>
        <td>18.2</td>
        <td>27.5</td>
        <td>23939</td>
        <td>39</td>
    </tr>
    <tr>
        <td>2</td>
        <td>West Ridge</td>
        <td>7.8</td>
        <td>17.2</td>
        <td>8.8</td>
        <td>20.8</td>
        <td>38.5</td>
        <td>23040</td>
        <td>46</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Uptown</td>
        <td>3.8</td>
        <td>24.0</td>
        <td>8.9</td>
        <td>11.8</td>
        <td>22.2</td>
        <td>35787</td>
        <td>20</td>
    </tr>
    <tr>
        <td>4</td>
        <td>Lincoln Square</td>
        <td>3.4</td>
        <td>10.9</td>
        <td>8.2</td>
        <td>13.4</td>
        <td>25.5</td>
        <td>37524</td>
        <td>17</td>
    </tr>
    <tr>
        <td>5</td>
        <td>North Center</td>
        <td>0.3</td>
        <td>7.5</td>
        <td>5.2</td>
        <td>4.5</td>
        <td>26.2</td>
        <td>57123</td>
        <td>6</td>
    </tr>
    <tr>
        <td>6</td>
        <td>Lake View</td>
        <td>1.1</td>
        <td>11.4</td>
        <td>4.7</td>
        <td>2.6</td>
        <td>17.0</td>
        <td>60058</td>
        <td>5</td>
    </tr>
    <tr>
        <td>7</td>
        <td>Lincoln Park</td>
        <td>0.8</td>
        <td>12.3</td>
        <td>5.1</td>
        <td>3.6</td>
        <td>21.5</td>
        <td>71551</td>
        <td>2</td>
    </tr>
    <tr>
        <td>8</td>
        <td>Near North Side</td>
        <td>1.9</td>
        <td>12.9</td>
        <td>7.0</td>
        <td>2.5</td>
        <td>22.6</td>
        <td>88669</td>
        <td>1</td>
    </tr>
    <tr>
        <td>9</td>
        <td>Edison Park</td>
        <td>1.1</td>
        <td>3.3</td>
        <td>6.5</td>
        <td>7.4</td>
        <td>35.3</td>
        <td>40959</td>
        <td>8</td>
    </tr>
    <tr>
        <td>10</td>
        <td>Norwood Park</td>
        <td>2.0</td>
        <td>5.4</td>
        <td>9.0</td>
        <td>11.5</td>
        <td>39.5</td>
        <td>32875</td>
        <td>21</td>
    </tr>
</table>



### Problem 6

##### Which schools in Community Areas 10 to 15 are healthy school certified?


```python
%sql SELECT * FROM CHICAGO_PUBLIC_SCHOOLS LIMIT 10
#%sql SELECT name_of_school, healthy_school_certified, community_area_name, community_area_number FROM CHICAGO_PUBLIC_SCHOOLS \
#WHERE (community_area_number between 10 AND 15) AND healthy_school_certified='Yes'


```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>School_ID</th>
        <th>name_of_school</th>
        <th>Elementary, Middle, or High School</th>
        <th>Street_Address</th>
        <th>City</th>
        <th>State</th>
        <th>ZIP_Code</th>
        <th>Phone_Number</th>
        <th>Link</th>
        <th>Network_Manager</th>
        <th>Collaborative_Name</th>
        <th>Adequate_Yearly_Progress_Made_</th>
        <th>Track_Schedule</th>
        <th>CPS_Performance_Policy_Status</th>
        <th>CPS_Performance_Policy_Level</th>
        <th>healthy_school_certified</th>
        <th>Safety_Icon</th>
        <th>safety_score</th>
        <th>Family_Involvement_Icon</th>
        <th>Family_Involvement_Score</th>
        <th>Environment_Icon</th>
        <th>Environment_Score</th>
        <th>Instruction_Icon</th>
        <th>Instruction_Score</th>
        <th>Leaders_Icon</th>
        <th>Leaders_Score</th>
        <th>Teachers_Icon</th>
        <th>Teachers_Score</th>
        <th>Parent_Engagement_Icon</th>
        <th>Parent_Engagement_Score</th>
        <th>Parent_Environment_Icon</th>
        <th>Parent_Environment_Score</th>
        <th>average_student_attendance</th>
        <th>Rate_of_Misconducts__per_100_students_</th>
        <th>Average_Teacher_Attendance</th>
        <th>Individualized_Education_Program_Compliance_Rate</th>
        <th>Pk_2_Literacy__</th>
        <th>Pk_2_Math__</th>
        <th>Gr3_5_Grade_Level_Math__</th>
        <th>Gr3_5_Grade_Level_Read__</th>
        <th>Gr3_5_Keep_Pace_Read__</th>
        <th>Gr3_5_Keep_Pace_Math__</th>
        <th>Gr6_8_Grade_Level_Math__</th>
        <th>Gr6_8_Grade_Level_Read__</th>
        <th>Gr6_8_Keep_Pace_Math_</th>
        <th>Gr6_8_Keep_Pace_Read__</th>
        <th>Gr_8_Explore_Math__</th>
        <th>Gr_8_Explore_Read__</th>
        <th>ISAT_Exceeding_Math__</th>
        <th>ISAT_Exceeding_Reading__</th>
        <th>ISAT_Value_Add_Math</th>
        <th>ISAT_Value_Add_Read</th>
        <th>ISAT_Value_Add_Color_Math</th>
        <th>ISAT_Value_Add_Color_Read</th>
        <th>Students_Taking__Algebra__</th>
        <th>Students_Passing__Algebra__</th>
        <th>9th Grade EXPLORE (2009)</th>
        <th>9th Grade EXPLORE (2010)</th>
        <th>10th Grade PLAN (2009)</th>
        <th>10th Grade PLAN (2010)</th>
        <th>Net_Change_EXPLORE_and_PLAN</th>
        <th>11th Grade Average ACT (2011)</th>
        <th>Net_Change_PLAN_and_ACT</th>
        <th>College_Eligibility__</th>
        <th>Graduation_Rate__</th>
        <th>College_Enrollment_Rate__</th>
        <th>college_enrollment</th>
        <th>General_Services_Route</th>
        <th>Freshman_on_Track_Rate__</th>
        <th>x_coordinate</th>
        <th>y_coordinate</th>
        <th>Latitude</th>
        <th>Longitude</th>
        <th>community_area_number</th>
        <th>community_area_name</th>
        <th>Ward</th>
        <th>Police_District</th>
        <th>Location</th>
    </tr>
    <tr>
        <td>610038</td>
        <td>Abraham Lincoln Elementary School</td>
        <td>ES</td>
        <td>615 W Kemper Pl</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60614</td>
        <td>(773) 534-5720</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610038.pdf</td>
        <td>Fullerton Elementary Network</td>
        <td>NORTH-NORTHWEST SIDE COLLABORATIVE</td>
        <td>No</td>
        <td>Standard</td>
        <td>Not on Probation</td>
        <td>Level 1</td>
        <td>Yes</td>
        <td>Very Strong</td>
        <td>99</td>
        <td>Very Strong</td>
        <td>99</td>
        <td>Strong</td>
        <td>74</td>
        <td>Strong</td>
        <td>66</td>
        <td>Strong</td>
        <td>65</td>
        <td>Strong</td>
        <td>70</td>
        <td>Strong</td>
        <td>56</td>
        <td>Average</td>
        <td>47</td>
        <td>96.00%</td>
        <td>2.0</td>
        <td>96.40%</td>
        <td>95.80%</td>
        <td>80.1</td>
        <td>43.3</td>
        <td>89.6</td>
        <td>84.9</td>
        <td>60.7</td>
        <td>62.6</td>
        <td>81.9</td>
        <td>85.2</td>
        <td>52</td>
        <td>62.4</td>
        <td>66.3</td>
        <td>77.9</td>
        <td>69.7</td>
        <td>64.4</td>
        <td>0.2</td>
        <td>0.9</td>
        <td>Yellow</td>
        <td>Green</td>
        <td>67.1</td>
        <td>54.5</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>813</td>
        <td>33</td>
        <td>NDA</td>
        <td>1171699.458</td>
        <td>1915829.428</td>
        <td>41.92449696</td>
        <td>-87.64452163</td>
        <td>7</td>
        <td>LINCOLN PARK</td>
        <td>43</td>
        <td>18</td>
        <td>(41.92449696, -87.64452163)</td>
    </tr>
    <tr>
        <td>610281</td>
        <td>Adam Clayton Powell Paideia Community Academy Elementary School</td>
        <td>ES</td>
        <td>7511 S South Shore Dr</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60649</td>
        <td>(773) 535-6650</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610281.pdf</td>
        <td>Skyway Elementary Network</td>
        <td>SOUTH SIDE COLLABORATIVE</td>
        <td>No</td>
        <td>Track_E</td>
        <td>Not on Probation</td>
        <td>Level 1</td>
        <td>No</td>
        <td>Average</td>
        <td>54</td>
        <td>Strong</td>
        <td>66</td>
        <td>Strong</td>
        <td>74</td>
        <td>Very Strong</td>
        <td>84</td>
        <td>Strong</td>
        <td>63</td>
        <td>Strong</td>
        <td>76</td>
        <td>Weak</td>
        <td>46</td>
        <td>Average</td>
        <td>50</td>
        <td>95.60%</td>
        <td>15.7</td>
        <td>95.30%</td>
        <td>100.00%</td>
        <td>62.4</td>
        <td>51.7</td>
        <td>21.9</td>
        <td>15.1</td>
        <td>29</td>
        <td>42.8</td>
        <td>38.5</td>
        <td>27.4</td>
        <td>44.8</td>
        <td>42.7</td>
        <td>14.1</td>
        <td>34.4</td>
        <td>16.8</td>
        <td>16.5</td>
        <td>0.7</td>
        <td>1.4</td>
        <td>Green</td>
        <td>Green</td>
        <td>17.2</td>
        <td>27.3</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>521</td>
        <td>46</td>
        <td>NDA</td>
        <td>1196129.985</td>
        <td>1856209.466</td>
        <td>41.76032435</td>
        <td>-87.55673627</td>
        <td>43</td>
        <td>SOUTH SHORE</td>
        <td>7</td>
        <td>4</td>
        <td>(41.76032435, -87.55673627)</td>
    </tr>
    <tr>
        <td>610185</td>
        <td>Adlai E Stevenson Elementary School</td>
        <td>ES</td>
        <td>8010 S Kostner Ave</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60652</td>
        <td>(773) 535-2280</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610185.pdf</td>
        <td>Midway Elementary Network</td>
        <td>SOUTHWEST SIDE COLLABORATIVE</td>
        <td>No</td>
        <td>Standard</td>
        <td>Not on Probation</td>
        <td>Level 2</td>
        <td>No</td>
        <td>Strong</td>
        <td>61</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>Average</td>
        <td>50</td>
        <td>Weak</td>
        <td>36</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>Average</td>
        <td>47</td>
        <td>Weak</td>
        <td>41</td>
        <td>95.70%</td>
        <td>2.3</td>
        <td>94.70%</td>
        <td>98.30%</td>
        <td>53.7</td>
        <td>26.6</td>
        <td>38.3</td>
        <td>34.7</td>
        <td>43.7</td>
        <td>57.3</td>
        <td>48.8</td>
        <td>39.2</td>
        <td>46.8</td>
        <td>44</td>
        <td>7.5</td>
        <td>21.9</td>
        <td>18.3</td>
        <td>15.5</td>
        <td>-0.9</td>
        <td>-1.0</td>
        <td>Red</td>
        <td>Red</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>1324</td>
        <td>44</td>
        <td>NDA</td>
        <td>1148427.165</td>
        <td>1851012.215</td>
        <td>41.74711093</td>
        <td>-87.73170248</td>
        <td>70</td>
        <td>ASHBURN</td>
        <td>13</td>
        <td>8</td>
        <td>(41.74711093, -87.73170248)</td>
    </tr>
    <tr>
        <td>609993</td>
        <td>Agustin Lara Elementary Academy</td>
        <td>ES</td>
        <td>4619 S Wolcott Ave</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60609</td>
        <td>(773) 535-4389</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_609993.pdf</td>
        <td>Pershing Elementary Network</td>
        <td>SOUTHWEST SIDE COLLABORATIVE</td>
        <td>No</td>
        <td>Track_E</td>
        <td>Not on Probation</td>
        <td>Level 1</td>
        <td>No</td>
        <td>Average</td>
        <td>56</td>
        <td>Average</td>
        <td>44</td>
        <td>Average</td>
        <td>45</td>
        <td>Weak</td>
        <td>37</td>
        <td>Strong</td>
        <td>65</td>
        <td>Average</td>
        <td>48</td>
        <td>Average</td>
        <td>53</td>
        <td>Strong</td>
        <td>58</td>
        <td>95.50%</td>
        <td>10.4</td>
        <td>95.80%</td>
        <td>100.00%</td>
        <td>76.9</td>
        <td>NDA</td>
        <td>26</td>
        <td>24.7</td>
        <td>61.8</td>
        <td>49.7</td>
        <td>39.2</td>
        <td>27.2</td>
        <td>69.7</td>
        <td>60.6</td>
        <td>9.1</td>
        <td>18.2</td>
        <td>11.1</td>
        <td>9.6</td>
        <td>0.9</td>
        <td>2.4</td>
        <td>Green</td>
        <td>Green</td>
        <td>42.9</td>
        <td>25</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>556</td>
        <td>42</td>
        <td>NDA</td>
        <td>1164504.290</td>
        <td>1873959.199</td>
        <td>41.80975690</td>
        <td>-87.67214460</td>
        <td>61</td>
        <td>NEW CITY</td>
        <td>20</td>
        <td>9</td>
        <td>(41.8097569, -87.6721446)</td>
    </tr>
    <tr>
        <td>610513</td>
        <td>Air Force Academy High School</td>
        <td>HS</td>
        <td>3630 S Wells St</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60609</td>
        <td>(773) 535-1590</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610513.pdf</td>
        <td>Southwest Side High School Network</td>
        <td>SOUTHWEST SIDE COLLABORATIVE</td>
        <td>NDA</td>
        <td>Standard</td>
        <td>Not on Probation</td>
        <td>Not Enough Data</td>
        <td>Yes</td>
        <td>Average</td>
        <td>49</td>
        <td>Strong</td>
        <td>60</td>
        <td>Strong</td>
        <td>60</td>
        <td>Average</td>
        <td>55</td>
        <td>Average</td>
        <td>45</td>
        <td>Average</td>
        <td>54</td>
        <td>Average</td>
        <td>53</td>
        <td>Average</td>
        <td>49</td>
        <td>93.30%</td>
        <td>15.6</td>
        <td>96.90%</td>
        <td>100.00%</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>14.6</td>
        <td>14.8</td>
        <td>NDA</td>
        <td>16</td>
        <td>1.4</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>302</td>
        <td>40</td>
        <td>91.8</td>
        <td>1175177.622</td>
        <td>1880745.126</td>
        <td>41.82814609</td>
        <td>-87.63279369</td>
        <td>34</td>
        <td>ARMOUR SQUARE</td>
        <td>11</td>
        <td>9</td>
        <td>(41.82814609, -87.63279369)</td>
    </tr>
    <tr>
        <td>610212</td>
        <td>Albany Park Multicultural Academy</td>
        <td>MS</td>
        <td>4929 N Sawyer Ave</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60625</td>
        <td>(773) 534-5108</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610212.pdf</td>
        <td>O&#x27;Hare Elementary Network</td>
        <td>NORTH-NORTHWEST SIDE COLLABORATIVE</td>
        <td>Yes</td>
        <td>Standard</td>
        <td>Not on Probation</td>
        <td>Level 1</td>
        <td>No</td>
        <td>Strong</td>
        <td>66</td>
        <td>Weak</td>
        <td>37</td>
        <td>Strong</td>
        <td>66</td>
        <td>Strong</td>
        <td>71</td>
        <td>Average</td>
        <td>43</td>
        <td>Average</td>
        <td>50</td>
        <td>Weak</td>
        <td>46</td>
        <td>Average</td>
        <td>51</td>
        <td>97.00%</td>
        <td>2.3</td>
        <td>96.90%</td>
        <td>100.00%</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>60.7</td>
        <td>39.8</td>
        <td>53.7</td>
        <td>59.8</td>
        <td>17.5</td>
        <td>20.8</td>
        <td>34.5</td>
        <td>15.6</td>
        <td>0.2</td>
        <td>0.3</td>
        <td>Yellow</td>
        <td>Yellow</td>
        <td>29.2</td>
        <td>50</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>266</td>
        <td>31</td>
        <td>NDA</td>
        <td>1153858.196</td>
        <td>1932691.891</td>
        <td>41.97114330</td>
        <td>-87.70962725</td>
        <td>14</td>
        <td>ALBANY PARK</td>
        <td>39</td>
        <td>17</td>
        <td>(41.9711433, -87.70962725)</td>
    </tr>
    <tr>
        <td>609720</td>
        <td>Albert G Lane Technical High School</td>
        <td>HS</td>
        <td>2501 W Addison St</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60618</td>
        <td>(773) 534-5400</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_609720.pdf</td>
        <td>North-Northwest Side High School Network</td>
        <td>NORTH-NORTHWEST SIDE COLLABORATIVE</td>
        <td>Yes</td>
        <td>Standard</td>
        <td>Not on Probation</td>
        <td>Level 1</td>
        <td>No</td>
        <td>Very Strong</td>
        <td>88</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>Strong</td>
        <td>62</td>
        <td>Average</td>
        <td>52</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>96.30%</td>
        <td>2.1</td>
        <td>96.20%</td>
        <td>99.40%</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>19.1</td>
        <td>19.5</td>
        <td>19.9</td>
        <td>20.1</td>
        <td>1</td>
        <td>23.4</td>
        <td>3.5</td>
        <td>67.9</td>
        <td>92.2</td>
        <td>79.8</td>
        <td>4368</td>
        <td>35</td>
        <td>90.7</td>
        <td>1158975.392</td>
        <td>1923791.705</td>
        <td>41.94661693</td>
        <td>-87.69105603</td>
        <td>5</td>
        <td>NORTH CENTER</td>
        <td>47</td>
        <td>19</td>
        <td>(41.94661693, -87.69105603)</td>
    </tr>
    <tr>
        <td>610342</td>
        <td>Albert R Sabin Elementary Magnet School</td>
        <td>ES</td>
        <td>2216 W Hirsch St</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60622</td>
        <td>(773) 534-4491</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610342.pdf</td>
        <td>Fulton Elementary Network</td>
        <td>WEST SIDE COLLABORATIVE</td>
        <td>No</td>
        <td>Standard</td>
        <td>Probation</td>
        <td>Level 3</td>
        <td>No</td>
        <td>Strong</td>
        <td>67</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>Weak</td>
        <td>30</td>
        <td>Very Weak</td>
        <td>18</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>94.70%</td>
        <td>28.1</td>
        <td>95.00%</td>
        <td>100.00%</td>
        <td>56.3</td>
        <td>NDA</td>
        <td>33.5</td>
        <td>33.5</td>
        <td>49.5</td>
        <td>49.5</td>
        <td>27.4</td>
        <td>39.3</td>
        <td>35.5</td>
        <td>44.4</td>
        <td>25</td>
        <td>23.4</td>
        <td>18.0</td>
        <td>12.8</td>
        <td>-1.8</td>
        <td>0.1</td>
        <td>Red</td>
        <td>Yellow</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>620</td>
        <td>35</td>
        <td>NDA</td>
        <td>1161265.299</td>
        <td>1909314.592</td>
        <td>41.90684338</td>
        <td>-87.68304259</td>
        <td>24</td>
        <td>WEST TOWN</td>
        <td>1</td>
        <td>14</td>
        <td>(41.90684338, -87.68304259)</td>
    </tr>
    <tr>
        <td>610524</td>
        <td>Alcott High School for the Humanities</td>
        <td>HS</td>
        <td>2957 N Hoyne Ave</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60618</td>
        <td>(773) 534-5979</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610524.pdf</td>
        <td>North-Northwest Side High School Network</td>
        <td>NORTH-NORTHWEST SIDE COLLABORATIVE</td>
        <td>NDA</td>
        <td>Standard</td>
        <td>Not on Probation</td>
        <td>Not Enough Data</td>
        <td>No</td>
        <td>Strong</td>
        <td>70</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>Strong</td>
        <td>67</td>
        <td>Average</td>
        <td>51</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>Strong</td>
        <td>57</td>
        <td>Weak</td>
        <td>43</td>
        <td>92.70%</td>
        <td>7.1</td>
        <td>96.90%</td>
        <td>100.00%</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>14.7</td>
        <td>13.7</td>
        <td>NDA</td>
        <td>16</td>
        <td>1.3</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>232</td>
        <td>33</td>
        <td>87.6</td>
        <td>1161870.556</td>
        <td>1919857.440</td>
        <td>41.93576106</td>
        <td>-87.68052441</td>
        <td>5</td>
        <td>NORTH CENTER</td>
        <td>1</td>
        <td>19</td>
        <td>(41.93576106, -87.68052441)</td>
    </tr>
    <tr>
        <td>610209</td>
        <td>Alessandro Volta Elementary School</td>
        <td>ES</td>
        <td>4950 N Avers Ave</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>60625</td>
        <td>(773) 534-5080</td>
        <td>http://schoolreports.cps.edu/SchoolProgressReport_Eng/Spring2011Eng_610209.pdf</td>
        <td>O&#x27;Hare Elementary Network</td>
        <td>NORTH-NORTHWEST SIDE COLLABORATIVE</td>
        <td>No</td>
        <td>Track_E</td>
        <td>Not on Probation</td>
        <td>Level 2</td>
        <td>No</td>
        <td>Average</td>
        <td>43</td>
        <td>Strong</td>
        <td>61</td>
        <td>Weak</td>
        <td>28</td>
        <td>Weak</td>
        <td>37</td>
        <td>Strong</td>
        <td>62</td>
        <td>Average</td>
        <td>56</td>
        <td>Average</td>
        <td>51</td>
        <td>Average</td>
        <td>53</td>
        <td>96.40%</td>
        <td>22.5</td>
        <td>95.90%</td>
        <td>100.00%</td>
        <td>63.9</td>
        <td>43.2</td>
        <td>51.3</td>
        <td>32.9</td>
        <td>50.7</td>
        <td>70</td>
        <td>52.5</td>
        <td>31.3</td>
        <td>59.8</td>
        <td>57.6</td>
        <td>16.5</td>
        <td>24.7</td>
        <td>19.9</td>
        <td>14.2</td>
        <td>0.3</td>
        <td>-0.4</td>
        <td>Yellow</td>
        <td>Yellow</td>
        <td>31.6</td>
        <td>65.2</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>NDA</td>
        <td>1023</td>
        <td>31</td>
        <td>NDA</td>
        <td>1149774.095</td>
        <td>1932831.151</td>
        <td>41.97160605</td>
        <td>-87.72464139</td>
        <td>14</td>
        <td>ALBANY PARK</td>
        <td>39</td>
        <td>17</td>
        <td>(41.97160605, -87.72464139)</td>
    </tr>
</table>



### Problem 7

##### What is the average school Safety Score? 


```python
%sql SELECT AVG(safety_score) FROM CHICAGO_PUBLIC_SCHOOLS 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>49.504873</td>
    </tr>
</table>



### Problem 8

##### List the top 5 Community Areas by average College Enrollment [number of students] 


```python
%sql SELECT community_area_name, AVG(college_enrollment) AS AVERAGE_ENROLLMENT FROM CHICAGO_PUBLIC_SCHOOLS \
group by community_area_name \
order by AVERAGE_ENROLLMENT desc LIMIT 5
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>community_area_name</th>
        <th>average_enrollment</th>
    </tr>
    <tr>
        <td>ARCHER HEIGHTS</td>
        <td>2411.500000</td>
    </tr>
    <tr>
        <td>MONTCLARE</td>
        <td>1317.000000</td>
    </tr>
    <tr>
        <td>WEST ELSDON</td>
        <td>1233.333333</td>
    </tr>
    <tr>
        <td>BRIGHTON PARK</td>
        <td>1205.875000</td>
    </tr>
    <tr>
        <td>BELMONT CRAGIN</td>
        <td>1198.833333</td>
    </tr>
</table>



### Problem 9

##### Use a sub-query to determine which Community Area has the least value for school Safety Score? 


```python
%sql SELECT community_area_name, safety_score FROM CHICAGO_PUBLIC_SCHOOLS \
    order by safety_score asc nulls last LIMIT 1 
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>community_area_name</th>
        <th>safety_score</th>
    </tr>
    <tr>
        <td>WASHINGTON PARK</td>
        <td>1</td>
    </tr>
</table>



### Problem 10

##### [Without using an explicit JOIN operator] Find the Per Capita Income of the Community Area which has a school Safety Score of 1.


```python
%sql SELECT CD.per_capita_income, CPS.community_area_name, CPS.safety_score \
    FROM CENSUS_DATA CD, CHICAGO_PUBLIC_SCHOOLS CPS \
    WHERE CD.community_area_number = CPS.community_area_number \
    AND CPS.safety_score = 1;
```

     * ibm_db_sa://smg47194:***@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000/BLUDB
    Done.





<table>
    <tr>
        <th>per_capita_income</th>
        <th>community_area_name</th>
        <th>safety_score</th>
    </tr>
    <tr>
        <td>13785</td>
        <td>WASHINGTON PARK</td>
        <td>1</td>
    </tr>
</table>



Copyright &copy; 2018 [cognitiveclass.ai](cognitiveclass.ai?utm_source=bducopyrightlink&utm_medium=dswb&utm_campaign=bdu). This notebook and its source code are released under the terms of the [MIT License](https://bigdatauniversity.com/mit-license/).

