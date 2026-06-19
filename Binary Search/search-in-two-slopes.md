# Leetcode problem 33

# Problem name 
Search in rotated sorted array

# Pattern
 two slopes, direction, exact_search

 # Goal
 Search target element in given rotated sorted array

 # Observation
 Not a typical binary search
 There is atleast one sorted array between either left-to-mid or mid-to-right
 check target exist in sorted array and discard if not and move your range to other half.

# Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int left,right, mid;
        boolean found = false;
        left = 0;
        right = nums.length-1;


        while(left<right){
            mid = left+(right-left)/2;
            if(nums[mid]==target) {
                found = true;
                return mid;}
            else if(nums[left]<=nums[mid]){
                if((nums[left]<=target) &&(target<nums[mid])){
                    right = mid-1;
                }
                else left = mid+1;
                
            }
            else if(nums[mid]<=nums[right]){
                if((nums[mid]<=target) && (target<=nums[right])) left = mid;
                else right = mid-1;
            }
            else{
                right = mid-1;
            }
        }

        return (nums[left]==target)?left:-1;

    }
}
```

# Time Complexity : O(logn) 

# Space Complexity : O(1)
