```python
import ibm_db
```


```python
#Replace the placeholder values with your actual Db2 hostname, username, and password:
dsn_hostname = "dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net" # e.g.: "dashdb-txn-sbox-yp-dal09-04.services.dal.bluemix.net"
dsn_uid = "smg47194"        # e.g. "abc12345"
dsn_pwd = "v0b8j^q48gk021x5"      # e.g. "7dBZ3wWt9XN6$o0J"

dsn_driver = "{IBM DB2 ODBC DRIVER}"
dsn_database = "BLUDB"            # e.g. "BLUDB"
dsn_port = "50000"                # e.g. "50000" 
dsn_protocol = "TCPIP"            # i.e. "TCPIP"
```


```python
dsn = (
    "DRIVER={0};"
    "DATABASE={1};"
    "HOSTNAME={2};"
    "PORT={3};"
    "PROTOCOL={4};"
    "UID={5};"
    "PWD={6};").format(dsn_driver, dsn_database, dsn_hostname, dsn_port, dsn_protocol, dsn_uid, dsn_pwd)

#print the connection string to check correct values are specified
print(dsn)
```

    DRIVER={IBM DB2 ODBC DRIVER};DATABASE=BLUDB;HOSTNAME=dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net;PORT=50000;PROTOCOL=TCPIP;UID=smg47194;PWD=v0b8j^q48gk021x5;



```python
try: 
    conn = ibm_db.connect(dsn, "", "")
    print ("connected to database: ", dsn_database, "as user: ", dsn_uid, "on host: ", dsn_hostname)
except:
    print ("unable to connect: ", ibm_db.conn_errormsg())
```

    connected to database:  BLUDB as user:  smg47194 on host:  dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net



```python
server = ibm_db.server_info(conn)

print ("DBMS_NAME: ", server.DBMS_NAME)
print ("DBMS_VER:  ", server.DBMS_VER)
print ("DB_NAME:   ", server.DB_NAME)
```

    DBMS_NAME:  DB2/LINUXX8664
    DBMS_VER:   11.01.0404
    DB_NAME:    BLUDB



```python
client = ibm_db.client_info(conn)

print ("DRIVER_NAME:          ", client.DRIVER_NAME) 
print ("DRIVER_VER:           ", client.DRIVER_VER)
print ("DATA_SOURCE_NAME:     ", client.DATA_SOURCE_NAME)
print ("DRIVER_ODBC_VER:      ", client.DRIVER_ODBC_VER)
print ("ODBC_VER:             ", client.ODBC_VER)
print ("ODBC_SQL_CONFORMANCE: ", client.ODBC_SQL_CONFORMANCE)
print ("APPL_CODEPAGE:        ", client.APPL_CODEPAGE)
print ("CONN_CODEPAGE:        ", client.CONN_CODEPAGE)
```

    DRIVER_NAME:           libdb2.a
    DRIVER_VER:            11.01.0404
    DATA_SOURCE_NAME:      BLUDB
    DRIVER_ODBC_VER:       03.51
    ODBC_VER:              03.01.0000
    ODBC_SQL_CONFORMANCE:  EXTENDED
    APPL_CODEPAGE:         1208
    CONN_CODEPAGE:         1208



```python
#Lets first drop the table INSTRUCTOR in case it exists from a previous attempt
dropQuery = 'drop table INSTRUCTOR'

#Now execute the drop statment
droptstmt = ibm_db.exec_immediate(conn, dropQuery)
```


```python
#Construct the Create Table DDL statement - replace the ... with rest of the statement
createQuery = 'create table INSTRUCTOR (ID integer PRIMARY KEY NOT NULL, FNAME VARCHAR(20), LNAME VARCHAR(20), CITY VARCHAR(20), CCODE CHAR(2))'

#Now fill in the name of the method and execute the statement
createstmt = ibm_db.exec_immediate (conn, createQuery)
```


```python
#Construct the query - replace ... with the insert statement
insertQuery = "insert into INSTRUCTOR values (1, 'Rav', 'Ahuja', 'Toronto', 'CA')"

#execute the insert statement
insertStmt = ibm_db.exec_immediate(conn, insertQuery)
```


```python
#Construct the query - replace ... with the insert statement
insertQuery = "insert into INSTRUCTOR values (2, 'Raul', 'Chong', 'Markham', 'CA')"

#execute the insert statement
insertstmt = ibm_db.exec_immediate (conn, insertQuery)
```


```python
#Construct the query that retrieves all rows from the INSTRUCTOR table
selectQuery = "select * from INSTRUCTOR"

#Execute the statement
selectStmt = ibm_db.exec_immediate(conn, selectQuery)

#Fetch the Dictionary (for the first row only) - replace ... with your code
ibm_db.fetch_both(selectStmt)
```




    {'ID': 1,
     0: 1,
     'FNAME': 'Rav',
     1: 'Rav',
     'LNAME': 'Ahuja',
     2: 'Ahuja',
     'CITY': 'Toronto',
     3: 'Toronto',
     'CCODE': 'CA',
     4: 'CA'}




```python
#now write and execute an update statement that changes the Rav's CITY to MOOSETOWN
updateQuery = "update INSTRUCTOR set CITY = 'MOOSETOWN' where FNAME = 'Rav'"
updateStmt = ibm_db.exec_immediate (conn, updateQuery)
```


```python
import pandas
import ibm_db_dbi
#connection for pandas
pconn = ibm_db_dbi.Connection(conn)
```


```python
#query statement to retrieve all rows in INSTRUCTOR table
selectQuery = "select * FROM INSTRUCTOR"
#retrieve the query results into a pandas dataframe
pdf = pandas.read_sql(selectQuery, pconn)
#print just the LNAME for first row in the pandas data frame
pdf.LNAME[1]
pdf
pdf.shape
```




    (2, 5)




```python
ibm_db.close(conn)
```




    True




```python

```
