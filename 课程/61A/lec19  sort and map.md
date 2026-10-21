
# sorted(_iterable_, _/_, _*_, _key=None_, _reverse=False_)
```python
sorted(iterable,key=lambda x:-x.stars)
##stars from more to less
```
Has two optional arguments which must be specified as keyword arguments.

_key_ specifies a function of ==one argument== that is used to extract a comparison key from each element in _iterable_ (for example, `key=str.lower`). The default value is `None` (compare the elements directly).

_reverse_ is a boolean value. If set to `True`, then the list elements are sorted as if each comparison were reversed.



```cpp
sort(iterable,key=[](int a,int b){return a<b})
//
```



	map={}
how to determine if there is the key?
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict