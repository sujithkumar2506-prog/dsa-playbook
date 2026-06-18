# LeetCode Problem - 34

# Pattern : Binary Search on Boundary

# Goal
Find the first and last occurrence of a target element in a sorted array.

## Observation
A normal binary search stops as soon as it finds the target.

This problem is different.

Finding one occurrence is **not enough**. We need to continue searching to find the leftmost and rightmost occurrences.
## Key Insight

When a target is found:

- For the **first occurrence**, continue searching on the **left half**.
- For the **last occurrence**, continue searching on the **right half**.

The answer is **not necessarily at the first match**.

---

# Pattern

## First Occurrence

Whenever target is found:

ans = mid;
right = mid - 1;

Reason:

There may be another occurrence further left.

Continue searching.

---

## Last Occurrence

Whenever target is found:

```cpp
ans = mid;
left = mid + 1;
```

Reason:

There may be another occurrence further right.

Continue searching.

---

# Mental Model

Normal Binary Search

Goal:

```
Find ANY target.
Boundary Binary Search
Goal:

Find the LEFT boundary
OR
Find the RIGHT boundary.

# Focus Variable
Normal Binary Search

Focus on mid.
```

Boundary Binary Search

```
Focus on answer (ans).

Whenever target is found,
update ans,
then continue searching.

# Why not return immediately

Because finding the target does not guarantee it is the first or last occurrence.

We must continue searching until no better candidate exists.


# First Occurrence

# cpp
int ans = -1;

while(left <= right){

    int mid = left + (right-left)/2;

    if(nums[mid] == target){
        ans = mid;
        right = mid - 1;
    }
    else if(nums[mid] < target){
        left = mid + 1;
    }
    else{
        right = mid - 1;
    }
}

return ans;
```

---

## Last Occurrence

```cpp
int ans = -1;

while(left <= right){

    int mid = left + (right-left)/2;

    if(nums[mid] == target){
        ans = mid;
        left = mid + 1;
    }
    else if(nums[mid] < target){
        left = mid + 1;
    }
    else{
        right = mid - 1;
    }
}

return ans;
```

---

# Time Complexity

O(log n)

# Space Complexity

O(1)

---

# Pattern Recognition

Whenever the problem asks:

- First occurrence
- Last occurrence
- Left boundary
- Right boundary
- Lower bound
- Upper bound

Think:

> "Don't stop after finding the target. Continue searching toward the required boundary."
