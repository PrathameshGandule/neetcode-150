# Contains Duplicate
# Date 19-01-2026

# Problem link
- https://leetcode.com/problems/contains-duplicate/description/

# Short description
- Find duplicates in an array, if found return true, else return false
- Example
```bash
Input: nums = [1,2,3,1]
Output: true
Explanation:
The element 1 occurs at the indices 0 and 3.
```
- Difficulty : EASY

# Brute force approach
- Iterate twice over the array with i and j, where
- `i=0` and `j=i+1` for iteration to avoid false comparison with self and previous double comparsion
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int n = nums.size();
        for(int i=0 ; i<n ; i++){
            for(int j=i+1 ; j<n ; j++){
                if(nums[i] == nums[j]) return true;
            }
        }
        return false;
    }
};
```
- Time Complexity = O(n<sup>2</sup>)
- Space Complexity = O(1)
- Takes too much time, TLE for larger inputs


# Optimal approach
- Use a `unordered_set`
- Iterate over the array and see if current element can be found in the set, if found return `true`
- If not found add current element to the set
- return `false` at last if no hit in the set
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> myset;
        int n = nums.size();
        for(int i=0 ; i<n ; i++){
            if(myset.count(nums[i])) return true;
            else myset.insert(nums[i]);
        }
        return false;
    }
};
```
- Time Complexity = O(n)
  - single possible iteration over the array
- Space Complexity = O(n)
  - Max capacity of `n` size acquired for `false` output
- Better and faster than brute force 