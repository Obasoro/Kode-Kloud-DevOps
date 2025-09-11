## Task

-------------
Installation of Postqresql

--------------


## Solution

```
log into the database server

systemctl start postgresql

systemctl status postgresql

sudo -u postgres psql
CREATE USER <Username> WITH PASSWORD 'hdyryAkfk';

CREATE DATABASE <database_name>;

GRANT ALL PRIVILEGES ON DATABASE <database_name> to <username>;
```



