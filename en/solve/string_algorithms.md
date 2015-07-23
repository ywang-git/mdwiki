#String Algorithms
##Sort
###LSD String Sort
```  public class LSD  {     public static void sort(String[] a, int W)     {  // Sort a[] on leading W characters.        int N = a.length;        int R = 256;        String[] aux = new String[N];        for (int d = W-1; d >= 0; d--)        { // Sort by key-indexed counting on dth char.           int[] count = new int[R+1];     // Compute frequency counts.           for (int i = 0; i < N; i++)               count[a[i].charAt(d) + 1]++;           for (int r = 0; r < R; r++)     // Transform counts to indices.              count[r+1] += count[r];           for (int i = 0; i < N; i++)     // Distribute.              aux[count[a[i].charAt(d)]++] = a[i];           for (int i = 0; i < N; i++)     // Copy back.              a[i] = aux[i];	    }      }  }

```

###MSD String Sort
```
public class MSD{￼private static int R = 256; // radixprivate static final int M = 15; // cutoff for small subarraysprivate static String[] aux; // auxiliary array for distributionprivate static int charAt(String s, int d){  
	if (d < s.length()) return s.charAt(d); else return -1;  
}public static void sort(String[] a){   int N = a.length;   aux = new String[N];   sort(a, 0, N-1, 0);}private static void sort(String[] a, int lo, int hi, int d){  // Sort from a[lo] to a[hi], starting at the dth character.   if (hi <= lo + M)   {  Insertion.sort(a, lo, hi, d); return;  }	int[] count = new int[R+2];	for (int i = lo; i <= hi; i++) // Compute frequency counts.   		count[charAt(a[i], d) + 2]++;	for (int r = 0; r < R+1; r++) // Transform counts to indices.   		count[r+1] += count[r];	for (int i = lo; i <= hi; i++)	// Distribute.   		aux[count[charAt(a[i], d) + 1]++] = a[i];	for (int i = lo; i <= hi; i++)     // Copy back.   		a[i] = aux[i - lo];	// Recursively sort for each character value.	for (int r = 0; r < R; r++)   		sort(a, lo + count[r], lo + count[r+1] - 1, d+1);} }```
Small subarrays are of critical importance in the performance of MSD string sort. We have seen this situation for other recursive sorts (quicksort and mergesort), but it is much more dramatic for MSD string sort. For example, suppose that you are sorting millions of ASCII strings (R = 256) that are all different, with no cutoff for small subarrays. Each string eventually finds its way to its own subarray, so you will sort millions of subarrays of size 1. But each such sort involves initializing the 258 entries of the count[] array to 0 and transforming them all to indices. This cost is likely to dominate the rest of the sort. With Unicode (R = 65536) the sort might be thousands of times slower. ###Three-way string quick sort
```
public class Quick3string{￼private static int charAt(String s, int d){  if (d < s.length()) return s.charAt(d); else return -1;  }public static void sort(String[] a){  sort(a, 0, a.length - 1, 0);  }private static void sort(String[] a, int lo, int hi, int d){   if (hi <= lo) return;   int lt = lo, gt = hi;   int v = charAt(a[lo], d);   int i = lo + 1;   while (i <= gt)   {      int t = charAt(a[i], d);      if      (t < v) exch(a, lt++, i++);      else if (t > v) exch(a, i, gt--);      else            i++;}   // a[lo..lt-1] < v = a[lt..gt] < a[gt+1..hi]   sort(a, lo, lt-1, d);   if (v >= 0) sort(a, lt, gt, d+1);   sort(a, gt+1, hi, d);} }
```
##Trie

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

Suffix sort solution.##References:
1. [How Do I Choose Between a Hash Table and a Trie (Prefix Tree)](https://stackoverflow.com/questions/245878/how-do-i-choose-between-a-hash-table-and-a-trie-prefix-tree)