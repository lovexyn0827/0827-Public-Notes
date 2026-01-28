# Introduction To Algorithms

> Take notes per chapter to allow more flexible rearrangements of topics.

## Part I Funderations

### CH 1

(Omitted)

### CH 2: Analyzing  Algorithms

Loop Invariant: A set of desired properties, say $P$.

- Initialization: $P$ holds before the first iteration of the loop.
- Maintenance: If $P$ holds before an iteration, so do it after the iteration.
- Termination: The loop terminates, giving some useful properties.

Divide and conquer:

- Divide: ~
- Conquer: ~ 
- Combine: ~

$$
T(n) = \begin{cases}
\Theta(1) & n < n_0\\
D(n) + aT(n/b)+C(n) & \text{Otherwise}
\end{cases}
$$

Pseudo code convention:

~

Insert sort:

````````
InsertionSort(A, n)
	for i = 2 to n
		key = A[i]
		j = i - 1;
		while j > 0 && A[j] > A[i]
			A[j + 1] = A[j]
			j--
		A[j + 1] = key
````````

Merge sort:

``````
Merge(A, p, q, r)
	nL = q - p + 1
	nR = r - q
	Let L[0:nL - 1], R[0:nR - 1] be new arrays
	Copy A[p:q] into L, A[q + 1:r] into R
	i = 0
	j = 0
	k = p
	while i < nL && j < nR
		if L[i] <= R[j]
			A[k] = L[i]
			i++
		else
			A[k] = R[j]
			j++
		k++
	if i < nL
		Copy L[i:nL - 1] to A[k, r]
	else
		Copy R[j:nR - 1] to A[k, r]

MergeSort(A, p, r)
	if (p >= r)
		return
	q = floor((p + q) / 2)
	MergeSort(A, p, q)
	MergeSort(A, q + 1, q)
	Merge(A, p, q, r)
``````

### CH 3: Characterizing Running Times

Notations:

- $O(g(n)) = \{f(n):\exists c>0\exist n_0>0\text{ s.t. }\forall n \ge n_0,0\le f(n)\le cg(n)\}$
- $\Omega(g(n)) = \{f(n):\exists c>0\exist n_0>0\text{ s.t. }\forall n \ge n_0,0\le cg(n)\le f(n)\}$
- $\Theta(g(n)) = \{f(n):\exists c_1,c_2>0\exist n_0>0\text{ s.t. }\forall n \ge n_0,0\le c_1g(n)\le f(n)\le C_2g(n)\}$
- $o(g(n)) = \{f(n):\forall c>0\exist n_0>0\text{ s.t. }\forall n \ge n_0,0\le f(n)< cg(n)\}$
- $\omega(g(n)) = \{f(n):\forall c>0\exist n_0>0\text{ s.t. }\forall n \ge n_0,0\le cg(n) < f(n)\}$

Properties:

- Transitivity holds for all notations.
- Reflectivity holds for the "big-x" family of notations.
- Symmetry holds only for $\Theta$-notation.
- Transpose Symmetry:
  - $f(n) = O(g(n)) \iff g(n) = \Omega(f(n))$
  - $f(n) = o(g(n)) \iff g(n) = \omega(f(n))$

> Trichotomy doesn't hold for any of these notations!

Ceiling & Floors:
$$
\left\lfloor \frac{\lfloor x/a \rfloor}{b} \right\rfloor = \left\lfloor \frac{x}{ab} \right\rfloor
$$

> Also holds for cellings

Functional iterations:
$$
f^{(i)}(n) = \begin{cases}
n & i = 0\\
f(f^{(i - 1)}(n)) & i > 0
\end{cases}
$$
Iterated Logarithm:
$$
\lg^*n = \min\{i\ge 0:lg^{(i)}n\le 1\}
$$

### CH 4: Divide-and-Conquer

Recurrence: (Recursive equation)

Algorithmic recurrence: for every sufficiently large threshold $n_0$

- $\forall n < n_0, T(n) = \Theta(1)$
- $\forall n\ge n_0, $ the recursions terminates in base cases.

Fast matrix multiplication: Reduce multiplications at the expense of more additions.

> This is why complexities like $\Theta(n^{2.81})$ occurs.

Solving recurrences:

- Substituting method: Guess and then prove with induction

  - Avoid inductive hypothesis including asymptotic notations like $T(n) = O(n)$ 

- Recursion tree method: (Applicable for both preliminary guesses & proof)

- Master method

  - The Master theorem: Let $a > 0$ and $b > 1$ be constants, $f(n)$ be a asymptotically nonnegative driving function. Define recurrence by
    $$
    T(n) = aT(n/b) + f(n)
    $$
    Where $a'T(n/b)$ means $a_1 T(\lfloor n/b \rfloor) + a_2 T(\lceil n/b \rceil)$ and $a = a_1 + a_2$, then

    1. $\exists \epsilon > 0$ s.t. $f(n) = O(n^{\log_b a - \epsilon})$, then $T(n) = \Theta(n^{\log_b a})$
    2. $\exists k\ge 0$ s.t. $f(n) = \Theta(n^{\log_b a}\lg^k n)$, then $T(n) = \Theta(n^{\log_b a} \lg^{k + 1}n)$
    3. $\exists \epsilon > 0$ s.t. $f(n) = \Omega(n^{\log_b a + \epsilon})$, and $\exist c\exists N\forall n>N, af(n/b) \le c f(n)$, then $T(n) = \Theta(f(n))$

  - By some means, we may interpret it as "$T(n) = \max\{n^{\log_b a},f(n)\}$"

- Akra-Bazzi method: For recurrence with $a_i, b_i\in\R$ and in form of
  $$
  T(n) = f(n) + \sum_{i = 1} ^ {k} a_i T(n / b_i)
  $$
  Find unique $p\in\R$ s.t. 
  $$
  \sum_{i = 1}^k \frac{a_i}{b_i^p} = 1
  $$
  Then
  $$
  T(n) = \Theta\left(n^p \left(1 + \int_1^n \frac{f(x)}{x^{p + 1}}\mathrm dx\right)\right)
  $$
  Celling & floors can only be ignored if $f(n)$ satisfies the polynomial-growth condition: 
  $$
  \exists \hat{n} > 0\forall \phi \ge 1\exist d > 0\text{ s.t. } \frac{f(n)}{d}\le f(\psi n)\le df(n), \forall 1\le\psi \le \phi\forall n\ge \hat{n}
  $$
  That is, roughly, for sufficiently large $n$'s, the changing ratio of $f$ could be bounded as long as the changing ratio of $n$ is bounded.

## CH 5: Probabilistic Analysis and Randomized Algorithms

Prob. Analysis vs. Randomized Algorithms:

- Probabilistic Analysis: Deciding on the distribution of inputs and analyze - Average case
- Randomized Algorithms: Impose a distribution to inputs with a RNG - Expected

Randomly permute an array:

````python
Randomly-Permute(A, n)
    for i = 1 to n
    	swap a[i] with A[Random(i, n)]
````

Generate a random sample:

`````python
S = EmptySet
for k = n - m + 1 to n
	i = Random(k)
    if i in S
    	Adjoint k to S
    else
    	Adjoint i to S
return S
`````

Classical Problems:

- The Hiring Problem: Interview one by one, and replace the current if a better one is encountered
  - The expected number of replacement is $\ln n + O(1)$
- The hat-checker problem: redistribute h bnnats of $n$ customers, the expected count of hats held by their previous owner.
- The birthday paradox: People required s.t. probability of having an matching pair is $\Theta(\sqrt{n})$
- Balls & bins: Tossing identical balls to $b$ bins
  - Number of balls fall in a given bin: follows $b(n, 1/b)$
  - $b$ tosses at average before an given bin contains a ball 
  - The coupon collector's problem: $(b\ln b + O(1))$  balls to toss before each bin has at least one ball
- Streaks: Flip a coin and encounter $n$ consecutive heads (or tails)
  - Omitted~
- The on-line hiring problem: Exactly one hiring, and accept or decline immediately after interviewing
  - Find the best of first $k$ of $n$ candidates, and then hire the first candidate better than it in following interviews.
    - $k = n/e$ to obtain the optimal probability of hiring the best, $1/e$

## Part II: Sorting and Order Statistics

### CH 6: Heapsort

(binary) heap: an array viewed as a nearly complete binary tree

Maximum & minimum heap:

- Max.: `A[Parent(i)] >= A[i]` - Root is the maximum
- Min.: `A[Parent(i)] <= A[i]` - Root is the minimum

> Relation between left & right children are not specified?

Heap operations:

- `MaxHeapify`: "Fix" the heap with a parent node violating the heap property, in $O(\lg n)$ time.
  - Exchange the violating parent with the largest child, and recurse.
- `BuildMaxHeap`: Build an max heap from arbitrary array, in $O(n)$ time.
  - `MaxHeapify(A, i)` for each `i = floor(n / 2) downto 1`.
- `Heapsort`: In-place sort an array in $O(n\lg n)$ time.
  - `BuildMaxHeap`, and for `i = n downto 2`:
    - Place the max. (`A[1]`) to the tail, and `MaxHeapify(A, 1)`
- `MaxHeapInsert`, `MaxHeapExtractMax`, and `HeapIncreaseKey`: $O(\lg n)$

```````
MaxHeapify(A, i)
	l = Left(i)
	r = Right(i)
	if l <= A.heapSize && A[l] > A[i]
		largest = l
	else 
		largest = i
	if r <= A.heapSize && A[r] > A[largest]
		largest = r
	if largest != i
		swap(A[i], A[largest])
		MaxHeapify(A, largest)
		
BuildMaxHeap(A, n)
	A.heapSize = n
	for i = floor(n / 2) downto 1
		MaxHeapify(A, i)

Heapsort(A, n)
	BuildMaxHeap(A, n)
	for i = n downto 2
		swap(A[1], A[i])
		A.heapSize--
		MaxHeapify(A, 1)
```````

Priority queue implementations: key for priority, and an set indexed by the key

- `Maximum` is trivially `A[1]`
- `ExtractMax` is like what is done in each loop of `Heapsort`
- `IncreaseKey` back-propagates the change to the root, possibly with swapping
- `Insert` places the key in the tail and invokes `IncreaseKey`

```````
Maximum(A)
	if A.heapSize == 0
		error "Underflow"
	return A[1]
	
ExtractMax(A)
	max = Maximum(A)
	A[1] = A[A.heapSize]
	A.heapSize--
	MaxHeapify(A, 1)
	return max

IncreaseKey(A, x, k)
	if k < A[i]
		error "k is smaller that current key!"
	x.key = k
	Find the index i of x in A
	while i > 1 && A[Parent(x)].key < A[x].key
		swap(A[x], A[Parent(x)]), updating satellite data
		x = Parent(x)

Insert(A, x, n)
	if (A.heapSize == n)]
		error "Overflow"
	A.heapSize++
	k = x.key
	x.key = -Infinity
	A[A.heapSize] = x
	map x to index A.heapSize in the array
	IncreaseKey(A, x, k)
```````

### CH 7: Quicksort

Implementation of quicksort:

````python
Quicksort(A, p, r)
	if p < r
    	q = Partition(A, p, r)
        Quicksort(A, p, q - 1)
        Quicksort(A, q + 1, r)
        
Partition(A, p, r)
	x = A[r]
    i = p - 1
    for j = p to r - 1
    	if A[j] <= x
        	i = i + 1
            swap(A[i], A[j])
	swap(A[i + 1], A[r])
    return i + 1
````

That is:

- Partition `A` into two sub-arrays at left & right of `q`, with left elements `<= A[q]` and inverse applies to the right part.
- Continue partitioning the sub-arrays, excluding the pivot `A[q]`.

Performance analysis:

- `Parition()` takes $\Theta(n)$ time.
- Worst case happens when all remaining elem. goes into one partition, with $\Theta(n^2)$ of running time.
- Best case happens when all partitions are completely balanced, with $\Theta(n\lg n)$ of running time.
- Given a fixed ratio of the size of two partitions, running time remains being $O(n\lg n)$, only affecting the constant.
- Average case running time is $O(n\lg n)$

Randomize the algorithm: Pick a random elem. as the pivot, instead of `A[r]` at all time.

Proof of expected running time of randomized `Quicksort()`: $O(n\lg n)$

- Running time of `Quicksort` is $O(n+\text{comparisions})$
- Given $z_1<\cdots < z_n$, $z_i, z_j$ is compared iff one of them is the first pivot in $\{z_i, \cdots, z_j\}$
- $\operatorname{Pr}[z_i, z_j \text{ gets compared}] = \frac{2}{j - i +1}$ 
- ~

Hoare's original implementation of `Partition()`:

`````python
HoarePartition(A, p, r)
	x = A[p]
    i = p - 1
    j = r + 1
    while True
    	repeat j-- until A[j] <= x
        repeat i++ until A[i] >= x
        if (i < j) swap(A[i], A[j])
        else return j
`````

Tail-recursion elimination: ~

### CH 8: Sorting in Linear Time

Theorem 8.1: Any comparison based algorithms requires $\Omega(n\lg n)$ comparisons in worst case.

Stretch of Proof: To draw the decision tree (a complete binary tree whose nodes have either both children or none), where all possible permutations is assigned a leaf and edges denote comparisons, then the number of leaves $l$depth $h$ satisfies:
$$
n!\le l \le 2^h
$$
Which implies
$$
h\ge \lg(n!) = \Omega(n\lg n)
$$
This means that heapsort & merge sort are asymptotically optimal.

Counting sort: 

- Assuming that possible values of array elements are within a small range, say $[1, k]\cap \Z$.
- Require the input array, an array for counts an an array for outputs.
- Has a running time of $\Theta(n + k)$.
- Stable, as long as the last pass is downwards.
- Multiple passes:
  - Initialize counters `C[0:k]` to 0;
  - Count how many times each number presents;
  - Convert the counts to number of elements less than or equals to each number;
  - Place elements to the output array.

Implementation:

``````pythom
CountingSort(A, n, k)
	let B[1:n] and C[0:k] be new arrays.
	Zero C[0:k]
	for j = 1 to n
		C[A[j]]++
	for i = i to k
		C[i] = C[i] + C[i - 1]
	for j = n downto 1
		B[C[A[j]]] = A[j]
		C[A[j]]--
``````

Radix sort:

- Sort on $d$ digits, each of which has $k$ possible values.
- Conterintutitively, it sorts on least significant digits first.
  - Thus relying on an stable sorting algorithm, typically counting sort.
- Takes $\Theta(d(n+k))$ time when using counting sort as the stable sort algorithm.

Implementation:

```````
RadixSort(A, n, d)
	for i = i to d
		Sort A on digit i with a stable sort.
```````

Lemma 8.4 (Sorting binary numbers): Given $n$ $b-$bit numbers and any positive integer $r\le b$, `RadixSort` sorts them in $\Theta((b/r)(n + 2^r))$ time if the stable sort takes $\Theta(n + k)$ time.

Picking optimal $r$:

- If $b < \lfloor\lg n\rfloor$, pick $r = b$ to yield a running time of $\Theta(n)$;
- If $b \ge \lfloor\lg n\rfloor$, pick $r = \lfloor\lg n\rfloor$ to yield a running time of $\Theta(bn/\lg n)$;

Bucket sort:

- Assumes that inputs are iid. and uniformly distributed within $[0, 1)$.
- Divides $[0,1)$ to $n$ equal-sized subintervals, called buckets, and assign each a linked list.
- Inserts inputs to buckets, and then sort each bucket.
- Concatenate all buckets, to produce an output.
- Runs in $\Theta(n)$ time at average case.
- One could transform keys to sort a wider range of inputs.

Implementation:

`````
BucketSort(A, n)
	Let B[0:n - 1] be a new array
	Create an empty list for each B[i]
	for i = 1 to n
		Insert A[i] to list B[floor(n * A[i])]
	for i = 0 to n - 1
		Sort B[i] with insertion sort
	Concatenate B[0], ..., B[n - 1] together in order
	return the concatenated lists.
`````

### CH 9: Medians and Order Statistics

The $i$th order statistic: the $i$th smallest element.

The selection problem: given set $A$ of $n$ numbers and integer i with $1\le i\le n$, select $x\in A$ that is larger than exactly $(i - 1)$ elements.

Selecting a minimum / maximum requires at least $(n - 1)$ comparisons, but selecting both of them simultaneously requires only $3\lfloor n / 2\rfloor$ comparisons (by comparing consecutive pairs first), fewer than the trivial solution with $(2n - 2)$ comparisons.

Select in expected linear time:

- Partition the input array around a pivot
- It is simple to tell how many numbers are smaller than the pivot.
- Continue searching the left or right part recursively, or pick the pivot if applicable.
- Runs in $\Theta(n)$ expected time, but $\Theta(n^2)$ in the worst case.
  - Like what happens to `Quicksort`.
  - The proof is DEADLY LONG!!!

Implementation:

```````
RandomizedSelect(A, p, r, i)
	if p == r
		return A[p]
	q = RandomizedPartition(A, p, r)
	k = q - p + 1
	if (k == i)
		return A[q]
	elseif i < k
		return RandomizedSelect(A, p, q - 1, i)
	else
		return RandomizedSelect(A, q + 1, r, i - k)
```````

Selecting in the worst-case linear time:

- Pick a provably "helpful" pivot.

Implementation:

``````
Select(A, p, r, i)
	while (r - p + 1) % 5 != 0
		for j = p + 1 to r
			if A[p] > A[j]
				swap(A[p], A[j])
		if i == 1
			return A[p]
		p++;
		i--;
	g = (r - p + 1) / 5
	Sort 5 equivalent classes module g
	x = Select(A, p + 2g, p + 3g - 1, ceil(g / 2))
	q = PartitionAround(A, p, r, x)
	k = q - p + 1
	if i == k       return A[q]
	elseif i < k   	return Select(A, p, q - 1, i)
	else            return Select(A, q + 1, r, i - k)
``````

Also works when groups are consist if 3 or 7 elements.

##  Part III: Data Structures

### Elementary Data Structures

Arrays: 

- Presumed to be stored in continuous memory regions. For $s-$origin array at address $a$ with records of size $b$, the $i$ th record occupies bytes:

    $$
    [a + b(i - s), a + b(i - s + 1) - 1]
    $$

    In particular, for 0-origin and 1-origin arrays, followings applies respectively:
    $$
    [a + b(i - 1), a + bi - 1]\\
    [a + bi, a + b(i + 1) - 1]
    $$

Matrices: May be stored in following schemes, 

- row-major order, where each row occupy a continuous region of memory.

  - If the index of columns and rows and index of the array starts at $s$, the index of $M[i,j]$ is
    $$
    \operatorname{IndexOf}(i, j) = 
    \begin{cases}
    s + n(i - s) + (j - s) = n(i - s) + j & \text{row-major}\\
    s + m(j - s) + (i - s) = m(j - s) + i & \text{column-major}
    \end{cases}
    $$

- column-major, where the converse applies.

- multiple-array, row-major: one array for each row, and one pointing to these arrays.

  - `A[i][j]` stores $M[i,j]$.
  - Convenient to store "ragged-arrays".

- multiple-array, column-major: ~

- block representation: each block is stored contiguously,

Stacks:

- LIFO
- `Push(S, x)`, `Pop(S)`, `StackEmpty(S)`
- Implementations omitted

Queues:

- FIFO

- `Enqueue(Q, x)` at the tail, `Dequeue(Q)` from the head.

- `Q.head == Q.tail` if empty

- `Q.head == Q.tail + 1 || Q.head = 1 && Q.tail == Q.size` if full.

- Implementation of (circular) queues (Without error detecting branches):

  ```````
  Enqueue(Q, x)
  	Q[Q.tail] = x
  	if Q.tail == Q.size
  		Q.tail = 1
  	else
  		Q.tail++
  		
  Dequeue(Q)
  	x = Q[Q.head]
  	if Q.head == Q.size
  		Q.head = 1
  	else
  		Q.head++
  	return x
  ```````

Linked lists: Sometimes also called "search lists"

- Singly & doubly linked lists: 
   - Nodes in doubly linked lists refers to both predecessor and successor.
   - Nodes in singly linked lists has only `next` ptr. but no `prev`.
   
- Sorted & Unsorted list

- Circular list

- Searching a linked list is straightforward.

   - May use Sentinels to save one comparison for nullity.
   - For sorted compact lists, make random guesses to skip nodes and run in average $O(\sqrt{n})$ time.

- Manipulation: Note that `L` keeps track of only `head` but not `tail`

   ```````
   ListPrepend(L, x)
   	x.next = L.head
   	x.prev = NIL
   	if L.head != NIL
   		L.head.prev = x
   	L.head = x
   
   // ... --> y --> x --> ...
   ListInsert(x, y)
   	x.next = y.next
   	x.prev = y
   	if y.next != NIL
   		y.next.prev = x
   	y.next = x
   	
   ListDelete(L, x)
   	if x.prev != NIL
   		x.prev.next = x.next
   	else
   		L.head = x.next
   	if x.next != NIL
   		x.next.prev = x.prev
   ```````

- Sentinels: A dummy object turning the list into a circular doubly linked list

   - `L.nil.prev` points to the tail, and `L.nil.next` points to the head

   - Thus the following works:

      ``````
      ListDelete'(L, x)
      	x.prev.next = x.next
      	x.next.prev = x.prev
      
      ListInsert'(x, y)
      	x.next = y.next
      	x.prev = y
      	y.next.prev =x
      	y.next = x
      	
      ListSearch'(L, k)
      	L.nil.key = k
      	x = L.nil.next
      	while x.key != k
      		x = x.next
      	if x = L.nil
      		return NIL
      	else
      		return x
      ``````

Trees:

- Binary trees: 3 pointers per node, `p`, `left` and `right`
- Rooted tree with unbounded branching: Left-child, right-sibling representation:
  - Each node, `x`, has 2 pointers:
    - `x.leftChild` pointing to the leftmost child of `x`
    - `x.rightSibling` pointing to the sibling of `x` immediately to its right
- Other representations, including heaps, etc.
- Traverse algorithms: Left as exercises~

### CH 11: Hash tables

Dictionary: Supports `Insert`, `Search` and `Delete`

Direct-address tables: When the universe of keys is reasonably small, say $U = \{0, 1, \dots, m - 1\}$, index directly with key

- Guarantee running time of $O(1)$ in the worst case;

Hash tables:

- Uses a hash function $h: U\to \{0, 1, \dots, m - 1\}$
- $k$ hashes to slot $h(k)$, and the hash value of $k$ is $h(k)$
  - Storing record with key $k$ in slot $h(k)$
- Two keys may hash into the same slot, causing a collision.

Hash functions:

- Independent form hash function:
    -  Chosen an slot uniformly from $\{0, \dots, m - 1\}$
    - Choice is independent of other inputs.
    - Such a hash function is also called a random oracle.
    - Load factor $\alpha = \frac nm = \frac{\text{elements}}{\text{slots}}$.
    - Memory overhead could be $\Theta(n)$ to maintain $O(1)$ expected time.
    - `Search` takes $O(n)$ time in worst case.
    
- Static hashing: A single hash function for all data.

    - The division method: Simply $h(k) = k\mod m$
        - May work well when $m$ is a prime not too close to an exact power of 2.
        - No guarantee that it provides good average-case performance.

    - The multiplication method: Given $0<A<1$, $h(k) = \lfloor m\operatorname{frac}(Ak)\rfloor$.
        - $m$ is not critical

    - The multiply-shift method: $h_a(k) = (ka\mod 2^w) \ggg (w - \mathscr l)$
        - Where $\mathscr l$ is desired length of hash value, $w$ is the length of machine word, $0 < a < 2^w$.
        - Can be implemented in only 3 instructions.
        - Fast, but no guarantee on good average-case performance.

- Random hashing: Choose a hash function in a manner independent of the key so that no particular input can elicit the worse-case performance. (Recommended!)

    - Define a family of hash functions $\mathscr H\subset \{f: U\to \Z_m\}$, with following achievable properties ($h\in \mathscr H$ is picked ramdomly):
        - Uniform: $\forall k\in U\forall q\in \Z_m,P(h(k) = q) = 1/m$
        - Universal: $\forall\text{distinct }k_1, k_2\in U, P(h(k_1)=  h(k_2))\le 1/m$
        - $\epsilon-$universal: $\forall\text{distinct }k_1, k_2\in U, P(h(k_1)=  h(k_2))\le \epsilon$
            - Exercise 11.3-5: $h:U\to Q$ has $\epsilon\ge \frac1{|Q|} -\frac1{|U|}$.

        - $d-$independent: $\forall\{k_1, \dots, k_d\}\subset U\forall q_1, \dots, d_d\in \Z_m, P(h(k_i) = q_i, \forall 1\le i\le d) = 1/m^d$

    - A number theory based universal family: Given $p$ large enough to hold all keys in $\Z_p$ (thus $p > m$)
        - $\{h_{ab} = ((ak + b)\mod p)\mod m: a\in \Z_m^*, b\in \Z_m\}$
        - Proof: Show that given $h_{ab}$, $k_1\ne k_2\implies r_1\ne r_2$, and that each valid pair $(a, b)$ yields a different pair $(r_1, r_2)$. Then, $P(k_1, k_2 \text{ collides}) = P(r_1\equiv r_2\mod m)\le \frac{(p - 1)/m}{p - 1}$.

    - A $2/m-$universal family based on the multiple-shift method: 
        - $\{h_a = (ka\mod 2^w)\ggg (w-  l): a \text{ is odd} \land 1\le a<m\}$
        - Compromises the upper bound of probability of collision but is calculated faster.

- Hashing long inputs (vectors, strings): Hash functions varies from input to input

    - Number theoretic methods: Extending previous results

        - Exercise 11.3-6 gives an example: $U = \Z_p^d$, $Q = \Z_p$, $p$ is prime, define $h_b:U\to Q$
            $$
            h_b(<a_0, \dots, a_{d - 1}>) = \left(\sum_{i = 0}^{d - 1} a_i d^i\right) \mod p
            $$
            Then $\mathscr H = \{h_b:b\in \Z_p\}$ is $\frac{d - 1}{p}-$universal.

    - Cryptographic hashing: Hash with SHA-256, etc.

        - $h(k) = \mathtt{Sha256}(k) \mod m$
        - or adding salt: $$h(k) = \mathtt{Sha256}(\mathtt{Concat}(k, \text{salt})) \mod m$$


Collision must be resolved: 

- By chaining: assign a linked list to each slot
  - Each slot points to a linked list or has value `NIL`.
  - `Insert` runs in $O(1)$ time assuming keys are distinct (no search is required)
  - `Delete` runs in $O(1)$ time when using doubly linked list and the node to delete is given.
  - `Search` runs in $O(1)$ (or rather, $O(1 + \alpha)$) time on average:
    - Proof for unsuccessful search:  Each list has expected length $\alpha$.
    - Proof for successful search: Turn out to be, lengthy though, trivial.
- By open addressing: Generate a sequence of hash, and successively probe, to find an empty slot.
  - If the number of slots is fixed, the hash table may be filled up, $\alpha\le 1$
  - Deletion is tricky: May use placeholder `DELETED` instead of `NIL`.
  - Probe sequence must be a permutation of $\Z_m$
    - Independent uniform permutation hashing: The sequence is equally likely to be any permutation possible.

  - Generating probe sequences:
    - Double hashing: $h(k, i) = (h_1(k) + ih_2(k)) \mod m$
      - Where $h_1, h_2$ are auxiliary hash functions.
      - $h_2(k)$ must be relatively prime to $m$ so that all slots can be probed, make its choice tricky.
      - Can generate $\Theta(n^2)$ distinct sequences if $m\in \mathbb P$ or $m = 2^n$

    - Linear probing: $h(k, i) = (h_1(k) + i)\mod m$
      - Double hashing with $h_2(k) = 1$
      - Generates only $m$ distinct probe sequences.

  - Performance (Assuming independent uniform permutation hashing and ignoring deletion)
    - The expected number of probes in an unsuccessful search is at most $1/(1-\alpha)$
      - Intuition: $1 + \alpha +\alpha^2+\cdots = 1/(1-\alpha)$
      - Corollary: So do insertion

    - The expected number of probes in an successful search is at most $\frac 1\alpha \ln\frac{1}{1-\alpha}$
      - Proof: Suppose $k$ is the $(i+1)$st key inserted, then searching for $k$ requires at most $\frac1{1-i/m}$ probes.


Practical considerations (Memory hierarchies):

- Linear probing demonstrates excellent performance & is more practical:

  - Probing usually runs in the same block of memory.

    - Primary clustering, or that long runs of occupied slots build up, increases search time in traditional RAM model, but is beneficial in hierarchical memory model.

  - Deletion is more convenient: Inverse $h$ with respect to $i$, as $g(k, q) = (q - h_1(k))\mod m$

    ``````
    LinearProbingHashDelete(T, q)
    	while True
    		T[q] = NIL
    		q' = q
    		repeat
    			q' = (q' + 1) % m
    			k' = T[q']
    			if k' == NIL
    				return
    		until g(k', q) < g(k', q')
    		T[q] = k'
    		q = q'
    ``````

    > You have reminded me of the winter in 2022, when i was sitting behind the one, both my best friend and who i have secretly liked, also in such a light gray clothing, in inches.

  - If $h_1$ is 5-independent, and $\alpha<2/3$, then search, insertion and deletion takes $O(1/(1-\alpha)^2)$ (constant) expected running time.

- Hash functions taking advantages of fast registers:

  - The wee hash function:
    $$
    \mathtt{swap}(x) = (x\ggg (w / 2)) + (x\lll (w / 2))
    $$

    $$
    f_a(k) = \mathtt{swap}((2k^2 + ak)\mod 2^w)
    $$

    $$
    h_{a,b,t,r} = \left(f^{(r)}_{a + 2t}(k + b)\right)\mod m
    $$

    Where $a$ is odd and $t$ is the length of $k$ in bits.

    For long inputs:

    `````
    Wee(k, a, b, t, r, m)
    	u = ceil(t / w)
    	<k_1, ..., k_u> = chop(k)
    	q = b
    	for i = 1 to u
    		q = f^{(r)}_{a + 2t}(k_i + q)
    	return q % m
    `````

### CH 12: Binary Search Trees

Binary-search-tree property:

- Keys in the left subtree of $x$ is no larger than the key of $x$
- Keys in the right subtree of $x$ is no smaller than the key of $x$

Keys can be printed in sorted order with inorder tree walk, which takes $\Theta(n)$ time:

``````
InorderTreeWalk(x)
	if x != NIL
		InorderTreeWalk(x.left)
		print(x.key)
		InorderTreeWalk(x.right)
``````

Search runs in $O(h)$, where $h$ is the height of the binary search tree (Unroll is possible since only one recursive invocation actually occurs):

``````
TreeSearch(x, k)
	if x == NIL or k == x.key
		return x
	if k < x.key
		return TreeSearch(x.left, k)
	else
		return TreeSearch(x.right, k)
		
IterativeTreeSearch(x, k)
	while x != NIL and k != x.key
		if k < x.key
			x = x.left
		else
			x = x.right
	return x
``````

Minimum & maximum is straightforward: $O(h)$

````````
TreeMinimum(x)
	while x.left != NIL
		x = x.left
	return x
	
TreeMaximum(x)
	while x.right != NIL
		x = x.right
	return x
````````

Successor & Predecessor: Also $O(h)$

```````
TreeSuccessor(x)
	if x.right != NIL
		return TreeMinimum(x.right)
	else
		y != x.p
		while y != NIL and x.p.right == x
			x = y
			y = y.p
		return y

TreePredecessor(x)
	if x.left != NIL
		return TreeMaximum(x.left)
	else
		y != x.p
		while y != NIL and x.p.left == x
			x = y
			y = y.p
		return y
```````

> Successors & predecessors are defined upon the inorder traverse sequence.
>
> Successor of $x$ either lays in the leftmost element of $x$'s right subtree, or is its nearest ancestor with a left subtree containing $x$. Converse applies for predecessors.

Insertion is basically straightforward: Search for a `NIL` to replace and use a trailing pointer `y`.

```````
TreeInsert(T, z)
	x = T.root
	y = NIL
	while x != NIL
		y = x
		if z.key < x.key
			x = x.left
		else
			x = x.right
	z.p = y
	if y == NIL
		T.root = z
	else if x.key < y.key	// x == y.left may not work since x is NIL
		y.left = z
	else
		y.right = z
```````

Deletion gets a little bit more complicated:

- When the element $z$ to delete has:
    - No child: Simply remove it
    - One child: Its sole child takes its place
    - Both children: Find the successor $y$ of $z$, who has no left child.
      - If $y$ is the right child of $z$: $y$ takes the place of $z$ and inherit the left child of $z$
      - Otherwise: $y$'s sole right child takes its place, and then $y$ takes $z$'s place.
- Implemented as follows:
    ````````
    Transplant(T, u, v)
        if u == T.root
            T.root = v
        elseif u == u.p.left
            u.p.left = v
        else
            u.p.right = v
        if v != NIL
            v.p = u.p
    
    TreeDelete(T, z)
        if z.left == NIL
            Transplant(T, z, z.right)
        elseif z.right == NIL
            Transplant(T, z, z.left)
        else
            y = TreeMinimum(z.right)
            if y != z.right
                Transplant(T, y, y.right)
                y.right = z.right
                y.right.p = y
            Transplant(T, z, y)
            y.left = z.left
            y.left.p = y
    ````````
    Note that some "custom" branches are not handled in `Transplant()`, and thus should be established manually.
    
    Using the predecessor also works, with necessary changes made.
- Also, deletion takes $O(h)$ time, mostly due to the `TreeMinimum()` operation.

Radix tree (Problem 12-2): (a.k.a. trie) Stores bit strings.

### CH 13: Red-Black Trees

> This should be the hardest chapter by now.

Red-black trees:

- Maintains an extra field `color`.
- No path is more than twice as long as any other (approximately balanced).
- Tree with $n$ internal nodes has height at most $2\lg(n + 1)$
  - Proved inductively.
- Satisfies following red-black properties:
  - Every node is either red or black
  - The root is black
  - Every leaf (`NIL` instead of leaves with payloads) is black
  - Both children of a red node is black
    - Implies that no adjacent red nodes are allowed
  - For each node, all simple path from the node to `NIL` contains the same number of black nodes.
    - Induces the definition of "black-height", $\mathtt{bh}(x)$.
- All operations takes $O(\lg n)$ time.

Rotation:

- Left rotation & right rotation

- "Twists" the branch between $x$ and $y$, and move the unnamed subtree at middle.

- Implemented as follows:

  ````````
  LeftRotate(T, x)
  	y = x.right
  	x.right = y.left
  	if x.right != T.nil
  		y.left.p = x
  	y.p = x.p
  	if x.p == T.nil
  		T.root = y
  	elseif x == x.p.left
  		x.p.left = y
  	else
  		x.p.right = y
  	y.left = x
  	x.p = y
  
  RightRotate(T, y)
  	x = y.left
  	y.left = x.right
  	if x.right != T.nil
  		x.right.p = y
  	x.p = y.p
  	if y.p == T.nil
  		T.root = x
  	elseif y.p.left == y
  		y.p.left = x
  	else
  		y.p.right = x
  	x.right = y
  	y.p = x
  ````````

  > That is, move unnamed node first, update parents, and then link $x$ and $y$.

- Noteworthy, rotation changes the depth of nodes in subtrees.

- Interestingly, (Problem 13.2-4) any $n-$node binary search tree can be rotated into another with $O(n)$ rotations.

Insertion: Where things begin to get complex

- Compared with `TreeInsert()`, `RBInsert()` use sentinels instead of `NIL`, $z$ is colored red, and further fix-up is carried out at the end.

- Proper 2 (root is black) or 4 (red nodes has both children black) may be violated initially.

- Fix-up handles following three cases, depending on the color of the "uncle" of the inserted node.

  - Uncle is red: Transfer the blackness of grandparent to parent and uncle, color grandparents red, and let $z = z.p.p$
    - Get rid of adjacent red nodes, while leaving black-height of ancestors unaffected
    - Usually, transformations follows a "black-up, unknown-up" fashion, leaving this case an exception.
  - Uncle is black, and $z$ is a right child: Left rotate on the parent, and let $z$ be the previous parent of $z$, falling in the next case
    - Turn the "twisted" chain into a straight train, which initializes case 3.
  - Uncle is black, and $z$ is a left child: Color grandparent red and parent black, then right rotate on the grandparent, and terminate.
    - Turn the chain of $z, z.p, z.p.p$ into a 2-level subtree, with the root black and immediate children of root red.

- Implementation:

  `````````
  RBInsert(T, z)
  	x = T.root
  	y = T.nil
  	while x != T.nil
  		y = x
  		if z.key < x.key
  			x = x.left
  		else
  			x = x.right
  	z.p = y
  	if y == T.nil
  		T.root = z
  	elseif z.key < y.key
  		y.left = z
  	else
  		y.right = z
  	z.left = T.nil
  	z.right = T.nil
  	z.color = RED
  	RBInsertFixup(T, z)
  
  RBInsertFixup(T, z)
  	while z.p.color == RED
  		if z.p == z.p.p.left
  			y = z.p.p.right
  			if y.color == RED
  				z.p.color = BLACK
  				y.color = BLACK
  				z.p.p.color = RED
  				z = z.p.p
  			else
  				if z == z.p.right
  					z = z.p
  					LeftRotate(T, z)
  				z.p.color = BLACK
  				z.p.p.color = RED
  				RightRotate(T, z.p.p)
  		else
  			y = z.p.p.left
  			if y.color == RED
  				z.p.color = BLACK
  				y.color = BLACK
  				z.p.p.color = RED
  				z = z.p.p
  			else
  				if z = z.p.left
  					z = z.p
  					RightRotate(T, z)
  				z.p.color = BLACK
  				z.p.p.color = RED
  				LeftRotate(T, z.p.p)
  	T.root.color = BLACK
  `````````

Deletion: Even more tricky

- Determine $x$ and $y$:

  - $y = z$ if $z$ has only one children, or $z$'s successor otherwise
  - $x$ is $y$'s sole child, which takes $y$'s place in deletion of $z$.

- When $z$ has both children, $y$ inherits $z$'s color.

- Record the original color of $y$. If the color is black, further fix-ups may be needed.

- Properties may be violated after simple deletion:

  - 2, when $y$ is the root and a red child of $y$ takes its place.
  - 4, when both $x$ and its new parent is red.
  - 5, moving black $y$ may affect black-heights.
    - Give an extra (ghost) black to $x$,  in compensation of the removed black $y$.
    - Purely imaginary, Indicated by the fact of being pointed by $x$, not an physical field.

- Transformations preserves the number of black nodes (including the ghost one) from the root of the subtree shown (inclusive), to each of collapsed subtrees. 

- Runs in four cases, depending on the sibling $w$ of $x$:

  - $w$ is red: Left rotate on the parent, exchange the color of $w$ and previous parent, and update $w$ to $x$'s new sibling .
    - Then fall in following 4 cases.
  - $w$ and both children of $w$ are black: Transfer blackness of the level of $x$ (i.e. both $x$ and $w$) to the parent, leaving $x$ only one black and $w$ red - but the parent has one more black by letting $x = x.p$
  - $w$ is black, with left child red and right child black: Switch colors between $w$ and left children and right rotate on $w$
    - Falls in case 4.
  - $w$ is black with a red right child: Exchange colors between $w$ and the parent, color the red right child black, left rotate on the parent, and set $x$ to the root to terminate the loop.
    - Moves one black from the subtree rooted on $w$ to the subtree rooted on $x$, and add a black to the former.

- Implementation:

  `````````
  RBTransplant(T, u, v)
  	if u.p == T.nil
  		T.root = v
  	elseif u = u.p.left
  		u.p.left = v
  	else
  		u.p.right = v
  	v.p = u.p
  
  RBDelete(T, z)
  	y = z
  	yOriginalColor = y.color
  	if z.left == T.nil
  		x = z.right
  		RBTransplant(T, z, z.right)
  	elseif z.right == T.nil
  		x = z.left
  		RBTransplant(T, z, z.left)
  	else
  		y = TreeMinimum(z.right)
  		yOriginalColor = y.color
  		x = y.right
  		if y != z.right
  			RBTransplant(T, y, y.right)
  			y.right = z.right
  			z.right.p = y
  		else
  			x.p = y						// In case x is T.nil
  		RBTransplant(T, z, y)
  		y.left = z.left
  		z.left.p = y
  		y.color = z.color
  	if yOriginalColor = BLACK
  		RBDeleteFixup(T, x)
  
  RBDeleteFixup(T, x)
  	while x != T.root and x.color != BLACK
  		if x == x.p.left
  			w = x.p.right
  			if w.color == RED
  				w.color = BLACK
  				x.p.color = RED
  				LeftRotate(T, x.p)
  				w = x.p.right
  			if w.left.color == BLACK and w.right.color == BLACK
  				w.color = RED
  				x = x.p
  			else
  				if w.right.color == BLACK
  					w.left.color = BLACK
  					w.color = RED
  					RightRotate(T, w)
  					w = x.p.right
  				w.color = x.p.color
  				w.p.color = BLACK
  				w.right.color = BLACK
  				LeftRotate(T, x.p)
  				x = T.root
  		else
  			w = x.p.left
  			if w.color = RED
  				w.color = BLACK
  				x.p.color = RED
  				RightRotate(T, x.p)
  				w = x.p.left
  			if w.left.color == BLACK and w.right.color == BLACK
  				w.color = RED
  				x = x.p
  			else
  				if w.left.color == BLACK
  					w.right.color = BLACK
  					w.color = RED
  					LeftRotate(T, w)
  					w = x.p.left
  				w.color = x.p.color
  				w.p.color = BLACK
  				w.left.color = BLACK
  				RightRotate(T, x.p)
  				x = T.root
  	x.color = BLACK
  `````````

(Problem 13-1) Persistent dynamic set: Record versions. Impl.: Assign each version a root and necessary nodes.

(Problem 13-3) AVL Trees: Height balanced tree (Taught in the winter of 2024)

- Height of left & right subtrees differs by at most 1.
- Easy to prove that an AVL tree of height $h$ has at lease $F_h$ nodes, and therefore $h=O(\lg n)$.
- Takes $O(n)$ time to insert.

## Part IV: Advanced Design and Analysis Techniques

### CH 14: Dynamic Programming

Dynamic programming: programming refers to a tabular method, not writing code.

- Typically applies to optimization problems
- Two elements:
  - Optimal structure: Optimal solutions contains optimal solutions of smaller (independent) subproblems. 
  - Overlapping subproblems: The space of subproblems is "small" (somewhat bounded), and with overlapping.
- Involve four steps:
  - Characterize the optimal structure of an optimal solution
  - Recursively define the value of an optimal solution
  - Compute the value of an optimal solution, typically bottom-up
  - Construct an optimal solution from the calculated information 
- And two basic organizations of algorithm:
  - Memoization: Top-down recursion, but with lazy-evaluation.
  - Bottom-up: Handle smallest subproblems first, concerning interdependency of subproblems.
