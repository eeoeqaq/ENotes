environmental diagram 
https://pythontutor.com/cp/composingprograms.html#mode=edit
什么是environment 和frame？
	frame是一系列名称和值（或函数）的对应
	environment是一系列frame
	name：A name evaluates to the value bound to that name in the earliest
	frame of the current environment in which that name is found.

print (print (1),print (2))  returns what?
1 
2
None None

why?
void print(a)
	"write a on screen"

返回值为None

一道好题：
The function tik takes an argument tok and returns a function insta that takes an argument gram. The insta function prints tok and gram on the same line separated by a space and has no return statement. Its implementation has been omitted intentionally. 
```
def tik(tok):
	"""Returns a function that takes gram and prints tok and gram on a line. >>> tik(5)(6) 5 6 """
	def insta(gram):
	 ... # The implementation of this function has been omitted.
	return insta i.  
 ```
	  
	  
What would the interactive Python interpreter display upon evaluating the expression?:
tik (tik (5)(print (6)))(print (7))