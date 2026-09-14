# functional language
![[Pasted image 20251231111839.png]]
	对于一种函数类语言，大量的递归使我们需要尾递归将空间复杂度从O（n）降至O（1）。无疑的，我们应该对一些递归调用使用尾递归。主旨思想是这应该是我们返回前干的最后一件事。用tail context来确定这样的expression。
	如果一个过程调用返回后，**当前函数不需要再做任何事情**（不需要再计算、组合、加法、cons、比较……），而是**直接把它的返回值作为自己的返回值**，那么这个调用就在**尾位置**，是**尾调用**。  
	当尾调用的目标过程恰好是“自己”时，就是**尾递归**。
__tail context__
	last body expression of lambda expression
	2 & 3 expression of  a tail context __if__ expression
	all non-predicate expressions in a tail context __cond__ 
	last expression of a lambda expression __/or/and/begin__
## rewrite linear recursive procedures to use tail calls



