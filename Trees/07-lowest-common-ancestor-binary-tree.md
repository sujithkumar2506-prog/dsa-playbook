# LeetCode 236 - Lowest Common Ancestor of a Binary Tree

## Pattern

- Tree
- DFS
- Bottom-Up Recursion
- Return TreeNode

---

## Core Insight

Each recursive call returns the deepest node among:

- `p`
- `q`
- Lowest Common Ancestor (if already found)
- `None` (if neither exists in the subtree)

---

## Recursive Contract

### Function

`lowestCommonAncestor(node, p, q)`

### Returns

- `None` → Neither `p` nor `q` exists in this subtree.
- `p` or `q` → One target node found.
- `LCA` → Lowest Common Ancestor already determined.

### Parent Expects

The result returned from the left and right subtree to determine whether the current node is the LCA.

---

## Approach

1. If the current node is `None`, return `None`.
2. If the current node is either `p` or `q`, return the current node.
3. Recursively search the left and right subtree.
4. If both recursive calls return non-null nodes, the current node is the LCA.
5. Otherwise, return whichever subtree returned a non-null node.

---

## Takeaways

- The recursion itself carries all the required information.
- No global variable or extra data structure is needed.
- A node becomes the LCA only when one target is found in each subtree.
- If only one subtree returns a node, propagate it upward.

---

## Code

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':

        if not root:
            return None

        if root is p or root is q:
            return root

        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        if left and right:
            return root

        return left or right
```

---

## Time Complexity

```text
O(n)
```

Each node is visited exactly once.

---

## Space Complexity

```text
O(h)

Worst Case (Skewed Tree): O(n)
Balanced Tree: O(log n)
```
