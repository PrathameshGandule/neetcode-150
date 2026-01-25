# 25-01-2026
### Minimum Difference Between Highest and Lowest of K Scores
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
