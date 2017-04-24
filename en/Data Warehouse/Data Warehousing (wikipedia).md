# Data Warehousing

## Fact table

[Fact Table](https://en.wikipedia.org/wiki/Fact_table)

- consists of measurements, metrics or facts of a business process
- located at the center of a star schema or a snowflake schema surrounded by dimension tables
- fact constellation schema when there are multiple fact tables

two types of columns:
1. contains fact
2. foreign key to dimension tables

primary key is made up of all of its foreign keys

contains the content of the data warehouse and store different types of measures like additive, non additive, and semi additive measures

### mesure types
- additive - measures that can be added across any dimension
- non additive - measures that cannot be added across any dimension
- semi additive - measures that can be added across some dimensions


detailed fact vs aggregated fact (summary table)

**Never store percentages or ratios in fact tables but only calculate these in the data access tool**

factless fact table / junction tables: to model many to many relationships or capture events

### Types
#### transactional
#### periodic snapshots
#### accumulating snapshots
#### temporal snapshots



### star schema?
### snowflake schema
### fact constellation schema
### surrogate keys

### design steps
- identify a business process for analysis (like sales)
- identify meausures 

## dimension tables



> Written with [StackEdit](https://stackedit.io/).