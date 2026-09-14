异步
- 异步与多线程

```js
const promise1 = get();
const promise2 = get();
console.log(promise1+promise2);
const promises = [promise1, promise2];
Promise.all(promises).then();
Promise.race(promises).then();
Promise.any(promises).then();
```

##### async and await
```js
console.log(await promise1 + await promise2);
```

##### context
- Contexts provide a way for higher-level components in our tree to
communicate to all of its sub-components.
```jsx
const UserContext = createContext();
```

创建 Context
↓
```jsx
<UserContext.Provider value={{ user }}>
```

提供数据
↓
```jsx
const { user } = useContext(UserContext);
```
读取数据