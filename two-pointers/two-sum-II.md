# Two Sum II
# Date 24-01-2026
# Problem link
- https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/
# Desciption
- we're given an 1-indexed array sorted in non-decreasing order
- we have to find 2 nums such that there sum is equal to `target`
- return the indexes of such numbers
- Example
```bash
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```
# Approach 1
- We may use `unordered_map<int, int>` like used in original [two-sum](../arrays/two-sum.md)
- but since here array is sorted in increasing order we may leverage the use of 2 pointers from both sides
- we take sum of cuurent position and if current sum if more than needed we move left pointer to right so that we can get bigger num
- similarly if current number is lesser than needed we move the right pointer to left in hope to find a smaller sum
```cpp
target=9

  2  7  11  15 
  l          r

sum = 17 > 9 -> r--

  2  7  11  15 
  l      r

sum = 13 > 9 -> r--

  2  7  11  15 
  l  r

sum = 9 == 9 -> found(return indices)
```
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l=0, r=numbers.size()-1;
        int curr = 0;
        while(l < r){
            curr = numbers[l] + numbers[r];
            if(curr == target) return { l+1, r+1 };
            else if (curr < target) l++;
            else if (curr > target) r--;
        }
        return { -1, -1 };
    }
};
```
- Time complexity : O(n)
- Space complexity : O(1)
# Quick Intuition
- use of two pointers lessen the space and time complexity
***