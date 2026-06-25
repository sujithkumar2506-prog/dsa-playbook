# LeetCode 226 - Invert Binary Tree

## Pattern

Tree, DFS, Tree Manipulation

## Problem Statement

Given the root of a binary tree, invert the tree and return its root.

---

## Key Insight

Every node swaps its left and right children.

After swapping, recursively invert both subtrees.

---

## Recursive Contract

**Function Name**

`invert(node)`

**Input**

* Current node

**Returns**

* Nothing

**Responsibility**

* Swap left and right child.
* Recursively invert both children.

---

## Approach

1. If node is `nullptr`, return.
2. Swap left and right child.
3. Recurse on left subtree.
4. Recurse on right subtree.

---

# Code

```cpp
class Solution {
public:
    void invert(TreeNode* root) {
        if (root == nullptr)
            return;

        swap(root->left, root->right);

        invert(root->left);
        invert(root->right);
    }

    TreeNode* invertTree(TreeNode* root) {
        invert(root);
        return root;
    }
};
```

---

## Time Complexity

```
O(n)
```

Every node is visited once.

---

## Space Complexity

```
O(h)
```

* Worst Case: O(n)
* Balanced Tree: O(log n)

---

## Takeaways

* Tree structure can be modified recursively.
* Not every recursive function has to return a value.
* Parent modifies itself before delegating work to children.
