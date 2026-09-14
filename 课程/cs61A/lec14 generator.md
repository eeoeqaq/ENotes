```python
def a():
	...
	...
	yield sth
	...
	...
	yield sth
```

i=a(),程序还没有被执行
next（i）执行到下一个yield 返回一个值

both generator and iterator：compute lazily
what is generator?
A function which returns a [generator iterator](https://docs.python.org/3.14/glossary.html#term-generator-iterator). It looks like a normal function except that it contains [`yield`](https://docs.python.org/3.14/reference/simple_stmts.html#yield) expressions for producing a series of values usable in a for-loop or that can be retrieved one at a time with the [`next()`](https://docs.python.org/3.14/library/functions.html#next "next") function.
```
:::yield from:::
def a(list1):
	yield from list1
```
```
def count(n):
	if n>0:
		yield(n)
		yield from count(n-1)


```
```
def prefix(s):
    if s:
        yield from prefix(s[:-1])
        yield s

def substr(s):
    if s:
        yield from prefix(s)
        yield from substr(s[1:])
```

![[e1b00d25dab780824c56c886f4a81c6d.png]]
