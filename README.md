# postgresql
Repository to save PostgreSQL scripts files

# Configuration File

## postgresql.conf

- Path: /var/lib/pgsql/<verion>/data
- Name: postgresql.conf


## postgresql.auto.conf

- Path: /var/lib/pgsql/<verion>/data
- Name: postgresql.auto.conf

## pg_hba.conf

- Path: /var/lib/pgsql/<verion>/data
- Name: pg_hba.conf

## pg_ident.conf

- Path: /var/lib/pgsql/<verion>/data
- Name: pg_ident.conf

# Authentication and Authorization

## Create a superuser

```postgresql
postgres=# create user diogo with superuser;
CREATE ROLE
postgres=# \password diogo
Enter new password: 
Enter it again: 
```

# Storage Organization

## Create a Database

```postgresql
postgres=# create database pgdb with owner = dhnomura encoding = 'UTF8';
CREATE DATABASE
postgres=# 
```

## Drop database

```sql
drop database [if exists] database_name;
```

# Objects

## Tables

### List all tables

```postgresql
SELECT 
    * 
FROM 
    information_schema.tables;
```

```postgresql
SELECT
    * 
FROM 
    information_schema.tables 
WHERE 
    table_schema = 'schema_name';
```

```postgresql
SELECT 
    *
FROM 
    pg_catalog.pg_tables
WHERE 
    schemaname != 'pg_catalog' AND 
    schemaname != 'information_schema';
```

```postgresql
\dt
\dt+
\dt schema_name.*
```

### List table columns

```postgresql
SELECT
	*
FROM
	information_schema.columns
WHERE
	table_schema = 'schema_name'
	AND table_name = 'table_name';
```

```postgresql
\d+ table_name
```

### Create table

```postgresql
create table actors (
    actor_id SERIAL PRIMARY KEY,
    first_name varchar(150),
    last_name varchar(150) not null,
    gender char(1),
    date_of_birth DATE,
    add_date date,
    update_date date
);
```
```postgresql
create table movies (
    movie_id SERIAL PRIMARY KEY,
    movie_name varchar(100) not null,
    movie_length int,
    movie_lang varchar(20),
    age_certificate varchar(10),
    release_date date,
    director_id int references directors (director_id)
);
```
```postgresql
create table movies_actors (
    movie_id int references movies (movie_id),
    actor_id int references actors (actor_id),
    primary key (movie_id, actor_id)
);
```
### Alter table

```postgresql
alter table accounts add column is_enable varchar(20);
```

### Alter Column

```postgresql
alter table accounts alter column is_enable set not null;
```
```postgresql
alter table accounts alter column is_enable set default 'Y';
```
```postgresql
alter table accounts rename add_date to adddate;
```
```postgresql
alter table accounts drop column bla;
```

### Drop Table

```postgresql
drop table teste_delete;
```

# DML

## Insert data

```postgresql
insert into customers (first_name, last_name, email, age)
values ('Diogo','Nomura','diogo@nomura.com',30);
 ```

```postgresql
insert into customers (first_name, last_name, email, age)
values
    ('a','a','a@a.com',10),
    ('b','b','b@b.com',20),
    ('c','c','c@c.com',30);
```

```postgresql
insert into customers (first_name, last_name, email, age)
values ('Diogo','Nomura','diogo@nomura.com',30) returning *;
 ```

 ## Update data

```postgresql
update customers
set email = 'a2@a.com'
where first_name='a'
returning *;
```

## Delete Data

```postgresql
delete from customers where first_name='a';
```

## Upsert

```postgresql
insert into t_tags(tag) values ('Pen') on conflict do nothing;
```

```postgresql 
insert into t_tags(tag) values ('Pen') on conflict(tag) do update set tag = excluded.tag, update_date = now();
```

## Query Data

## Data Types

- Bolean
- Char, Varchar, Text
- Numeric
- Decimal
- Date, time, timestamp
- UUID
- Array
- hstore
- JSON

# Miscelaneous

## Check connection info

```postgresql
\conninfo
```

```postresql
SELECT session_user, current_user;
```
```postgresql
SELECT current_database();
```

## Change database

```postgresql
\c database
```

## Change user

```postgresql 
\c - newuser
```

```postgresql
SET ROLE <role_name>;
```

## Change database and user

```postgresql
\c database user
```

select * from information_schema.tables where table_name='awsdms_validation_failures_v1';

## Parameters

SELECT current_setting('max_connections');

select * from pg_settings;

show all;
