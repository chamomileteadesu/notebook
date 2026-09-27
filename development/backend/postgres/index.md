# PostgreSQL

## [[psql]]

PSQL is a client of Postgres.

## [[metadata]]

Manage cluster metadata.

## [[data_types]]

Show types supported in Postgres.

## Database Manipulation

```sql
-- create a databse
CREATE DATABASE mydb;
-- savely
CREATE DATABASE IF NOT EXISTS mydb;
-- specify encoding
CREATE DATABASE mydb WITH ENCODING 'UTF8';

-- drop a database
DROP DATABASE mydb;
-- savely
DROP DATABASE IF EXISTS mydb;

-- show current database
SELECT current_database();
```

## Table Manipulation

```sql
-- create a table
CREATE TABLE users(
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email TEXT NOT NULL,
    age INTEGER CHECK (age > 0 AND age < 150),
    status CHAR(1) DEFAULT 'A',
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- better to use the following statement rather than 'SERIAL' 
CREATE TABLE users(
    id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY
);

-- add table-level comment
COMMENT ON TABLE users IS 'the user table';
-- add column-level comment
COMMENT ON COLUMN users.username IS 'user full name';

-- alter table name
ALTER TABLE users RENAME TO members;

-- truncate table
TRUNCATE TABLE users;
-- truncate table and reset any related sequence object.
TRUNCATE TABLE users RESTART IDENTITY;

-- drop table
DROP TABLE users;
-- cascade drop table
DROP TABLE IF EXISTS users CASCADE;
```

## Column Manipulation

```sql
-- add column
ALTER TABLE users ADD COLUMN phone VARCHAR(32);
-- drop column
ALTER TABLE users DROP COLUMN phone;

-- modify column type
ALTER TABLE users ALTER COLUMN phone TYPE TEXT;
-- modify column property
ALTER TABLE users ALTER COLUMN status SET DEFAULT 'A';
ALTER TABLE users ALTER COLUMN status DROP DEFAULT;
ALTER TABLE users ALTER COLUMN email SET NOT NULL;
ALTER TABLE users ALTER COLUMN email DROP NOT NULL;
-- rename column
ALTER TABLE users RENAME COLUMN phone TO mobile;
```

## Data Manipulation Language

### Insert Data

```sql
-- insert data
INSERT INTO users (username, email) VALUES ('alice', 'alice@example.com');
-- batch insert
INSERT INTO users (username, email) VALUES
    ('bob', 'bob@example.com'),
    ('charlie', 'charlie@example.com');
-- insert and return some fields（Postgres only）
INSERT INTO users (username, email)
VALUES ('dave', 'dave@example.com')
RETURNING id, email;
-- insert the result of a subquery
INSERT INTO users_backup
SELECT * FROM users WHERE id = 1;
```

### Update Data

```sql
-- update 
UPDATE users
SET email = 'bar@example.com'
WHERE id = 1;
-- update and return the result
UPDATE users
SET email = 'new@example.com'
WHERE id = 1
RETURNING *;
```

### Upsert Data

```sql
-- upsert
-- if a conflict occurs, specified fields will be overwritten
INSERT INTO users (id, username, email)
VALUES (1, 'foo', 'foo@example.com')
ON CONFLICT (id) DO UPDATE SET email = EXCLUDED.email;
-- upsert
-- if a conflict occurs, do nothing
INSERT INTO users (username, email)
VALUES ('foo', 'foo@example.com')
ON CONFLICT DO NOTHING;
```

### Delete Data

```sql
DELETE FROM users WHERE id = 1;
-- delete and return the result
DELETE FROM users WHERE status = 'I' RETURNING *;
```

## Data Query

```sql
-- specify wanted field
SELECT id, username FROM users;

-- filter after scanning users
SELECT * FROM users WHERE status = 'A';

-- deduplication
SELECT DISTINCT status FROM users;

-- sort
SELECT * FROM users ORDER BY created_at DESC;

-- pagination
-- example: skip the first 20 rows and return the next 10 rows
-- alway use ORDER BY: the result order is not guaranteed
-- performance: avoid large OFFSET in production
SELECT * FROM users ORDER BY id ASC LIMIT 10 OFFSET 20;

-- pattern matching
-- start with A
SELECT * FROM users WHERE username LIKE 'a%';
-- exactly two characters
SELECT * FROM users WHERE username LIKE '__';
-- regex match
SELECT * FROM users WHERE email ~ '^[a-z]+@';
-- regex match(ignore case)
SELECT * FROM users WHERE email ~* '^[A-Z]+@';

-- IN statement
SELECT * FROM users WHERE status IN ('A', 'B', 'C');
-- BETWEEN statement
SELECT * FROM users WHERE age BETWEEN 18 AND 30;
-- CASE WHEN statement
SELECT username,
    CASE status
        WHEN 'A' THEN 'active'
        WHEN 'I' THEN 'inactive'
        ELSE 'unknown'
    END AS status_text
FROM users;
```

## index

```sql
-- create a common index
CREATE INDEX idx_users_email ON users(email);
-- create a unique index
CREATE UNIQUE INDEX idx_users_username ON users(username);
-- create a compound index
CREATE INDEX idx_users_status_created ON users(status, created_at DESC);
-- create a partial index
CREATE INDEX idx_active_users ON users(username) WHERE status = 'A';
-- create a expression index
CREATE INDEX idx_users_lower_email ON users(LOWER(email));
-- create a GIN index
CREATE INDEX idx_users_data ON users USING GIN(data);
-- drop a index
DROP INDEX idx_users_email;
```

## Aggregate Functions and Common Functions

```sql
COUNT(*)
COUNT(DISTINCT col)  -- 去重计数
SUM(col)         -- 求和
AVG(col)         -- 平均值
MAX(col) / MIN(col)  -- 最大/最小值
STRING_AGG(col, ',') -- 字符串聚合
ARRAY_AGG(col)   -- 数组聚合
----------------- 字符串函数
CONCAT('a', 'b', 'c')       -- 字符串拼接 -> 'abc'
'Hello' || ' ' || 'World'   -- 拼接操作符 -> 'Hello World'
LOWER('ABC')                -- 转小写 -> 'abc'
UPPER('abc')                -- 转大写 -> 'ABC'
LENGTH('hello')             -- 长度 -> 5
LPAD('42', 5, '0')          -- 左填充 -> '00042'
RPAD('42', 5, '0')          -- 右填充 -> '42000'
TRIM('  hello  ')           -- 去除两端空格 -> 'hello'
SUBSTRING('hello' FROM 2 FOR 3)  -- 子串 -> 'ell'
REPLACE('hello', 'l', 'L')  -- 替换 -> 'heLLo'
SPLIT_PART('a,b,c', ',', 2) -- 分割取值 -> 'b'
----------------- 数值函数
CEIL(3.2)        -- 向上取整 -> 4
FLOOR(3.8)       -- 向下取整 -> 3
ROUND(3.14159, 2)-- 四舍五入 -> 3.14
TRUNC(3.14159, 2)-- 截断 -> 3.14
MOD(10, 3)       -- 取模 -> 1
ABS(-5)          -- 绝对值 -> 5
RANDOM()         -- 随机数 [0, 1)
----------------- 日期时间函数
CURRENT_DATE     -- 当前日期
CURRENT_TIME     -- 当前时间
CURRENT_TIMESTAMP / NOW()  -- 当前时间戳
EXTRACT(YEAR FROM NOW())   -- 提取年份
DATE_TRUNC('month', NOW()) -- 截断到月初
AGE(timestamp1, timestamp2)-- 计算时间差
NOW() + INTERVAL '1 day'   -- 日期加减
NOW() - INTERVAL '2 hours'
date1 - date2              -- 两个日期相差天数
----------------- NULL 处理
COALESCE(col1, col2, 'default')  -- 返回第一个非 NULL 值
NULLIF(a, b)     -- 如果 a = b 返回 NULL，否则返回 a
```

## View

```sql
-- create a view
CREATE VIEW active_users AS
SELECT id, username, email
FROM users
WHERE status = 'A';
-- 创建或替换视图
CREATE OR REPLACE VIEW active_users AS
SELECT id, username, email, created_at
FROM users
WHERE status = 'A';
-- 创建带 CHECK OPTION 的视图
CREATE VIEW young_users AS
SELECT * FROM users WHERE age < 30
WITH CHECK OPTION;  -- 通过视图插入/更新时强制检查条件
-- 删除视图
DROP VIEW active_users;
DROP VIEW IF EXISTS active_users CASCADE;
-- 物化视图（缓存查询结果）
CREATE MATERIALIZED VIEW user_stats AS
SELECT status, COUNT(*) as cnt FROM users GROUP BY status;
-- 刷新物化视图
REFRESH MATERIALIZED VIEW user_stats;
REFRESH MATERIALIZED VIEW CONCURRENTLY user_stats;  -- 并发刷新，不阻塞读
```

## 集合操作

```sql
-- 并集（去重）
SELECT username FROM users_a
UNION
SELECT username FROM users_b;
-- 并集（保留重复）
SELECT username FROM users_a
UNION ALL
SELECT username FROM users_b;
-- 交集
SELECT username FROM users_a
INTERSECT
SELECT username FROM users_b;
-- 差集
SELECT username FROM users_a
EXCEPT
SELECT username FROM users_b;
```

## 连接查询

```sql
-- 内连接
SELECT u.username, o.order_id
FROM users u
INNER JOIN orders o ON u.id = o.user_id;
-- 左外连接
SELECT u.username, o.order_id
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
-- 右外连接
SELECT u.username, o.order_id
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
-- 全外连接
SELECT u.username, o.order_id
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;
-- 交叉连接（笛卡尔积）
SELECT * FROM users CROSS JOIN products;
```

## 子查询

```sql
-- 标量子查询
SELECT username,
    (SELECT COUNT(*) FROM orders WHERE user_id = users.id) AS order_count
FROM users;
-- IN 子查询
SELECT * FROM users
WHERE id IN (SELECT user_id FROM orders WHERE amount > 100);
-- EXISTS 子查询
SELECT * FROM users u
WHERE EXISTS (SELECT 1 FROM orders WHERE user_id = u.id);
-- 派生表
SELECT * FROM (
    SELECT username, COUNT(*) as cnt
    FROM users GROUP BY username
) AS t
WHERE cnt > 1;
```

## CTE（公用表表达式）

```sql
-- 基本 CTE
WITH active_users AS (
    SELECT * FROM users WHERE status = 'A'
)
SELECT * FROM active_users WHERE age > 18;
-- 多个 CTE
WITH
    active AS (SELECT * FROM users WHERE status = 'A'),
    young AS (SELECT * FROM active WHERE age < 30)
SELECT * FROM young;
-- 递归 CTE（如查询组织树）
WITH RECURSIVE org_tree AS (
    -- 基础查询（根节点）
    SELECT id, name, parent_id, 1 AS level
    FROM departments
    WHERE parent_id IS NULL
    UNION ALL
    -- 递归查询
    SELECT d.id, d.name, d.parent_id, t.level + 1
    FROM departments d
    INNER JOIN org_tree t ON d.parent_id = t.id
)
SELECT * FROM org_tree ORDER BY level;
```

## 窗口函数

```sql
-- ROW_NUMBER：行号
SELECT username, created_at,
    ROW_NUMBER() OVER (ORDER BY created_at) AS row_num
FROM users;
-- RANK：排名（有并列会跳过）
SELECT username, score,
    RANK() OVER (ORDER BY score DESC) AS rank
FROM users;
-- DENSE_RANK：密集排名（有并列不跳过）
SELECT username, score,
    DENSE_RANK() OVER (ORDER BY score DESC) AS rank
FROM users;
-- 分区窗口
SELECT dept, username, salary,
    ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC) AS dept_rank
FROM employees;
-- 窗口聚合
SELECT username, salary,
    AVG(salary) OVER () AS company_avg,
    AVG(salary) OVER (PARTITION BY dept) AS dept_avg
FROM employees;
-- LAG / LEAD：前后行值
SELECT username, salary,
    LAG(salary) OVER (ORDER BY id) AS prev_salary,
    LEAD(salary) OVER (ORDER BY id) AS next_salary
FROM employees;
```

## 约束

```sql
CREATE TABLE users (
    id INTEGER GENERATED ALWAYS AS IDENTITY,
    username VARCHAR(50) NOT NULL,
    email TEXT NOT NULL,
    age INTEGER,
    status CHAR(1) DEFAULT 'A',
    dept_id INTEGER,
    -- 主键约束
    PRIMARY KEY (id),
    -- 唯一约束
    UNIQUE (username),
    UNIQUE (email),
    -- 检查约束
    CHECK (age > 0 AND age < 150),
    CHECK (status IN ('A', 'I', 'D')),
    CHECK (email LIKE '%@%'),
    -- 外键约束
    FOREIGN KEY (dept_id) REFERENCES departments(id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
-- 外键的删除策略
-- ON DELETE CASCADE     -- 级联删除
-- ON DELETE SET NULL    -- 设为 NULL
-- ON DELETE SET DEFAULT -- 设为默认值
-- ON DELETE RESTRICT    -- 禁止删除（默认）
-- ON DELETE NO ACTION   -- 延迟检查，效果类似 RESTRICT
-- 添加约束
ALTER TABLE users ADD CONSTRAINT chk_age CHECK (age > 0);
-- 删除约束
ALTER TABLE users DROP CONSTRAINT chk_age;
```

## Sequence

```sql
-- create a sequence
CREATE SEQUENCE user_id_seq
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;

-- get next value
SELECT nextval('user_id_seq');

-- get current value
-- you can only use this function to get the current value if the nextval function has already been called for that sequence
SELECT currval('user_id_seq');

-- set sequene value
-- the parameter 'is_called' defaults to true
-- you get 101 next time
SELECT setval('user_id_seq', 100);
-- you get 100 next time
SELECT setval('user_id_seq', 100, false);

-- drop a sequence
DROP SEQUENCE user_id_seq;
```

## User and Permissions Management

```sql
-- create a user
CREATE USER myuser WITH PASSWORD 'mypassword';
-- alter user password
ALTER USER myuser WITH PASSWORD 'newpassword';
-- drop user
DROP USER myuser;
-- show current user and session user
SELECT CURRENT_USER, SESSION_USER;

-- create a role
CREATE ROLE readonly;

-- grant permissions
-- grant database permissions to user
GRANT CONNECT ON DATABASE mydb TO myuser;
-- grant schema permission to user
GRANT USAGE ON SCHEMA public TO myuser;
-- grant table permission to user
-- fine-grained control
GRANT SELECT, INSERT, UPDATE ON users TO myuser;
-- coarse-grained control
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO myuser;
-- grant sequence permission to user
GRANT USAGE ON ALL SEQUENCES IN SCHEMA public TO myuser;

-- revoke permission
REVOKE INSERT ON users FROM myuser;

-- set default permission
ALTER DEFAULT PRIVILEGES
IN SCHEMA public
GRANT SELECT ON TABLES TO readonly;
```

## Transcation

```sql
-- basic transcation
BEGIN;
    UPDATE accounts SET balance = balance - 100 WHERE id = 1;
    UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- rollback
-- no data is actually deleted
BEGIN;
    DELETE FROM users;
ROLLBACK;

-- partial rollback
-- only 'foo' inserted
BEGIN;
    INSERT INTO users (username) VALUES ('foo');
    SAVEPOINT sp;
    INSERT INTO users (username) VALUES ('bar');
    ROLLBACK TO sp;
COMMIT;

-- isolation level
-- default
BEGIN ISOLATION LEVEL READ COMMITTED;
BEGIN ISOLATION LEVEL REPEATABLE READ;
BEGIN ISOLATION LEVEL SERIALIZABLE;
-- check current isolation level
SHOW transaction_isolation;
```

## Schema

```sql
-- create a schema
CREATE SCHEMA myschema;
-- create a table specifying a schema
CREATE TABLE myschema.users(id SERIAL PRIMARY KEY);

-- drop schema
DROP SCHEMA myschema CASCADE;

-- search path
-- show current search path
SHOW search_path;
-- set search path(for current session)
SET search_path TO schema_a, public;
-- set search path(for user)
ALTER ROLE myuser SET search_path TO schema_a, public;
-- set search path(for database)
ALTER DATABASE mydb SET search_path TO schema_a, public;
```

## JSONB 操作

```sql
-- 创建带 JSONB 列的表
CREATE TABLE events (
    id SERIAL PRIMARY KEY,
    data JSONB NOT NULL
);
-- 插入 JSON 数据
INSERT INTO events (data) VALUES ('{"type": "click", "page": "/home"}');
-- 查询 JSON 字段
SELECT data->>'type' AS event_type FROM events;  -- 返回文本
SELECT data->'page' FROM events;                  -- 返回 JSON
-- 嵌套访问
SELECT data->'user'->>'name' FROM events;
-- 包含查询
SELECT * FROM events WHERE data @> '{"type": "click"}';
-- 存在查询
SELECT * FROM events WHERE data ? 'type';      -- 键存在
SELECT * FROM events WHERE data ?| array['type', 'page'];  -- 任一键存在
SELECT * FROM events WHERE data ?& array['type', 'page'];  -- 所有键存在
-- GIN 索引优化 JSONB 查询
CREATE INDEX idx_events_data ON events USING GIN(data);
```

## Extensions

```sql
-- show installed extensions
SELECT * FROM pg_extension;
-- show available extensions 
SELECT * FROM pg_available_extensions;

-- install a extension
-- uuid generation functions
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
-- key-value store
CREATE EXTENSION IF NOT EXISTS "hstore";
-- geospatial data & gis
CREATE EXTENSION IF NOT EXISTS "postgis";
-- trigram-based fuzzy text search
CREATE EXTENSION IF NOT EXISTS "pg_trgm";
-- automatically logs slow queries with execution plans
CREATE EXTENSION IF NOT EXISTS "auto_explain";
-- tracks query performance and execution statistics
CREATE EXTENSION IF NOT EXISTS "pg_stat_statements";
-- vector similarity search
CREATE EXTENSION IF NOT EXISTS "pg_vector";

-- update a extension
ALTER EXTENSION ext_name UPDATE;

-- generate uuid
SELECT uuid_generate_v4();
-- perform fuzzy search using pg_trgm
SELECT * FROM users
WHERE username % 'alice'
ORDER BY similarity(username, 'alice') DESC;
```

## DBMS Maintenance

```sql
-- VACUUM：回收死元组空间
VACUUM users;             -- 普通清理
VACUUM FULL users;        -- 完全清理（会锁表）
VACUUM ANALYZE users;     -- 清理并更新统计信息
-- ANALYZE：更新统计信息（用于查询优化器）
ANALYZE users;
-- REINDEX：重建索引
REINDEX INDEX idx_users_email;
REINDEX TABLE users;
-- 查看表大小
SELECT pg_size_pretty(pg_total_relation_size('users'));
-- 查看数据库大小
SELECT pg_size_pretty(pg_database_size(current_database()));
-- 查看活动连接
SELECT * FROM pg_stat_activity;
-- 终止连接
SELECT pg_terminate_backend(pid) FROM pg_stat_activity
WHERE datname = 'mydb' AND pid <> pg_backend_pid();
```

## Acces Control using pg_hba.conf

PostgreSQL 使用 `pg_hba.conf` 文件控制客户端访问（而非 MySQL 的 `user@host` 格式）：

```conf
# TYPE  DATABASE  USER  ADDRESS       METHOD
local   all       all                 peer        # Unix socket 本地连接
host    all       all   127.0.0.1/32  scram-sha-256  # 本地 IPv4
host    all       all   ::1/128       scram-sha-256  # 本地 IPv6
host    mydb      myuser 192.168.1.0/24 scram-sha-256  # 局域网访问
host    all       all   0.0.0.0/0     scram-sha-256  # 所有 IP（生产慎用）
```

修改后需重新加载配置：

```sql
SELECT pg_reload_conf();
```
