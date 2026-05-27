# sort
```cpp
void sort( RandomIt first, RandomIt last );
void sort( RandomIt first, RandomIt last, Compare comp );
bool cmp(const Type1& a, const Type2& b);
```
Sorts the elements in the range `[`first`,` last`)` in non-descending order. The order of equal elements ==is not guaranteed to be preserved.==
1) Elements are [sorted](https://en.cppreference.com/w/cpp/algorithm.html#Requirements "cpp/algorithm") with respect to operator<(until C++20)[std::less](https://en.cppreference.com/w/cpp/utility/functional/less.html){}(since C++20).
2) Elements are sorted with respect to comp.

# unique

```cpp
ForwardIt unique( ForwardIt first, ForwardIt last );
ForwardIt unique( ExecutionPolicy&& policy,ForwardIt,first,ForwardIt,last );
ForwardIt unique( ForwardIt first, ForwardIt last, BinaryPred p );
```
Removes all except the first element from every consecutive group of equivalent elements from the range `[`first`,` last`)` and returns a past-the-end iterator for the new end of the range.
1) Elements are compared using operator==.
 If operator== does not establish an [equivalence relation](https://en.wikipedia.org/wiki/equivalence_relation "enwiki:equivalence relation"), the behavior is undefined.
3) Elements are compared using the given binary predicate p.
 If p does not establish an equivalence relation, the behavior is undefined.

# lower_bound

```cpp
ForwardIt lower_bound( ForwardIt first, ForwardIt last,const T& value );
ForwardIt lower_bound( ForwardIt first, ForwardIt last,const T& value, Compare comp );
```
Searches for the first element in the partitioned range `[`first`,` last`)` which is **not** ordered before value.
1) The order is determined by operator<:

|                                                                                                                                                                                                                                                                                                                                                                  |               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Returns the first iterator iter in `[`first`,` last`)` where bool(*iter < value) is false, or last if no such iter exists.<br><br>If the elements elem of `[`first`,` last`)` are not [partitioned](https://en.cppreference.com/w/cpp/algorithm.html#Requirements "cpp/algorithm") with respect to the expression bool(elem < value), the behavior is undefined. | (until C++20) |
| Equivalent to std::lower_bound(first, last, value, [std::less](https://en.cppreference.com/w/cpp/utility/functional/less.html){}).                                                                                                                                                                                                                               | (since C++20) |
2) The order is determined by comp:

 Returns the first iterator iter in `[`first`,` last`)` where bool(comp(*iter, value)) is false, or last if no such iter exists.

 If the elements elem of `[`first`,` last`)` are not [partitioned](https://en.cppreference.com/w/cpp/algorithm.html#Requirements "cpp/algorithm") with respect to the expression bool(comp(elem, value)), the behavior is undefined.


# upper_bound

```cpp
ForwardIt upper_bound( ForwardIt first, ForwardIt last,const T& value );
ForwardIt upper_bound( ForwardIt first, ForwardIt last,const T& value, Compare comp );
```
Searches for the first element in the partitioned range `[`first`,` last`)` which is ordered after value.

1) The order is determined by operator<:

|                                                                                                                                                                                                                                                                                                                                                                 |               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Returns the first iterator iter in `[`first`,` last`)` where bool(value < *iter) is true, or last if no such iter exists.<br><br>If the elements elem of `[`first`,` last`)` are not [partitioned](https://en.cppreference.com/w/cpp/algorithm.html#Requirements "cpp/algorithm") with respect to the expression bool(value < elem), the behavior is undefined. | (until C++20) |
| Equivalent to std::upper_bound(first, last, value, [std::less](https://en.cppreference.com/w/cpp/utility/functional/less.html){}).                                                                                                                                                                                                                              | (since C++20) |
|                                                                                                                                                                                                                                                                                                                                                                 |               |

2) The order is determined by comp:

 Returns the first iterator iter in `[`first`,` last`)` where bool(comp(value, *iter)) is true, or last if no such iter exists.

 If the elements elem of `[`first`,` last`)` are not [partitioned](https://en.cppreference.com/w/cpp/algorithm.html#Requirements "cpp/algorithm") with respect to the expression bool(comp(value, elem)), the behavior is undefined.