对于s=\[1,2,3]
s.extend 和s.append有何区别？

s.extend(\[s.append(9), s.append(10)]) 
s
\[1,2,3,9,10,None,None]

s.append(\[s.append(9), s.append(10)]) 
s
\[1,2,3,9,10,\[None,None]]