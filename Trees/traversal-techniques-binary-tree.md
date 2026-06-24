Traversal -> traversing the binary tree to find relation, node etc...

# Traversal Types
## Inorder
This method follows the technique first exploring the left subtree followed by visiting current node and exploring right subtree
Can be implemented using recursion and stack as well.
Stack implementation has a tiny edge over recursion in terms of memory.
Below is my Recursion way Inorder traversal implemention in C++.
```cpp
//Node Structure
class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int x) {
        data = x;
        left = right = NULL;
    }
};

void inOrder(Node* node, vector<int>& res) {
    if (node == nullptr)
        return;
        
    // Traverse the left subtree first
    inOrder(node->left, res);
    
    // Visit the current node
    res.push_back(node->data);
    
    // Traverse the right subtree last
    inOrder(node->right, res);
}

```

## PreOrder Traversal
This method starts off, first visiting current node followed exploring left subtree and right subtree.
Below is implementation of PreOrder traversal using recursion.
```cpp
void preOrder(Node* node, vector<int>& res) {
    if (node == nullptr)
        return;

    // Visit the current node first
    res.push_back(node->data);

    // Traverse the left subtree
    preOrder(node->left, res);

    // Traverse the right subtree
    preOrder(node->right, res);
}
```
## PostOrder Traversal
This methods starts first exploring left subtree followed by right subtree and finally visiting current node itself.
Below is implementation of PostOrder traversal using recursion.
```cpp
void postOrder(Node *node, vector<int> &res)
{
    if (node == nullptr)
        return;
    // First we traverse left subtree
    postOrder(node->left, res);
    // After visiting left, traverse right subtree
    postOrder(node->right, res);
    // now we visit node
    res.push_back(node->data);
}
```

## Level Order Traversal
Level order traversal is process of exploring tree elements by levels. Starting with level 0 root node, followed by level 1 nodes from left to right and so on.
Queue is designed data structure to implement this traversal as it propose FIFO.
```cpp
void levelOrderRec(Node* root, int level, vector<vector<int>>& res) {
    // Base case
    if (root == nullptr) return;
    // Add a new level to the result if needed
    if (res.size() <= level) res.push_back({});
    // Add current node's data to its corresponding level
    res[level].push_back(root->data);
    // Recur for left subtree and right subtree
    levelOrderRec(root->left, level + 1, res);
    levelOrderRec(root->right, level + 1, res);
}

// Function to perform level order traversal
vector<vector<int>> levelOrder(Node* root) {
    // Stores the result level by level
    vector<vector<int>> res; 
    levelOrderRec(root, 0, res);
    return res;
}
```
## Key Insights
Why this many traversals??. Well the advantage of binray tree is its efficient access and insertion and deletion. to do so, we need to traverse the tree.
Each traversal methods has its own advantage. Depending upon its purpose use right traversal method.
### Base case defining is key in recursion implementation.
