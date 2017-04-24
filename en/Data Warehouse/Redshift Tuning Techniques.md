#Redshift Tuning Techniques

https://aws.amazon.com/blogs/big-data/top-10-performance-tuning-techniques-for-amazon-redshift/

## 1. Incorrect column encoding

Redshift is column-oriented (data is stored by column, and rows are extracted from column storage at runtime) - well suited to analytics queries on tables with large number of columns (most queries only access a subset of all possible dimensions and measures. 

query only accesses columns in `select` and `where` clause

no index is needed (each column has its own index)

## 2. Skewed table data

## 3. Queries not benefiting from sort keys

## 4. Tables without statistics or which need vacuum

Redshift (like other databases) requires statistics about tables and the composition of data blocks being stored in order to make good decisions when planning a query.

[ANALYZE Command History](http://docs.aws.amazon.com/redshift/latest/dg/c_check_last_analyze.html)

[missing_table_stats.sql](https://github.com/awslabs/amazon-redshift-utils/blob/master/src/AdminScripts/missing_table_stats.sql)

data blocks are immutable. (rows are simply logically deleted)

[VACUUM command](http://docs.aws.amazon.com/redshift/latest/dg/r_VACUUM_command.html)

[perf_alert.sql](https://github.com/awslabs/amazon-redshift-utils/blob/master/src/AdminScripts/perf_alert.sql): identify tables that have had alerts about scanning a large number of delted rows raised in the last seven days

## 5. Tables with very large VARCHAR columns

## 6. Queries waiting on queue slots

## 7. Queries that are disk-based

## 8. Commit queue waits

## 9. Inefficient data loads

## 10. Inefficient use of Temporary Tables



> Written with [StackEdit](https://stackedit.io/).