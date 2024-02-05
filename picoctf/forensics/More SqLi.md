We have been given a login page which we can bypass using the payload 'Or 1=1;-- </br></br>
It basically does an SQL injection which changes the query to something like SELECT id FROM users WHERE password = '' or 1=1;--' and username = 'abc'. 
This essentially bypasses the need for the username and password and we are directed to the Welcome page. </br></br>
We can test some queries to find out, what DB is used, and with this query:</br> ' UNION SELECT 1, sqlite_version(), 3;-- </br>
In this case, the injected SELECT statement only includes the sqlite_version() function, which retrieves the version of the SQLite database. 
The UNION operator is used to combine the results of this new query with the original query's results. Hence we know that sqlite is being used.</br></br>
Now we can just list all tables with this query:</br>
' UNION SELECT name, sql, null from sqlite_master;--</br></br>

We can now get the flag using:</br>
123' UNION SELECT flag, null, null from more_table;--
