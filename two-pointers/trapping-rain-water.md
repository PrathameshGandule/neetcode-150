# Trapping rain water
# Date 25-01-2026
# Problem link
- https://leetcode.com/problems/trapping-rain-water/description/
# Description
- We're given an array of integers representing elevation of blocks across a line
- lets say if it rain's suddenly, how many blocks of water can this distributed blocks trap in them?
- we have to calculate total amount blocks that will be filled by rainwater, considering everything fills to its maximum capacity
- Example

![blocks image from leetcode](../assets/rainwatertrap.png)
```bash
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```
# Approach one - `extra space for max left & right`
- we create 2 new vectors to store `maxLeft` and `maxRight` for current element

|index|0|1|2|3|4|5|6|7|8|9|10|11|
|-|-|-|-|-|-|-|-|-|-|-|-|-|
|input|0|1|0|2|1|0|1|3|2|1|2|1|
|maxLeft|0|0|1|1|2|2|2|2|3|3|3|3|
|maxRight|3|3|3|3|3|3|3|2|2|2|1|0|
|min(L,R)|0|0|1|1|2|2|2|2|2|2|1|0|
|min(L,R) - input|0|-1|**`1`**|-1|**`1`**|**`2`**|**`1`**|-1|0|**`1`**|-1|-1|
- blocks that are filled = 1 + 1 + 2 + 1 + 1 = **`6`**
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        vector<int> maxLeft(n);
        vector<int> maxRight(n);
        int leftmax = 0;
        int rightmax = 0;
        int res = 0, temp = 0;
        for(int i=0 ; i<n ; i++){
            maxLeft[i] = leftmax;
            leftmax = max(leftmax, height[i]);
        }
        for(int i=n-1 ; i>=0 ; i--){
            maxRight[i] = rightmax;
            rightmax = max(rightmax, height[i]);
        }
        for(int i=0 ; i<n ; i++){
            temp = min(maxLeft[i], maxRight[i]) - height[i];
            if(temp > 0) res += temp;
        }
        return res;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(n)
# Approach 2 - two pointers
- In this approach we use 2 pointers `l` & `r` and `leftMax` & `rightMax` vars
- if `leftMax < rightMax` we do `l++` then set `leftMax` to new value according to curr element and do `res += leftMax - height[l]`
- else we do `r--` then set `rightMax` to new value according to curr element and do `res += rightMax - height[r]`
- then we return the `res`
- Below is my solution which is little quirky
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        int maxL = height[0], maxR = height[n-1];
        int isModeL;
        if(maxL <= maxR) isModeL = true;
        else isModeL = false;
        int l=0, r=n-1;
        int res = 0;
        int temp = 0;
        while(l < r){
            if(isModeL){
                temp = maxL - height[l];
                if(temp > 0) res += temp;
            } else {
                temp = maxR - height[r];
                if(temp > 0) res += temp;
            }
            if(height[l] <= height[r]){
                maxL = max(maxL, height[l]);
                l++;
                isModeL = true;
            } else {
                maxR = max(maxR, height[r]);
                r--;
                isModeL = false;
            }
        }
        return res;
    }
};
```
- Below is solution from `neetcode` which is little better
- Both of them are same but mine is little different
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        if (height.empty()) {
            return 0;
        }
        int l = 0, r = height.size() - 1;
        int leftMax = height[l], rightMax = height[r];
        int res = 0;
        while (l < r) {
            if (leftMax < rightMax) {
                l++;
                leftMax = max(leftMax, height[l]);
                res += leftMax - height[l];
            } else {
                r--;
                rightMax = max(rightMax, height[r]);
                res += rightMax - height[r];
            }
        }
        return res;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(1)
***