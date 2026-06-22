# Leetcode 4. Median of two sorted arrays

## Pattern
Binary Search
Partition

## Goal
Find median of two sorted arrays

## Key Observation
Binary Search is not always on numbers and values in array.
Sometimes it is the partition, the property which leads to designed result.
Median is not mean middle number in an array always but also mean the position which array can be split into equal halves.
In this approach, binary search on cut position is key to the problem.

## Approach
Say nums1,nums2 two arrays, nums1 has to be smaller array, nums2 is larger array.
an array of size n can be cut into n+1 partitions.
make cuts in nums1 , so that left array and right array of nums1 , nums2 is split with equal size.
when making cut1 in nums1, our total left element has to be keep in mind, accordingly cut in nums2. so that total left elements in num1+num2 is total left elements of merged sorted array

## Brute force approach
Merging the two sorted array into one.
Binary search on final sorted array
its expensive
### Time complexity 
O(klogk) where k=m+n
### Space complexity
O(k)

## Optimal Binary Search on Partition
move the cut in nums1 to left, if left element of nums1 contributed many large elements. to eliminate that nums1 large element, move cut in nums1 to left, so partition in nums1 change accordingly and large element in unconsidered in range 
move the cut in nums1 to right, if left element of nums2 contributed many large elements. to eliminate that nums2 large element, move cut in nums1 to right, so partition in nums2 change accordingly and large element is unconsidered.
```python
class Solution:
    
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:

        # nums1 has to be Smaller array 
        # nums2 has to be Larger array
        if len(nums1)>len(nums2):
            nums1,nums2 = nums2,nums1
        m = len(nums1)
        n = len(nums2)
        low = 0
        high = len(nums1)
        int_max = float('inf')
        int_min = -int_max
        totalLeft = (m+n+1)//2
        """
        In this binary search approach ,
        move the cut in nums1 is key to solve this problem
        """
        while low<=high:
            cut1 = (low+high)//2
            diff = abs(totalLeft-cut1)
            cut2 = diff

            lmax1 = nums1[cut1-1] if cut1>0 else int_min
            lmax2 = nums2[cut2-1] if cut2>0 else int_min
            rmin1 = nums1[cut1] if cut1<m else int_max
            rmin2 = nums2[cut2] if cut2<n else int_max

            left = max(lmax1,lmax2)
            right = min(rmin1,rmin2)
            if left<=right:
                print("fine")
                if (m+n)%2==0:
                    return (left+right)/2
                return left
            
            elif lmax1>rmin2:
                high = cut1-1
            else:
                low = cut1+1

        
```
## Time Complexity
O(log(min(m,n)))
## Space Complexity
O(1)
