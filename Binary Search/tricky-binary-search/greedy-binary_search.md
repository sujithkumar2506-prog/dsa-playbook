# LeetCode 1552 - Magnetic Force Between Two Balls

## Pattern

**Primary Pattern:** Binary Search on Answer

**Secondary Pattern:** Greedy

---

# Goal

Find the **maximum possible minimum distance** between any two balls placed in the baskets.

---

# Key Observation

If a minimum distance **k** is feasible, then every distance smaller than **k** is also feasible.

# Search Space

### Answer Variable

Minimum distance between any two balls.

### Lower Bound

```python
1
```

Reason:

The smallest possible distance between two balls.

### Upper Bound

```python
position[-1] - position[0]
```

Reason:

The largest possible distance is between the first and last basket.

---

# Core Insight

Instead of searching basket positions, search every possible minimum distance.

For every guessed distance **k**:

- Place the first ball in the first basket.
- Greedily place every remaining ball in the first valid basket.
- If all **m** balls can be placed, try a larger distance.
- Otherwise, search for a smaller distance.

---

# Helper Function

### Purpose

Checks whether **m** balls can be placed while maintaining at least **k** distance.

# Binary Search Logic

If helper(mid) is **True**

```python
low = mid + 1
```

Reason:

Current distance works.
Try to maximize the answer.

---

If helper(mid) is **False**

```python
high = mid - 1
```

Reason:

Current distance is too large.
Search for a smaller distance.

---

# Code

### Python

```python
class Solution:
    def maxDistance(self, position: List[int], m: int) -> int:

        position.sort()

        def canPlace(balls, distance):

            prev = position[0]
            balls -= 1

            for curr_pos in position[1:]:

                if curr_pos - prev >= distance:
                    balls -= 1
                    prev = curr_pos

            return balls <= 0

        low = 1
        high = position[-1] - position[0]

        while low <= high:

            mid = (low + high) // 2

            if canPlace(m, mid):
                low = mid + 1
            else:
                high = mid - 1

        return high
```

### C++

```cpp
class Solution {
public:

    bool canPlace(vector<int>& position, int balls, int distance){

        int prev = position[0];
        balls--;

        for(int i = 1; i < position.size(); i++){

            if(position[i] - prev >= distance){
                balls--;
                prev = position[i];
            }
        }

        return balls <= 0;
    }

    int maxDistance(vector<int>& position, int m) {

        sort(position.begin(), position.end());

        int low = 1;
        int high = position.back() - position.front();

        while(low <= high){

            int mid = low + (high - low) / 2;

            if(canPlace(position, m, mid))
                low = mid + 1;
            else
                high = mid - 1;
        }

        return high;
    }
};
```

---

# Complexity

### Time Complexity

```
O(n log D)
```

where

- n = number of baskets
- D = position[n−1] − position[0]

### Space Complexity

```
O(1)
```

---

# Mistakes / Edge Cases

- Sort the basket positions first.
- Always place the first ball in the first basket.
- Never use `abs()` since the positions are sorted.
- Greedily choose the first valid basket.
- Return `high`, not `low`.
- This is a **Maximum Feasible Answer** problem.

---

# Pattern Takeaway

Whenever a problem asks:

- Maximum of Minimum
- Largest Feasible Answer

Try Binary Search on Answer.

The helper function should answer:

```python
canPlace(mid)
```

Binary Search Pattern:

```python
if canPlace(mid):
    low = mid + 1
else:
    high = mid - 1

return high
```

---

# Similar Problems

- LC 875 - Koko Eating Bananas
- LC 1011 - Capacity To Ship Packages Within D Days
- LC 1482 - Minimum Number of Days to Make m Bouquets
- LC 410 - Split Array Largest Sum
