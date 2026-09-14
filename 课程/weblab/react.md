tree-like structure
root - parents - child - leaf
###### props
- immutable
- from parents to childs

###### states
- mutable
- parents' states depends childs' props(usual)

```js
import React,{ setState } from "react";

const Post = (prop) => {
	const [isLiked, setIsLiked] = setState(false) 
	
	return (
		<div className = "post">
			<p>{prop.name}<p>
			<p>{prop.content}<p>
			<button
				onClick = {() => {
					setIsLiked(!isLiked)
				}}>	
				{isLiked ? "Liked" : "Like"}
			</button>	
		</div>
	)
}
```


##### components life circle
	mount -> state change -> rerander -> ...... -> dismount
DOM and react virtual DOM `document object model`
	`trigger render commit


###### routing
```jsx
import { Link } from "react-router-dom";
<Link to="/" className="NavBar-link">1</Link>
```
