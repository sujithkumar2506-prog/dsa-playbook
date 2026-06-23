# LeetCode 378 - Kth Smallest Element in a Sorted Matrix

## Pattern

Binary Search on Answer

## Core Insight

Need to count how many elements are <= mid.
Since rows and columns are sorted, start from bottom-left.
If current <= mid:
- Count row + 1 elements.
- Move right.
Else:
- Move up.

## Helper Function

countLessEqual(mid)

## Binary Search

Search on value range.

Low = matrix[0][0]

High = matrix[n-1][n-1]

Condition:
count >= k

Need:
First True

Return:
low

## Code
```python
class Solution:
    # Helper function to return how many elements less than equal to give mid element
    def countLessEqual(self,matrix,mid):

        rows,cols = len(matrix),len(matrix[0])
        grid = matrix
        ans  = 0
        r = rows-1
        c = 0

        while r>=0 and c<cols:
            if grid[r][c] <= mid:
                ans += (r+1)
                c+=1
            else:
                r-=1
        return ans

    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        rows = len(matrix)
        cols = len(matrix[0])
        grid = matrix
        low = grid[0][0]
        high = grid[-1][-1]
        # ans =-1
        while low<=high:
            mid = (low+high)//2
            getK = self.countLessEqual(grid,mid)
            if getK<k:
                low = mid+1
            else:
                # ans = mid
                high = mid-1
        
        return low

```

## Time Complexity

O(n log(maxValue - minValue))

## Mistakes I Made
- Initially thought of searching indices.
- Needed to search values instead.
- Remember: return low because this is First True.
