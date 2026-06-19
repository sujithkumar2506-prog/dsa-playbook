# LeetCode Problem : 162

## Problem Name : Find Peak element

# Pattern 
Hill direction search

# Goal 
Find any peak Element

# Observation
Not a typical binary search or insertion pattern. a bit tricky one
not all the time left<=right works, depend upon problem case we use left<right

# Approach
We comparing element, consider we are standing at point, there can slope on either sides, these slopes are way to peak of hill(peak element).
compare with next element, so that guarantees the direction of peak element exists

# Key Insight
In this approach, we are comparing mid with mid+1 element.
if nums[mid] < nums[mid+1] then there must be peak element from mid+1 to right array, Discard the left half.
if nums[mid] > nums[mid+1] then there must be peak element from left to mid. not exclduing mid, 
unlike typical binary search problem does right = mid-1. We are not sure mid-1 contains ele greater than mid.
left<right instead of left <=right handles cases 
when there is one element in an array, avoid mid<mid+1 index out of bound exception
 ### key var used is left , move left to close to the slope possible and return left.

# Code section
## Java
```Java
class Solution {
    public int findPeakElement(int[] nums) {
     int left,right,mid,ans;
     left = 0;
     right = nums.length-1;
    
     while(left<right){
        mid = left+(right-left)/2;
        
        if(nums[mid]<nums[mid+1]){
            
            left = mid+1;
        }
        else{
            
            right = mid;
        }
     }  

     return left; 
    }
}
```
## Python
```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[mid + 1]:
                right = mid
            else:
                left = mid + 1
        return left

```
# Time Complexity : O(logn) // log base 2

# Space Complexity : O(1) // constant space

Additional Note: Since this is hill slope problem pattern, low,high would be better instead of left, right
