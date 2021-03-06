
# POSTGRES NOTES
### Load SQL Files in CL:
psql restaurant -f restaurant.sql


COMMAND LINE POSTGRES UTILITIES:
================================
### createuser: 
creates a user

### createdb: 
creates a database

### dropuser: 
deletes a user

### dropdb: 
deletes a database

### postgres: 
executes the SQL server itself (we saw that one above when we checked our Postgres version!)

### pg_dump: 
dumps the contents of a single database to a file

### pg_dumpall: 
dumps all databases to a file

### psql: 
we recognize that one!

*** NOTHING WILL HAPPEN WHEN YOU INPUT ***

ex. createuser patrick --createdb
==========================================

1. postgres -V [ Version Check ] User default 'postgres' off rip

2. psql postgres

3. postgres=# \du = database users AKA roles

4. Create role with psql: *** Always Lowercase ***
CREATE ROLE kethny WITH LOGIN PASSWORD 'Luvm0ther!'

5. ALTER ROLE kethny CREATEDB;

6. CREATE DATABASE kays_database;

7. psql postgres -U kethny

8. CREATE DATABASE super_awesome_application;

9. GRANT ALL PRIVILEGES ON DATABASE super_awesome_application TO julie; 

10. \list =  List Databases
 
11. \connect super_awesome_application 

12. \dt 

13. \password [user]

13. \q

==========================================
\list: lists all the databases in Postgres
\connect: connect to a specific database
\dt: list the tables in the currently connected database
\q: quits
==========================================

ALTER DATABASE [ database culprit ] RENAME TO [ new db name ]; 

- Every Table in Database need Primary Key within database

- When Creating any table:
CREATE TABLE [ table ] (
id serial PRIMARY KEY,
name varchar
);

CREATE TABLE [ table_2 ] (
id serial PRIMARY KEY,
title varchar,
author_id integer REFRENCES author (id)
); // References is the Foreign key that links the two tables

* Author Table is the parent -> Everything else is a child table

=========================
Source Link:
https://pgexercises.com/questions/basic/selectspecific.html

Queries:
[select] * || column [from] table [where] condition [like] '%(string)%'

----------------------------

Matching against multiple possible values:

select * from cd.facilities where facid in (1,5);

----------------------------

Classify results into buckets:

select name, 
	case when (monthlymaintenance > 100) then
		'expensive'
	else
		'cheap'
	end as cost
	from cd.facilities; 

----------------------------

Working with dates:

select memid, surname, firstname, joindate 
	from cd.members
	where joindate >= '2012-09-01';

----------------------------

Removing duplicates, and ordering results

SELECT DISTINCT (no dupes essentially) surname FROM cd.members ORDER BY surname LIMIT 10;          

----------------------------

Combining results FROM multiple queries:

SELECT surname 
    FROM cd.members
UNION
SELECT name
	FROM cd.facilities; 

----------------------------

Simple aggregation

SELECT MAX(joindate) AS latest(new column)
	FROM cd.members;  

----------------------------

More aggregation

select firstname, surname, joindate
	from cd.members
	where joindate = 
		(select max(joindate) 
			from cd.members);

----------------------------
Insert some data into a table

INSERT INTO cd.facilities
    (facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
    VALUES 
    (9, 'Spa', 20, 30, 100000, 800);

or 

insert into cd.facilities values (9, 'Spa', 20, 30, 100000, 800);

----------------------------

Insert multiple rows of data into a table

insert into cd.facilities
    (facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
    values
        (9, 'Spa', 20, 30, 100000, 800),
        (10, 'Squash Court 2', 3.5, 17.5, 5000, 80);   

----------------------------

Update some existing data

update cd.facilities
    set initialoutlay = 10000
    where facid = 1;  

----------------------------
Update multiple rows and columns at the same time

update cd.facilities
    set
        membercost = 6,
        guestcost = 30
    where facid in (0,1); 

----------------------------

Delete all bookings

delete from cd.bookings;

----------------------------

Delete a member from the cd.members table

delete from cd.members where memid = 37;

----------------------------

Delete based on a subquery

delete from cd.members where memid not in (select memid from cd.bookings);          


----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------

----------------------------



