# Pattern
BFS
Queue
Math

## Problem
Given a binary tree , must find the bottom view and top view of the binary tree.
## Approach
BFS traversal on level is the key
Initialize a Queue for BFS. We have to keep in mind the distance of all nodes, so we are pushing (node,distance) into queue.
Root is base distance 0. nodes left to root are its parent node-1. right to root are parent node+1.
This way , we can see for all distance last seen node. Using Hash Map to override latest seen distance nodes.
once got node val based on distances, sort in acending order based on distance.

## Insights
DFS traversal is key when problem has to find anything that needs from child
BFS is used for level wise traversal problem
## Code
### Bottom view
```python
class Solution:
    def bottomView(self, root):
        # code here
        dis = 0
        Q = deque()
        Q.append((root,dis))
        
        mapp = {}
        
        while Q:
            node,dis = Q.popleft()
            mapp[dis] = node.data
            
            if node.left:
                Q.append((node.left,dis-1))
            if node.right:
                Q.append((node.right,dis+1))
                
        res = list(mapp.items())
        # print(res)
        res.sort(key= lambda x: x[0])
        ans = []
        for _,val in res:
            ans.append(val)
        # print(ans)
        return ans
        
```

### Top view
```python
class Solution:
    def topView(self, root):
        # code here
        Q = deque()
        mapp = {}
        dis = 0
        Q.append((root,dis))
        
        while Q:
            node,dis = Q.popleft()
            if dis not in mapp:
                mapp[dis] = node.data
            if node.left:
                Q.append((node.left,dis-1))
            if node.right:
                Q.append((node.right,dis+1))
                
        res = list(mapp.items())
        res.sort(key = lambda x: x[0])
        ans = []
        for _,val in res:
            ans.append(val)
            
        return ans
```
## Time Complexity
O(nlogn) -- worst case
O(n) -- average case
## Space Complexity
O(n)
