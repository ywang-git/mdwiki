#String Algorithms
##Sort
###LSD String Sort
```

```

###MSD String Sort
```
public class MSD
	if (d < s.length()) return s.charAt(d); else return -1;  
}
Small subarrays are of critical importance in the performance of MSD string sort. We have seen this situation for other recursive sorts (quicksort and mergesort), but it is much more dramatic for MSD string sort. For example, suppose that you are sorting millions of ASCII strings (R = 256) that are all different, with no cutoff for small subarrays. Each string eventually finds its way to its own subarray, so you will sort millions of subarrays of size 1. But each such sort involves initializing the 258 entries of the count[] array to 0 and transforming them all to indices. This cost is likely to dominate the rest of the sort. With Unicode (R = 65536) the sort might be thousands of times slower. 
```
public class Quick3string



performance characteristics:
Search hits take time proportional to the length of the search key
Search misses involve examining only a few characters

Tries(prefix tree)

Basic properties.
each node has R links (null links)
link value -> character
node value -> null / the value associated with one of the string keys in the symbol table

nodes with null values exist to facilitate search in the trie and do not correspond to keys


BOTTOM LINE: do not try to use trie for large numbers of long keys taken from large alphabets.


##Suffix arrays
Longest repeated substring.


