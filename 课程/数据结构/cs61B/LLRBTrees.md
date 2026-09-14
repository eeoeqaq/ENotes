# 理论
tranform a 23 tree to BST -> LLRB

# 性质
	黑高平衡
	左倾，无相连红节点

# 实现
```java
if (tar.left != null && tar.left.colorTowardsParent == color.red && tar.left.left != null && tar.left.left.colorTowardsParent) rotateLeft(tar);

if (isRed(tar.right)) rotateLeft(tar);

if (isRed(tar.right)) return rotateLeft(tar);

if (isRed(tar.right)) tar = rotateLeft(tar);

```

```java
if (tar.right == null && tar.right.colorTowardsParent == color.red && tar.right.right == null && tar.right.right.colorTowardsParent == color.red) rotateRight(tar);
if (isRed(tar.left) && isRed(tar.left.left)) rotateRight(tar);
if (isRed(tar.left) && isRed(tar.left.left)) return rotateRight(tar);
if (isRed(tar.left) && isRed(tar.left.left)) tar = rotateRight(tar);
```
`山重水复疑无路，柳暗花明又一村。
这里体现了如下思想：
	极度巧妙的递归！
	逻辑运算截断效应的妙用
	函数返回值的物尽其用

# 删除
如何在删除时保持原有rb性质？或许可以从bst删除和btree（23tree）里找到灵感
## bst：
是否为根节点？
有几个子嗣？
0个直接删，1个删后上接，2个看tar属于左枝右枝，同属性枝上接（tar左枝则tar的左枝作为新左枝），异属性枝接在与tar.parents 值最相近的tar的异侧叶节点
## 23t：
是否为根节点？
不是 - 和值最相近的右（左）侧叶节点交换
是 - 
是否为3node？
是 - 直接删
不是 - 删除留下emptyleaf
### filling in empty node FIEN 
try to del EN everywhere and assume empty node has one children

case 1 : 有3node sibling
rotate即可
 
case 2 : 无3node sibling， 有3node parent
`X and right sibling steal parent’s keys. Middle sibling moves into the parent.

case 3 : 无3node sibling、3node parent
merge parent and sibling into a 3node
move the EN up

## finally : LLRBT
最后我们来写LLRBT的删除。。。
how？
向下找，找到，交换？？ 叶节点删除？？？

再引入另一种23Tree删除：
在我们递归式下探时，保证我们每次下探来到的都是3node 
用和上述技巧类似的旋转合并操作可以实现
找到目标后与右树最小值交换，删除目标 ：可以保证目标最后处于一个3node内










