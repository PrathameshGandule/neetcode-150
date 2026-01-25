# Product of Array except self
# Date 21-01-2026
# Problem link
- https://leetcode.com/problems/product-of-array-except-self/description/

# Desciption
- We are given an array `nums` we have to return an array containing product of all other elements except current element
- Example
```bash
Input: nums = [1,2,3,4]
Output: [24,12,8,6]

24 = 2 x 3 x 4
12 = 1 x 3 x 4
8 = 1 x 2 x 4
6 = 1 x 2 x 3
```
# Approach 1 - `product of all and divide`
- First approach would be to just calculate product of all numbers in array
- then iterate over the input array and putting value for current index as whole product divided by current num
- just we have to watch out for 2 edge cases
  - if there exists exactly 1 `0` in input , we have to calculate whole product except for that zero and put that prod there and other nums as zero in result, as multiplication with 0 is always zero
  - if there exists more than 1 zero then whole array is going to be filled with zero only
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int prod = 1;
        int indexZero = -1;
        int zeroCount = 0;
        for(int i=0 ; i<nums.size() ; i++){
            if(nums[i] == 0){
                indexZero = i;
                zeroCount++;
                continue;
            }
            prod *= nums[i];
        }
        vector<int> res(nums.size());
        if(zeroCount > 1){
            fill(res.begin(), res.end(), 0);
        } else if(indexZero != -1){
            fill(res.begin(), res.end(), 0);
            res[indexZero] = prod;
        } else {
            for(int i=0 ; i<nums.size() ; i++){
                res[i] = prod/nums[i];
            }
        }
        return res;
    }
};
```
- Time complexity : O(n);
- Space complexity : O(1)
- It uses division, there exists a solution without using division

# Approach 2 - `prefix product method`
- Here we use a prefix sum method
- We create 2 array prefix and postfix
- we store the product of previous elements for that num in prefix and vice versa for postfix

|index|0|1|2|3|
|-|-|-|-|-|
|input|1|2|3|4|
|prefix|1|1|2|6|
|postfix|24|12|4|1|
|output|24|12|8|6|
- here output element is equal to `prefix[i] * postfix[i`
- for values non-existent like `prefix[-1]` or `postfix[n]` we take 1
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int temp = 1;
        int n = nums.size();
        vector<int> prefix(n, 1);
        vector<int> postfix(n, 1);
        prefix[0] = 1;
        for(int i=1 ; i<n ; i++){
            temp *= nums[i-1];
            prefix[i] = temp;
        }
        temp = 1;
        postfix[n-1] = 1;
        for(int i=n-2 ; i>=0 ; i--){
			temp *= nums[i+1];
            postfix[i] = temp;
        }
        vector<int> res;
        for(int i=0 ; i<n ; i++){
            res.push_back(prefix[i] * postfix[i]);
        }
        return res;
    }
};
```
- Time complexity : O(n)
- Space Complexity : O(n)
- Takes extra space
# Approach 3
- This approach is same as previous
- but we don't use an extra space this time
- we fill the output array using 2 passes
- we keep multiplying elements once from left and one from right, prefix and postfix respectively
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> res(n, 1);
        int pref = 1;
        for(int i=0 ; i<n ; i++){
            res[i] = pref;
            pref *= nums[i];
        }
        int post = 1;
        for(int i=n-1 ; i>=0 ; i--){
            res[i] *= post;
            post *= nums[i];
        }
        return res;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(1)
***