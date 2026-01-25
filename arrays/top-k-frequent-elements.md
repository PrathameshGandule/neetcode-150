# Top k frequent elements
# Date 20-01-2026
# Problem link
- https://leetcode.com/problems/top-k-frequent-elements/

# Description
- There's an array `nums` with repeated numbers, we have to return `k` amount of top frequent elements, so like only return k numbers which have occured most number of times in the array
Example
```bash
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
# Approach 1 - `max heap (priority queue)`
- Now first approach was to use a [max heap](https://www.geeksforgeeks.org/cpp/max-heap-in-cpp/) which is used using priority queue from STL in C++, which stores the maximum values at top, as it's a complete binary tree where always `val(parent) >= val(child)` so we always get the top element when we pop
- But implementation for that was hard in cpp so I didn't do it : )

# Approach 2 - `unordered map and index bucket sort`
- This ones better than max heap
- We count the occurences of each element first with a `unordered_map<int, int>`
- Then create a `vector<vector<int>>` with size `n+1` where n is size of input array
- Here we're going to iterate over the umap and push the elements with same count in one bucket
- This concept is called a bucket sort

|count|0|1|2|3|4|5|6|
|-|-|-|-|-|-|-|-|
|nums|-|{3}|{2}|{1}|-|-|-|

- Now we iterate from end and pick only the `k` amount of elements in answer `vector<int>`
```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> umap;
        int n = nums.size();
        for(int num : nums){
            umap[num]++;
        }
        vector<vector<int>> count(n+1);
        for(auto ele : umap){
            count[ele.second].push_back(ele.first);
        }
        vector<int> res;
        for(int i=n ; i>=0 ; i--){
            for(int num : count[i]){
                if(k > 0){
                    res.push_back(num);
                    k--;
                } else break;
            }
        }
        return res;
    }
};
```
- Time Complexity : O(n)
- Space Complexity : O(n)

***

