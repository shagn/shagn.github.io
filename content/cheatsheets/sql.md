---
title: "SQL"
date: "2025-01-14"
tags: ["stub"]
draft: false
---

## Postgres

### Select query on _jsonb_ column

Example content of the _json_column_name_: `[{"json_key":"json_value"}]`

```sql
-- Get specific value of the first element of an array
SELECT json_column_name -> 0 ->> 'json_key'
FROM table_name
WHERE json_column_name IS NOT NULL AND json_column_name <> '[]'::jsonb;

-- Get length of an JSON array
select jsonb_array_length(json_column_name)
FROM table_name
```

### Check schema

```sql
SELECT 
    column_name, 
    data_type, 
    character_maximum_length,
    column_default,
    is_nullable
FROM 
    information_schema.columns
WHERE 
    table_schema = 'table_schema'
    and table_name = 'table_name';
```

### Create an index

```sql
CREATE INDEX idx_collection_id ON langchain_pg_embedding (collection_id);
```

### Check running activities

```postgres
SELECT pid, state, query
FROM pg_stat_activity
WHERE state != 'idle'
ORDER BY query_start DESC;
```

### Kill a specific activity

1. Via **pg_cancel_backend**

   ```sql
   SELECT pg_cancel_backend(pid);
   ```

   Attempts to cancel the current query, which is safer but might not work if the process is truly idle and not executing any query

1. Via **pg_terminate_backend**

   ```sql
   SELECT pg_terminate_backend(pid);
   ```

   Forcefully closes the connection, which will definitely stop the transaction but might cause issues for the client

### Change ownership of tables

Generate SQL statements to change ownership of tables to an user

```sql
select 'ALTER TABLE ' || t.tablename || ' OWNER TO psr_master;' 
from  pg_tables t
where t.tableowner = 'masterUser'
and schemaname = 'psr'
```

### Creating / Restoring from dumps

Using `pg_dump` and `pg_restore` to migrate the data between Postgres databases

```postgresql
pg_dump -v -h <host_adress> -U <user> -F c -f <file_name> -a --schema=<schema> <database>
pg_restore -v -h <host_adress> -U <user> -a --schema=<schema> -d <database> <file_name>
```

- `-a`: only data
- `-F c`: using custom format -> makes restoring with pg_restore necessary
- `<user>`: can be different ones

## MSSQL

### Show open database connections

```sql
select dbid, loginame, login_time, * 
from sys.sysprocesses
```
