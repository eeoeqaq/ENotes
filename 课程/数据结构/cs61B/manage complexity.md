
What is complexity in CS? Anything in a system that disturb you to understand and modify it.
### Three symptoms of complexity:
- modify amplification: how much you have to re-code to modify
- cognitive afford: how many you need know to modify
- unknown unknowns: can't figure out where to re-code to modify

### How to control it?
- If have to make a part more complex, choose one you spend less time.
- time investment
	- Rather than implementing the first idea, try coming up with (and possibly even partially implementing) a few different ideas.
    - When you feel like you have found something that feels clean, then fully implement that idea.
    - In real systems: Try to imagine how things might need to be changed in the future, and make sure your design can handle such changes.
- avoid patch making a.k.a. many if-else branches. Instead, change the base design gracefully. 
- avoid "temporal decomposion"

![[Pasted image 20260418140736.png]]
try to tell the informal parts properly
