# LeetCode 687 - Longest Univalue Path

## Pattern

- Tree
- DFS
- Bottom-Up Recursion
- Global Answer

---

## Key Idea

Each node returns the **longest same-value path (in edges) that can be extended to its parent**.

A node may combine both left and right same-value paths to update the global answer, but it can return only one path to its parent.

---

## Recursive Contract

### Function

`dfs(node)`

### Returns

Longest downward path (in edges) starting from the current node where all nodes have the same value.

### Parent Expects

The longest extendable same-value path from its child.

---

## Approach

1. Recursively compute the longest same-value path from the left and right child.
2. If the left child has the same value, extend the left path.
3. If the right child has the same value, extend the right path.
4. Update the global answer using `leftEdge + rightEdge`.
5. Return `max(leftEdge, rightEdge)` to the parent.

---

## Takeaways

- Path length is measured in **edges**, not nodes.
- A parent can combine both child paths.
- A parent can extend only **one** child path upward.
- Recursive contract is almost identical to Diameter of Binary Tree.

---

## Code

```python
class Solution:
    def longestUnivaluePath(self, root: Optional[TreeNode]) -> int:

        ans = [0]

        def dfs(node):

            if not node:
                return 0

            leftChild = dfs(node.left)
            rightChild = dfs(node.right)

            leftEdge = rightEdge = 0

            if node.left and node.val == node.left.val:
                leftEdge = 1 + leftChild

            if node.right and node.val == node.right.val:
                rightEdge = 1 + rightChild

            ans[0] = max(ans[0], leftEdge + rightEdge)

            return max(leftEdge, rightEdge)

        dfs(root)
        return ans[0]
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
