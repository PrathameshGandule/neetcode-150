# Longest consecutive sequence
# Date 24-01-2026
# Problem link
- https://leetcode.com/problems/longest-consecutive-sequence/description/
# Description
- We are given a unsorted array `nums` we have to find longest consecutive sequence
- Example
```bash
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```
# Approach 1
- We sort the nums first
- Then we iterate over them, as we now know that consecutive numbers will for sure be after one another
- we keep track using `cnt` and `cntmax` as we iterate over them, 
- for `nums` with length 0 and 1 we return 0 and 1 respectively
- to avoid edge cases like `[1,0,1,2]` where expected output is 3 but by we might get 2 as sorted array becomes `[0,1,1,2]` we skip over the same numbers while iterating over them
```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        if(n <= 1)return n;
        int cnt = 1;
        int cntmax = 1;
        for(int i=1 ; i<n ; i++){
            if(nums[i] == nums[i-1]) continue;
            if(nums[i] == nums[i-1]+1) cnt++;
            else{
                cntmax = max(cntmax, cnt);
                cnt=1;
            }
        }
        cntmax = max(cntmax, cnt);
        return cntmax;
    }
};
```
- Time complexity
  - activity = nlog(n) + n 
  - `O(nlogn)` as we are using `sort` function here
- Space complexity
  - activity = n or 1
  - `O(n)` or `O(1)` depending or sorting algorithm used or to account for it or not

# Approach 2
- In this approach we are going to use a `unordered_set<int>`
- we fill the set with numbers from `nums`
- then we iterate over the set to see if we can get `curr+1` in set if so we increment a temp cnt var
- then we continue this until this streak is broken, then we get the `cntmax = max(cnt, cntmax);`
- to avoid reiterating for every num in numset we check if that number can actually be start of a sequence, by checking if a `curr-1` exists in set, if it does that means it must be part of some other sequence so we skip inner loop checking for it
```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)return 0;
        unordered_set<int> numSet(nums.begin(), nums.end());
        int cnt=1, cntmax=1;
        int length=1;
        for(int num : numSet){
            if(numSet.find(num-1) != numSet.end()) continue;
            while(numSet.find(num+length) != numSet.end()){
                length++;
                cnt++;
            }
            cntmax=max(cnt, cntmax);
            cnt=1;
            length=1;
        }
        return cntmax;
    }
};
```
- Time complexity
  - activity : n + n
  - `O(n)` as each number is possibly visited once only
- Space complexity
  - `O(n)` extra to store the unordered_set

***