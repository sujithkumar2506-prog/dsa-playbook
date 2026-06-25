# LeetCode 100 - Same Tree

## Pattern

Tree, DFS, Recursion, Compare Two Trees

## Problem Statement

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same.

Two binary trees are considered the same if:

* They are structurally identical.
* Corresponding nodes have the same value.

---

## Key Insight

Compare both trees simultaneously.

At every recursive call:

* If both nodes are `None`, they are identical.
* If only one node exists, trees differ.
* If both exist but values differ, trees differ.
* Otherwise, recursively compare both left subtrees and both right subtrees.

---

## Recursive Contract

**Function Name**

`isSameTree(node1, node2)`

**Input**

* Current node from Tree 1
* Current node from Tree 2

**Returns**

* `True` if both subtrees rooted at these nodes are identical.
* `False` otherwise.

**Parent Expects**

Whether both corresponding subtrees are identical.

---

## Approach

1. If both nodes are `None`, return `True`.
2. If both nodes exist and values are equal:

   * Compare left subtrees.
   * Compare right subtrees.
3. If any condition fails, return `False`.

---

# Code

```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:

        if not p and not q:
            return True

        if p and q and p.val == q.val:
            return (
                self.isSameTree(p.left, q.left) and
                self.isSameTree(p.right, q.right)
            )

        return False
```

---

## Time Complexity

```
O(n)
```

* Visit each corresponding node once.
* `n` = number of nodes.

---

## Space Complexity

```
O(h)
```

* `h` = height of the tree due to recursion stack.
* Worst Case (Skewed Tree): `O(n)`
* Balanced Tree: `O(log n)`

---

## Takeaways

* This is the first tree problem that uses **two recursive parameters**.
* Compare the current nodes first, then recursively compare their children.
* The recursive function returns exactly what the parent needs:

  > "Are these two subtrees identical?"
### Solution can be obtained using BFS level order traversal Queue as well.
