So what happens is that you set the parent of a function to be whatever the current frame is when that function was created.
创建函数（def）时所在帧成为该函数父级
调用函数时创建新帧，其父级即为函数父级

nested def：
The inner def is going to have the frame of the outer def's function call.
内部 def 将具有外部 def 函数调用产生的的框架。

How to Draw an Environment Diagram
When a function is defined:
Create a function value: func <name>(<formal parameters>)[parent=<parent>]
Its parent is the current frame.
When a function is called:
1.Add a local frame, titled with the <name> of the function being called.
2.Copy the parent of the function to the local frame: [parent=<label>]
3.Bind the <formal parameters> to the arguments in the local frame.
4. Execute the body of the function in the environment that starts with the local frame.

柯里化新方法！
def curry2(f):
	def g(x):
		def h(y):
			 return f(x,y)
		return h	 
	return g	 

**==curry2=lambda f : lambda x : lambda y :f(x,y)==** 

>>>(lambda: 3)()
3
直接写lambda x：x返回的是这个函数的’函数名‘（？）
a=lambda: 3
定义中抛除了def return 函数名
def k()
	return 3
a=k

