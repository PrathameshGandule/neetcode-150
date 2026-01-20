# Two Sum
# Date 19-01-2026
# Problem link
- https://leetcode.com/problems/two-sum/description/

# Description
- Given an array `nums` return index of 2 such numbers that add upto `target`
- Assume single, distinct(index) and for sure solution exists for each case
- Example
```bash
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

# Approach 1
- Nested iteration over the array level 2
- `i=0` and `j=i+1` to avoid repetitive and false answers
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        for(int i=0 ; i<n ; i++){
            for(int j=i+1 ; j<n ; j++){
                if(
                    nums[i]+nums[j] == target
                ) return { i, j };
            }
        }
        return {-1, -1};
    }
};
```
- Time complexity : O(n<sup>2</sup>)
- Space complexity : O(1)
- Very inefficient, takes forever

# Approach 2
- create a `unordered_map<int, int>` 
- store the `nums[i]` in `first` and index `i` in `second` of umap
- now we store the `nums[i]` in first because that's what we are searching for, it's the key in umap, keys are searchable with `O(1)` complexity, something that I get confused with sometimes
- basically as we iterate over the array we calculate `complement` which is `target - nums[i]` for curr if we found the complement in umap then we can say we found the solution, return `{ i, umap[comp] }` 
- and continue to add the `umap[nums[i]] = i` as we proceed in iteration
- else return `{-1,-1}` at the end 
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        unordered_map<int, int> umap;
        int comp = 0;
        for(int i=0 ; i<n ; i++){
            comp = target - nums[i];
            if(umap.find(comp) != umap.end()){
                return { i, umap[comp] };
            }
            umap[nums[i]] = i;
        }
        return {-1, -1};
   }
};
```
- Time complexity : O(n)
- Space complexity : O(n)

***