`data indexed array: ocupied too much memory`
`how to smaller the size, and has a O(1) insert and check?`


# hashcode
casting a value from a set of huge number(or even infinity)of vals to a set of smaller number of vals


Warning : Never override equals without also overriding hashCode.
- Can also lead to items getting lost and generally weird behavior.
    
- HashMaps and HashSets use equals to determine if an item exists in a particular bucket.

- 如果 `a.equals(b)` 为 `true`，那么 **`a.hashCode() == b.hashCode()` 必须为 `true`**
- 反过来不要求：hash 相同不一定 equals 相同（会有碰撞）

# hashtable

implmentation
even distribution
bucket
open addressing
