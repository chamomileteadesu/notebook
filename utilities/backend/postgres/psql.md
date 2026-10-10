# PSQL

## PSQL Command

```sh
# connect to a postgres instance
# -d: specify a database, defaulting to your OS username if omitted 
# -U: log in the session as this user
psql -d mydb -U postgres
```

## PSQL Client

```sh
# list all databases
\l

# change database
\c DATABASE

# list all tables in current schema
\dt

# list all tables
\dt *.*

# describe table
\d TABLE

# list indices
\di

# list serial
\ds             

# list view
\dv             

# list function
\df             

# list user
\du             

# list privilege
\dp             

# list extensions
\dx             

# 切换扩展显示模式
\x              

# show search time spent
\timing         

# execute sql file
\i file.sql     

# output to file
\o output.txt   

# quit psql
\q              
```
