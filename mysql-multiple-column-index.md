## What is multiple-column index?
MySQL can use multiple-column indexes for queries that test all the columns in the index, 
or queries that test just the first column, the first two columns, the first three columns, and so on. 
If you specify the columns in the right order in the index definition, 
a single composite index can speed up several kinds of queries on the same table.

A multiple-column index can be considered a sorted array, 
the rows of which contain values that are created by concatenating the values of the indexed columns.

## Experiment
For our experiment we created 3 different tables with:
- consolidated
- consolidated_single
- consolidated_multi

```
  CREATE TABLE `consolidated` (
	  `consolidated_id` int(11) NOT NULL AUTO_INCREMENT,
	  `pub_id` int(11) DEFAULT NULL,
	  `cp_id` int(11) DEFAULT NULL,
	  `ro_id` int(11) DEFAULT NULL,
	  `country_id` int(11) DEFAULT NULL,
	  `views` int(11) DEFAULT NULL,
	  PRIMARY KEY (`consolidated_id`)
	) ENGINE=InnoDB;


	CREATE TABLE `consolidated_single` (
	  `consolidated_id` int(11) NOT NULL AUTO_INCREMENT,
	  `pub_id` int(11) DEFAULT NULL,
	  `cp_id` int(11) DEFAULT NULL,
	  `ro_id` int(11) DEFAULT NULL,
	  `country_id` int(11) DEFAULT NULL,
	  `views` int(11) DEFAULT NULL,
	  PRIMARY KEY (`consolidated_id`)
	) ENGINE=InnoDB;

	CREATE INDEX idx_1 ON consolidated_single (pub_id);
	CREATE INDEX idx_2 ON consolidated_single (cp_id);
	CREATE INDEX idx_3 ON consolidated_single (ro_id);
	CREATE INDEX idx_4 ON consolidated_single (country_id);

	CREATE TABLE `consolidated_multi` (
	  `consolidated_id` int(11) NOT NULL AUTO_INCREMENT,
	  `pub_id` int(11) DEFAULT NULL,
	  `cp_id` int(11) DEFAULT NULL,
	  `ro_id` int(11) DEFAULT NULL,
	  `country_id` int(11) DEFAULT NULL,
	  `views` int(11) DEFAULT NULL,
	  PRIMARY KEY (`consolidated_id`)
	) ENGINE=InnoDB;

CREATE INDEX idx_1 ON consolidated_multi (pub_id, cp_id, ro_id, country_id);

```
  
## Query and Results
For our reporiting query on the above 3 tables with 3 set of data loaded (6 Million, 10 Million, 20 Million rows).
  
### Query:
```
select pub_id, cp_id, ro_id, country_id, sum(views) 
      from consolidated
      group by pub_id, cp_id, ro_id, country_id;
      
select pub_id, cp_id, ro_id, country_id, sum(views) 
      from consolidated_single
      group by pub_id, cp_id, ro_id, country_id;
      
select pub_id, cp_id, ro_id, country_id, sum(views) 
      from consolidated_multi
      group by pub_id, cp_id, ro_id, country_id;
 ```
  
### Results:
|	Rows	|	No Index	|	Single Index	|	Multi-Column Index
|	-	|	-	|	-	|	-
|	600000	|	3.24 sec	|	3.36 sec	|	0.55 sec
|	1000000	|	3.96 sec	|	4.01 sec	|	1.3 sec
|	2000000	|	9.8 sec	|	9.8 sec	|	2.87 sec

  
  
