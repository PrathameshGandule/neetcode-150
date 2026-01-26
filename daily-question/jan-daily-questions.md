# 25-01-2026
### 1984. Minimum Difference Between Highest and Lowest of K Scores
- Link : https://leetcode.com/problems/minimum-difference-between-highest-and-lowest-of-k-scores/description/?envType=daily-question&envId=2026-01-25
- Difficulty : **`EASY`**
### Description
- We're given array of scores and a num `k`
- we have to select `k` scores from array such that difference between their max and min score is minimum that is possible
### Approach
- Sort the array and use sliding windows
- Then use 2 pointers `l=0`, `r=k+1`
- iterate over the array with constant width sliding window finding minimum possible score
***
# 26-01-2026
### 1200. Minimum Absolute Difference
- Link : https://leetcode.com/problems/minimum-absolute-difference/description/?envType=daily-question&envId=2026-01-26
- Difficulty : **`EASY`**
### Description
- We're given an array if distinct integers `arr`, we have to find pairs of nums such that their difference is minimum possible that can be in that array
- Example
```bash
Input: arr = [4,2,1,3]
Output: [[1,2],[2,3],[3,4]]
Explanation: The minimum absolute difference is 1. List all pairs with difference equal to 1 in ascending order.
```
### Approach
- First we sort the array, this will make sure we only get minimum differences in one loop
- then we iterate over the array to find minimum difference their is in the array
- now we iterate over the array once again to find pair matching `minDiff` that we found from previous loop and return this vector of pairs
- Time complexity : `O(nlogn)`
- Space complexity : `O(n)` or `O(1)` depending on sorting algorithm
*** 