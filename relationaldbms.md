# Relational DBMS
information_schema is a meta-database that holds information about your current database. information_schema has multiple tables you can query with the known SELECT * FROM syntax:

tables: information about all tables in your current database
columns: information about all columns in all of the tables in your current database
```
SELECT column_name, data_type 
FROM information_schema.columns 
WHERE table_name = 'university_professors' AND table_schema = 'public';
```
To add columns you can use the following SQL query:

ALTER TABLE table_name
ADD COLUMN column_name data_type;

Migrating Data
Insert Into tablename
select distinct columnnames
from tablename;

alter table tablename
rename columnname oldname to newname;

insert into tablename(column names)
values(values);

alter table tablename
drop column columnname

When joining tables with a common field name, e.g.
```
SELECT *
FROM countries
  INNER JOIN economies
    ON countries.code = economies.code
You can use USING as a shortcut:

SELECT *
FROM countries
  INNER JOIN economies
    USING(code)
	
	SELECT name, continent, code, surface_area,
    -- 1. First case
    CASE WHEN surface_area > 2000000 THEN 'large'
        -- 2. Second case
        WHEN surface_area > 350000 THEN 'medium'
        -- 3. Else clause + end
        ELSE 'small' END
        -- 4. Alias name
        AS geosize_group
-- 5. From table
FROM countries;
```
