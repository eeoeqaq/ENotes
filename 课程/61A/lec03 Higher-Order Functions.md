高阶函数
实例：用函数模拟求和符号

为什么不用函数取代控制语句？
if_(c,f,t)
	if c:
		return f
	else:
		 return t

函数计算时必须全部计算c，f，t的值

条件运算符使用例：
have_big_square:
	x>0 and sqrt(x)>10
not_too_big:
	x == 0 or 1/x!=0


创建返回值为函数的函数：
函数的泛化

```def 
  def area(x,constant):
	  assert x>0
	  return x*x*constant
  def hexagon(x):
	  return area(x,3*sqrt(3)/2)
	  
  def square(x):
	  def triangle(x):
	  
   
   
```


	sasa