# simple demo

## create database

```m
SHOW DATABASES;
CREATE DATABASE IF NOT EXISTS mysql_development;
USE mysql_development;
```

## create table

```m
SHOW TABLES;
CREATE TABLE students (name VARCHAR(20), sex CHAR(1), birth DATE);
DESCRIBE students;
```

## create

```m
INSERT INTO students (name, sex, birth) VALUES ("a", "g", "1992-02-01"), ("b", "b", "1992-02-02");
```

## retrieve

```m
SELECT * FROM students;
SELECT name, sex, birth FROM students WHERE name = 'a';
SELECT name AS NAME, sex AS SEX, birth AS BIRTH FROM students;
```

## update

```m
UPDATE students SET name = 'c' WHERE name = 'a';
SELECT * FROM students;
```

## delete

```m
DELETE FROM students WHERE name = 'c';
SELECT * FROM students;
```
