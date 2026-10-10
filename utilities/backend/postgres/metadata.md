# Metadata

Show Postgres Version

```sql
SHOW server_version
select version()
```

List all database(using pg_catalog)

```sql
SELECT datname
FROM pg_catalog.pg_database;
```

List all schemas

```sql
SELECT schema_name
FROM information_schema.schemata;
```

List all tables

```sql
SELECT table_schema, table_name, table_type
FROM information_schema.tables;
```

List all users

```sql
SELECT *
FROM pg_catalog.pg_user;
```

Describe table

```sql
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'users';
```

Show keywords

```sql
SELECT word, resword
FROM pg_get_keywords()
```
