# Leetcode problem 875
# Pattern
first Occurence, boundary search
## Problem statement
oko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.
Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.
Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return. Return the minimum integer k such that she can eat all the bananas within h hours.

## Goal 
Return minimum possible k bananas per hour to be eaten within h hours

## Observation
Not all problem we apply left,right vals on arrays. It depends on problem

## Approach
initialize low,high values on 1 and maximum of piles.
take mid_k and compute total hours taken at mid_k rate and compare with given hour
if it less than or equal to given h, shrink the search space to left half, discard the right half
if not less, shrink the search space to right half.
## Key Insight
this pattern reminds me of first occurence, meaning in a monotonic increasing search space, if one element is valid, all element to its right are valid, so we continue to search for the minimum in left half.

# Code
'''python
class Solution:
    # Helper function to return total hours taken at k rate
    def totalHours(self,piles,k):
        summ = 0
        for bananas in piles:
            summ+= ceil(bananas/k)
        return summ

    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        low,high = 1,max(piles)
        while low<=high:
            mid_k = (low+high)//2
            hoursTaken = self.totalHours(piles,mid_k)
            if hoursTaken<=h:
                high = mid_k-1
            else:
                low = mid_k+1
        return low
```

## Time Complexity
O(nlogn)

## Space Complexity
O(1)
