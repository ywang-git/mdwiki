
#Basic Data Structures
| Data Structure | Interfaces | C++ | Related Algorithms & Techniques|
|--|--|--|--|
|Array (Bag)|add(Item item)<br/>isEmpty()<br/>size()|iterator vector::insert(const_iterator position, const value_type& val)<br/>bool vector::empty() const<br/>size_type vector::size() const noexcept
|Linked List| |list|1. runner / cursor
|Stack|push(Item item)<br/>pop()<br/><br/>isEmpty()<br/>size()|void stack::push(value_type& val)<br/>void stack::pop()<br/>refernece& stack::top()<br/>bool stack::empty() const<br/>size_type stack::size() const<br/>|1. recursion
|Queue|void enqueue(Item item)<br/>Item dequeue()<br/>boolean isEmpty()<br/>int size()|void queue::push(value_type& val)<br/>void queue::pop()<br/>refrence& queue::front()<br/>bool queue::empty()<br/>size_type queue::size() const|1. breadth first traverse of tree|
|Hashtable|CHAINED-HASH-INSERT(T, x)<br/>CHAINED-HASH-SEARCH(T, k)<br/>CHAINED-HASH-DELETE(T, x)|iterator unordered_map::find ( const key_type& k );<br/>template <class P> pair< iterator,bool > unordered_map::insert ( P&& val );<br/>size_type erase ( const key_type& k );|1. find duplicate (strings)<br/>2. look up table (for int / string keys)|
|Heap||priority_queue
|Priority Queue|INSERT(S, x): inserts the element x into the set S, which is equivalent to the operation S = S ∪ {x}.<br/>MAXIMUM(S) returns the element of S with the largest key.<br/>EXTRACT-MAX(S) removes and returns the element of S with the largest key.<br/>INCREASE-KEY(S, x, k) increases the value of element x's key to the new value k, which is assumed to be at least as large as x's current key value|void priority_queue::push(const value_type& val)<br/>const value_type& priority_queue::top() const<br/>void priority_queue::pop()<br/>|


##Heap Algorithm

The sorting routine uses two subroutines, heapify and siftDown. The former is the common in-place heap construction routine, while the latter is a common subroutine for implementing heapify.

```
BUILD-MAX-HEAP(A)
     A.heap-size = A.length
     for i = ⎣A.length / 2⎦ downto 1
          MAX-HEAPIFY(A, i)
```

```
MAX-HEAPIFY(A, i)
l = LEFT(i)
r = RIGHT(i)
if l <= A.heap-size and A[l] > A[i]
     largest = l
else largest = i
if r <= A.heap-size and A[r] > A[largest]
     largest = r
if largest != i
     exchange A[i] with A[largest]
     MAX-HEAPIFY(A, largest)
```


```
HEAPSORT(A)
BUILD-MAX-HEAP(A)
for i = a.length downto 2
     exchange A[1] with A[i]
     A.heap-size = A.heap-size -1
     MAX-HEAPIFY(A, 1)
```
```
HEAP-MAXIMUM(A)
return A[1]
```
 𝚯(1)

```
HEAP-EXTRACT-MAX(A)
if A.heap-size < 1
     error "heap underflow"
max = A[1]
A[1] = A[A.heap-size]
A.heap-size = A.heap-size - 1
MAX-HEAPIFY(A, 1)
return max
```
O(log n)

```
HEAP-INCREASE-KEY(A, i, key)
if key < A[i]
     error "new key is smaller than current key"
A[i] = key
while i > 1 and A[PARENT(i)] < A[i]
     exchange A[i] with A[PARENT(i)]
     i = PARENT[i]
```
O(log n)

```
MAX-HEAP-INSERT(A, key)
A.heap-size = A.heap-size + 1
A[A.heap-size] = -∞
HEAP-INCREASE-KEY(A, A.heap-size, key)
```
O(log n)
        
##Reference
1. [Differences between HashMap and Hashtable?](https://stackoverflow.com/questions/40471/differences-between-hashmap-and-hashtable)

