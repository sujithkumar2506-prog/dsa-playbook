# Insertion Point

# Leetcode Problem : 35

# Pattern 
Insertion Point

# Goal
Search for insertion point

# Focus
focus on left, left always points to first possible insertion
move left to first possible insetion

# Key Observation
Searching for insertion is not like searching a target value,
It searches for a property, that looks for first possible insertion point.


int searchInsertion(int nums, int target){
  int left, right, mid;
  left = 0;
  right = nums.size()-1;
  while(left<=right){
    mid = left+(right-left)/2;
    if(nums[mid]==target) return mid;
    else if(nums[mid]<target) left = mid+1;
    else right = mid+1;
    }
  return l+1;      
    }

# Time Complexity : O(logn) // log base 2
# Space Complexity: O(1)

    
