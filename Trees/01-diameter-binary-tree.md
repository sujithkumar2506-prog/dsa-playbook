# LeetCode 543 - Diameter of Binary Tree

## Pattern

Tree, DFS, Bottom-Up Recursion

## Problem Statement

Given the `root` of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes. This path may or may not pass through the root.

---

## Key Insight

Each node should return the **height of its subtree** to its parent.

While returning the height, compute the diameter passing through the current node.

```
Diameter through current node = Left Height + Right Height
```

Maintain a global maximum diameter while traversing all nodes.

---

## Recursive Contract

**Each node returns:**

- Height of its subtree.

**Each node computes:**

- Diameter passing through itself.
- `leftHeight + rightHeight`

**Global variable stores:**

- Maximum diameter among all nodes.

---

## Why Bottom-Up?

The current node cannot compute its diameter until both children return their heights.

Information flows from:

```
Leaf
  ↑
Parent
  ↑
Root
```

Hence, this is a **Bottom-Up DFS** problem.

---

## Approach

1. Perform DFS recursively.
2. Get left subtree height.
3. Get right subtree height.
4. Update global diameter using:
   ```
   leftHeight + rightHeight
   ```
5. Return:
   ```
   1 + max(leftHeight, rightHeight)
   ```

---

# Code

```python
class Solution:
    def __init__(self):
        self.maxDiameter = 0

    def height(self, node):
        if not node:
            return 0

        leftHeight = self.height(node.left)
        rightHeight = self.height(node.right)

        self.maxDiameter = max(
            self.maxDiameter,
            leftHeight + rightHeight
        )

        return 1 + max(leftHeight, rightHeight)

    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.height(root)
        return self.maxDiameter
```

---

## Time Complexity

```
O(n)
```

Every node is visited exactly once.

---

## Space Complexity

```
O(h)
```

- `h` = height of the tree.
- Worst Case (Skewed Tree): `O(n)`
- Balanced Tree: `O(log n)`

---

## Takeaways

- Think from the **parent's perspective**:
  > "What information do I need from my children?"

- Each node returns **height**, not diameter.

- The diameter is a **side computation** while combining the heights of the left and right subtrees.

- This problem introduces the powerful tree pattern:

  **Return one value to the parent while updating a global answer.**
