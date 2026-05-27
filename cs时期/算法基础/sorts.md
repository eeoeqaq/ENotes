## selection sort
find the smallest, exchange with first.
## heap sort
like a varient of selection sort
bottom-up heapification, then pop-up, put it on the last pos

## merge sort
recursively build a bigger arranged list with two small arranged list.

## insertion sort
insert every element into right position. often done by some swap actions.

## shell sort
insert sort using a stride length out of one. 
time assumption is unique.
![[Pasted image 20260417160739.png]]

## quick sort
let first(or anyelse) element be the pivot, guarantee any element smaller than pivot is on the left and bigger is on the right (left and right are unsorted)
then, quicksort left and right.
`BSTsort:BST-based insertion sort`

- *Pivot Selection Strategy*
Leftmost
Exact Median
- *Partition Algorithm*         
3scan
Hoare
- *Worst Case Avoidance Strategy*
Shuffle
Exact Median (quick select)
introspection (example : introsort)

以上为基于比较的排序。可以证明，基于比较的排序$O()\supset{}O(nlog(n)) = O(log(n!))$
$log(n!)$ -> 理想情况下二分法找特定全排列

非比较的排序方法：

## counting sort
nothing much to say.
notice that by using a trick of prefix sum we can get a stable sort

## bucket sort
a concept of divide (here) then conquer.
## radix sort
like the sort to strings
requires target has 1's to k's key word (for strings with different length, put 0s at front or back)
LSD sort from back to front. `the reservation of stability`
MSD divide by bucket sort then conquer by bucket sort.





