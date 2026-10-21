	iter（iterable）
next（iterator）


![[Pasted image 20251114143006.png]]

![[Pasted image 20251114145417.png]]
![[Pasted image 20251114150210.png]]
map:
Return an iterator that applies _function_ to every item of _iterable_, yielding the results.

filter:Construct an iterator from those elements of _iterable_ for which _function_ is true.
Note that `filter(function, iterable)` is equivalent to the generator expression `(item for item in iterable if function(item))` if function is not `None` and `(item for item in iterable if item)` if function is `None`.
