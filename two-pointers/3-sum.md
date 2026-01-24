# 3 Sum
# Date 24-01-2026
# Problem link
- https://leetcode.com/problems/3sum/description/
# Description
- Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.
- Notice that the solution set must not contain duplicate triplets.
- Example
```bash
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```
# Approach 1
- A brute force approach here would be to iterate over the array in triple nested loop and loo for triplets that make total sum of 0
- we have to make sure no duplicate entries go in result vector
- and all the nums in a triplet are unique
- This is inefficient and may give TLE

# Approach 2
- This approach is better than brute but still mid level
- We create a `unordered_map<int, int>` from input array for `O(1)` lookup 
- We fixate a num and since we're finding a triplet who's sum is zero, we try to set new `target=0-nums[i]`, and now we search for a pair of this number through standard [two sum](../arrays/two-sum.md) approach with `unordered_map<int, int>`
- we make sure all condition's are met like triplets are unique and individual numbers in triplet are unique
- to do this we sort the triplet and push it in a set of vectors - `set<vector<int>>` so that we only get unique answers
- then at last we get this set in `vector<vector<int>>` as needed for answer and completed
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        unordered_map<int, int> vals;
        int n = nums.size();
        int tar1, comp;
        set<vector<int>> myset;
        vector<int> temp;
		// filling the lookup umap
        for(int i=0 ; i<n ; i++){
            vals[nums[i]] = i;
        }
        for(int i=0 ; i<n ; i++){
			// setting a target to find
            tar1 = 0 - nums[i];
			// standard 2 sum
            for(int j=i+1 ; j<n ; j++){
                comp = tar1 - nums[j];
                if(
                    vals.find(comp) != vals.end() && 
                    i != vals[comp] &&
                    vals[comp] != j
                ){
					// sort and insert in set
                    temp = {nums[i], nums[vals[comp]], nums[j]};
                    sort(temp.begin(), temp.end());
                    myset.insert(temp);
                }
            }
        }
		// fill the 2d vector and return
        vector<vector<int>> ans(myset.begin(), myset.end());
        return ans;
    }
};
```
- Time complexity
  - activity : n + n<sup>2</sup> + n
  - `O(n^2)` effective time complexity
- Space complexity
  - activity : n + n + 3
  - `O(n)` effective
# Approach 3
- The optimal approach where we use 2 pointers
- basic idea : We sort the input array first and then fixate a target like in [approach 2](#approach-2) then use 2 pointers over sorted array like in [two-sum-II](./two-sum-II.md) problem to find the triplet
- since array is sorted we try to avoid repetitive values like we may encounter in array where `nums[i] == nums[i-1]` and same like we did in 2sum-2 we increment j if `curr < target` and decrement k if `curr > target`
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        int n = nums.size();
        int j=0, k=0, total=0;
        for(int i=0 ; i<n ; i++){
			// skipping over duplicate values
            if(i > 0 && nums[i] == nums[i-1]) continue;
            j = i+1;
            k = n-1;

            while(j < k){
				// curr val
                total = nums[i] + nums[j] + nums[k];

                if(total > 0){
                    k--;
                } else if (total < 0){
                    j++;
                } else {
                    res.push_back({ nums[i], nums[j], nums[k] });
                    j++;
					// skip over duplicate this way we don't need a new set to fill get only unique vals
                    while(nums[j] == nums[j-1] && j < k){
                        j++;
                    }
                }
            }
        }
        return res;
    }
};
```
- Time complexity : O(n<sup>2</sup>)
- Space complexity : O(n) or O(1) depending on sorting algo
***