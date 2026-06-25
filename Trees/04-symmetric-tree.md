# LeetCode 101 - Symmetric Tree

## Pattern

Tree, DFS, Mirror Recursion

## Problem Statement

Given the root of a binary tree, determine whether it is symmetric around its center.

---

## Key Insight

Instead of comparing:

```
Left ↔ Left
Right ↔ Right
```

compare mirror nodes:

```
Left ↔ Right
Right ↔ Left
```

---

## Recursive Contract

**Function Name**

`isMirror(node1, node2)`

**Input**

* Left subtree node
* Right subtree node

**Returns**

* True if both subtrees are mirror images.

---
## Code
```python
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        
        if root==None:
            return
        Queue = deque()
        Queue.append((root.left,root.right))

        while Queue:
            
            L,R = Queue.popleft()
            if L==None and R==None:
                continue
            if L==None or R==None or L.val!=R.val:
                return False
            Queue.append((L.left,R.right))
            Queue.append((L.right,R.left))


        return True
```
## Approach

1. If both nodes are `nullptr`, return true.
2. If only one node exists, return false.
3. If values differ, return false.
4. Compare:

   * Left of first with Right of second.
   * Right of first with Left of second.

---

## Time Complexity

```
O(n)
```

---

## Space Complexity

```
O(h)
```

---

## Takeaways

* Extension of Same Tree.
* Compare mirror children instead of corresponding children.
* First mirror-recursion pattern.
