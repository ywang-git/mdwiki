
# Redshift Best Practices

## Tutorial: Tuning Table Design

### Select Sort Keys

1. If recent data is queried most frequently, specify the timestamp column as the leading column for the sort key.
2. If you do frequent range filtering or equality filtering on one column, specify that column as the sort key.
3. If you frequently join a (dimension) table, specify the join column as the sort key.

### Select Distribution Styles

You should assign distribution styles to achieve these goals.

* Collocate the rows from joining tables
When the rows for joining columns are on the same slices, less data needs to be moved during query execution.
* Distribute data evenly among the slices in a cluster.
If data is distributed evenly, workload can be allocated evenly to all the slices.

#### Distribution Styles
KEY distribution

The rows are distributed according to the values in one column. The leader node will attempt to place matching values on the same node slice. If you distribute a pair of tables on the joining keys, the leader node collocates the rows on the slices according to the values in the joining columns so that matching values from the common columns are physically stored together.

ALL distribution

A copy of the entire table is distributed to every node. Where EVEN distribution or KEY distribution place only a portion of a table's rows on each node, ALL distribution ensures that every row is collocated for every join that the table participates in.

EVEN distribution

The rows are distributed across the slices in a round-robin fashion, regardless of the values in any particular column. EVEN distribution is appropriate when a table does not participate in joins or when there is not a clear choice between KEY distribution and ALL distribution. EVEN distribution is the default distribution styl



> Written with [StackEdit](https://stackedit.io/).