![[Pasted image 20251029173422.png]]
![[Pasted image 20251029174529.png]]

the most important:know exactly what your function do
(by express and detail:what are its input and output?believe your func can do it!!)
如何验证？：
1.初始情况
2.n-->n+1(1+2=数学归纳法！！)
3.边际条件


#### is_prime的递归写法
```py
def is_prime(n):
	 def f(i): 
		if i == n:
			return True 
		elif n%i==0: 
			return False
		else: 
			return f(i+1) 
	return f(2)
```
# tree recursion
求斐波那契数列用递归：压栈量指数级上升！怎么办？
维护一个数组！(并调用)

tree recursion其一：递推
##### Counting Partitions
The number of partitions of a positive integer n, using parts up to size m, is the number
of ways in which n can be expressed as the sum of positive integer parts up to m in
increasing order.
example：CountingPartition（6，4）=9
6=
2+4
1+1+4
3+3
1+2+3
1+1+1+3
2+2+2
1+1+2+2
1+1+1+1+2
1+1+1+1+1+1

recursion leap:
![[Pasted image 20251209110215.png]]

