---
title:  "Resize a column in a PostgreSQL table without changing data"
date:   2019-08-14 14:23:09
categories: postgresql
tags: postgresql, db, database
---

I needed to increase the length of a column without any change in data. I went through stackoverflow as usual :) and found a old article by [sniptools](https://sniptools.com/databases/resize-a-column-in-a-postgresql-table-without-changing-data/) .

The original article was writen in 2009 and few things has to be changed.

TL;DR

<br />

In the below example table name is TAB1 and the column that we want to alter is COL1

To check the existing size, simply run the following query.

```

SELECT atttypmod FROM pg_catalog.pg_attribute 
WHERE attrelid = 'TAB1'::regclass 
AND attname = 'COL1';

```


<br />


The sample result is 

```
attypmod
---------
34
```


This means that the column current size is 30 (4 was added for a legacy reason it seems.)

<br />

Now we can change it to ***varchar(40)*** by executing the following query.


```
UPDATE pg_catalog.pg_attribute SET atttypmod = 40+4
WHERE attrelid = 'TAB1'::regclass
AND attname = 'COL1';
```


<br />


The sample result is

```
UPDATE 1
```

<br />

This can be verified by running ***\d DATABASENAME***

Cheers!!!