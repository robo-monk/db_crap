# Indexing

##  Data Storae TL;DR
### Memory Hierarchy
* register -> cache -> main memory -> hard disk -> tertiary storage
* the more left the cheaper, tertiary storage has 10^9 latency gap witha register, 10^7 capacity gap

### HDD
<img src="images/hdd.png">
<img src="images/hdd_calculate_bs.png">

### Row stores
* Traditional way for storage
* Multiple records stored per page 
* Easy to add new records 
* Efficient often most parts of a record are needed - wastes performance otherwise
* Less efficient for large-scale statistics

### Column stores
* Many newer systems opt for this
* Stores column data in different pages - reconstructing the whole record is hard
* Efficient compression
* Efficient for column-based statistics

## Design Decisions
* use the identifying property of an entity as a primary key
* sort all entities by their primary key - allow for skip-fwd / bisection search
* block all entities and sort by key
	* for each block, indicate first & last contained key
	* ordered sparse block primary index

* build a ordered dense primary index of all keys in the collection

## Primary Index
* created by default for the primary key attributes of a table
* index physically reorders the whole table
* efficient search is possible
* can be augumented with additional data structured to improve access even further

## Secondary Index
* optional indexes for non-primary key attributes
* extremely beneficial for speeding up joins on foreign key constraints
* builds an additional data structure containing the index
* you can have multiple secondary indexes
	* each secondary index tho:
		* costs space, since some data are replicated
		* update the db has more overhead since each update has to be reflected


## Hash-based indexes
* search keys are distributed uniformly across blocks using some hash function
* hashed value of search key decides for storage block

## Tree-based indexes
* search keys are stored in sorted order
* single/multi-level ordered indexes

## Primary Sparse block index
* index record contains pointer to the respective storage place (block address)
* Advantages
	* number of blocks needed for storing the index is small compared to data (not all records are indexed) 
	* can often be kept in buffer
	* insertions deletions require few changes in the index
* Dis
	* quering non-existing data still need access to the data
	* finding a data point might require bringing more blocks in memory than needed

## Primary dense index
* ++
	* existence of records can easily be checked
*  --
	* requires more space than a sparse index
	* requires more updates on insertion/deletion
	
## B-Trees



