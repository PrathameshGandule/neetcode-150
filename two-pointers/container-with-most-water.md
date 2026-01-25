# Container with most water
# Date 25-01-2026
# Problem link
- https://leetcode.com/problems/container-with-most-water/description/
# Description
- You're given an array `height`
- if we consider 2 heights to be walls of a 2d container that holds water to it's fullest, we have to find 2 heights such that they can hold maximum amount of water in them

![container image](../assets/water_container.jpg)

- Example
```bash
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```
# Approach 1 - double nested loop
- In this approach we simply try to simulate this problem by iterating over the `height` array with double nested loop
- at each iteration we calculate maxarea by comparing `maxarea` and current area between `i` and `j`, then we return the `maxarea`
- this solution is inefficient and may give TLE
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxarea = 0;
        int n = height.size();
		int currarea = 0;
        for(int i=0 ; i<n ; i++){
            for(int j=i+1 ; j<n ; j++){
				currarea = min(height[i], height[j])*(j-i);
                maxarea = max(maxarea, currarea);
            }
        }
        return maxarea;
    }
};
```
- Time complexity : O(n<sup>2</sup>)
- Space complexity : O(1)

# Approach 2 - two pointers
- In this approach we use two pointers iterating over the array
- `l=0` and `r=n-1` where `n` is size of `height`
- we get maxarea like previous problem by comparing current and max areas
- we move the pointer which is smaller in to it's next position
  - `l++` if `height[l] <= height[r]` (necessary to accomodate `==` condition somewhere to avoid confusion)
  - `r--` if `height[l] > height[r]`
- then we return `maxarea`
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxarea = 0;
        int n = height.size();
        int l=0, r=n-1;
        int currarea = 0;
        while(l < r){
            currarea = min(height[l], height[r])*(r-l);
            maxarea = max(maxarea, currarea);
            if(height[l] <= height[r]) l++;
            else if (height[l] > height[r]) r--;
        }
        return maxarea;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(1)
***