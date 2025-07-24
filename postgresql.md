# PostgreSQL

### Manage roles and privileges



```sql
-- connect db server using user postgres
psql -U postgres -d db_name

-- list all users and roles
\du+

SELECT CURRENT_USER;

-- change current user to bob
SET ROLE bob;


SHOW TIMEZONE;
SET timezone = 'Asia/Shanghai';
```

### Manage databases

```sql
CREATE DATABASE db_name;

-- show all the db
\l

-- connect to db using user
\c db_name user_name
```

### Manage schemas

When you create object without schema name, it'll go into `public` schema by default.

```sql
```





### Manage tables

```sql
CREATE TABLE IF NOT EXISTS table_name (
  id SERIAL PRIMARY KEY,
  name VARCHAR (50),
  sex CHAR (1) NOT NULL,
  username VARCHAR (50) UNIQUE NOT NULL,
  email VARCHAR (255) UNIQUE NOT NULL,
  create_time TIMESTAMP default CURRENT_TIMESTAMP NOT NULL,
  update_time TIMESTAMP WITH TIME ZONE default CURRENT_TIMESTAMP NOT NULL
);

-- view table
\d table_name

ALTER TABLE table_name
  ALTER COLUMN column_name TYPE TIMESTAMPTZ,
  ALTER COLUMN column_name TYPE VARCHAR(255);

ALTER TABLE employees
  ADD COLUMN create_time timestamp,
  ADD COLUMN update_time timestamp,
  ADD COLUMN create_by varchar(32),
  ADD COLUMN update_by varchar(32);

DROP TABLE IF EXISTS table_name;


INSERT INTO table_name (column1, update_time)
VALUES (val1, current_timestamp);



UPDATE table_name
SET column1 = 'xyz'
WHERE column2 = 'abc';



CREATE FUNCTION update_timestamp_auto()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_time = now();
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_timestamp_auto
    BEFORE UPDATE
    ON
        table_name
    FOR EACH ROW
EXECUTE PROCEDURE update_timestamp_auto();
```



