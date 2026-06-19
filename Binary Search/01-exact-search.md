# Exact Search

# Leetcode Problem - 704
# Pattern : exact search
# Goal 
to find the target value in an array.
## focus 
On mid value , move mid until it equal the target and return mid value.
mistakes : No mistakes, just a very basic binary search algo implementation.
# Key Insight
Whenever nums[left]<target, 
values on the left of mid, can never have target,
so Discard that half.

# Code
'''c
int findindex(int &nums,int target){
  int left, right, mid;
  left = 0;
  right = nums.size()-1;
  while(left<=right){
    mid = left+(right-left)/2;
    if(nums[mid]==target) return mid;
    else if(nums[mid]<target) l = mid+1;
    else r = mid-1;
  }
  return -1;  // -1 indicates that the target element is not found in array.
}
'''
Time Complexity : O(logn)  // log base 2 to the n.
Space Complexity : O(1)
